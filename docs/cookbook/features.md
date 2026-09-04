# What is a Feature?

A feature is a component of a game, such as computers, player movement, entities, etc.

## Feature-driven architecture

Office Nowhere utilizes a concept known as **Feature-driven architecture**. Feature-driven architecture is a way to organize folders and scripts based on the feature they fall under.

### Computer feature example

```tree title="ReplicatedStorage"
nowhere/
    features/
        computer/
            cli/
            core/
            files/
            gui/
            disableEmoteWheel.client.lua
            observe.client.lua
```

```tree title="ServerScriptService"
nowhere/
    features/
        computer/
            gui/
            observe.server.lua
            sendToWebhook.server.lua
```

Inside of the features folder, all scripts and modules responsible for handling that feature, such as computer hacking, will be placed under a folder *for* that feature. For features that use server scripts, always place them under the features folder found in `ServerScriptService`.

Now that we know where to place our features, let's make a new one!
