# Feature: "Kill Brick"

To start off, let's make a folder called "killbricks" and place it in our features folder in `ServerScriptService`, as kill bricks should be handled on the server.

```tree title="ServerScriptService"
nowhere/
    features/
        killbricks/
```

Now we may populate our killbricks folder with scripts that handle a kill brick. We need to have a server script that handles all kill brick parts, but what is the cleanest approach to handling kill bricks?

## The `Observers` package

[Observers](https://sleitnick.github.io/RbxObservers/api/Observers/) will be used frequently in the Office Nowhere codebase. Let's create a new observer that observes any instances tagged with "KillBrick"

```tree title="ServerScriptService"
nowhere/
    features/
        killbricks/
            observe.server.lua
```

```luau title="observe.server.luau"
local Observers = require("@game/ReplicatedStorage/packages/Observers")

-- Runs this function for every part that is tagged as "KillBrick".
Observers.observeTag("KilBrick", function(killBrick: BasePart)
    print("Part has tag: 'KillBrick'")
end)
```

We need to understand how an observer works. Every callback for an observer should have a cleanup function returned. When a tag is removed from a part, such as removing a "KillBrick" tag from a kill brick, the observer will call the cleanup function returned from the callback.

```luau title="observe.server.luau"
-- The function returned is called when a part loses its "Kill Brick" tag.
Observers.observeTag("KilBrick", function(killBrick: BasePart)
    print(`{killBrick.Name} has tag: 'KillBrick'`)

    return function()
        print(`{killBrick.Name} no longer has tag: 'KillBrick'`)
    end
end)
```

## Implementing our feature

Now that we understand how an observer works, we can add functionality to our kill brick. First, let's establish a step-by-step plan.

1. Create an observer that handles all parts with the "Kill Brick" tag.
2. Create a `Touched` connection for the part.
3. Validate the character in the connection.
4. Set the character's health to zero.
5. Return the cleanup function that disconnects the `Touched` connection.

```luau title="observe.server.luau"
Observers.observeTag("KilBrick", function(killBrick: BasePart)
    -- Establish the connection.
    local touchedConnection = killBrick.Touched:Connect(function(touchedPart: BasePart) 
        local character = touchedPart.Parent
        local humanoid = character and character:FindFirstChildWhichIsA("Humanoid")

        -- Returns if the touching part does not belong to a player's character.
        if not humanoid then
            return
        end

        -- Kills the player by setting their health to zero.
        humanoid.Health = 0
    end)

    return function()
        -- Disconnect the connection when the tag is removed.
        touchedConnection:Disconnect()
    end
end)
```
