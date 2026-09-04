# Spacing

WIP

## Good example

```luau
type Counter = {
    count: number,
    thread: thread?,
}

local function counter(): Counter
    local counterTable: Counter = {
        count = 0
    }

    counterTable.thread = task.spawn(function()
        while task.wait(1) do
            counterTable.count += 1
        end
    end)

    return counterTable
end

local function main()
    local newCounter = counter()

    task.wait(3)

    thread.cancel(newCounter)
    print(newCounter.count)
end

main()

```

## Bad Example

```luau
type Counter = {
    count : number,
    thread :thread?,
}

local function counter(): Counter

    local counterTable: Counter = {
        count = 0
    }

        counterTable.thread = task.spawn(function()

            while task.wait(1) do

                counterTable.count += 1

            end

        end)

    return counterTable
end

local function main()

    local newCounter = counter()

    task.wait(3)

    thread.cancel(newCounter)
    print(newCounter.count)
end

main()
```
