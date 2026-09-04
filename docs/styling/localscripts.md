# No LocalScripts

The concept of not having LocalScripts may seem confusing, but there is a valid reason for the deprecation of LocalScripts.

## Use `RunContext` instead

Normal scripts have a RunContext attribute, which determines what environment the script will run under. Now, scripts with a RunContext of "Client" can be ran in ReplicatedStorage.

## Why?

Debugging a LocalScript is often painful as clicking an error produced from a LocalScript will not take you to where the error was produced. Additionally, organizing LocalScripts is trivial as many LocalScripts will be spread out between `StarterPlayerScripts`, `StarterCharacter`, and `StarterGui`. With the RunContext approach, all client scripts can be placed under one service: ReplicatedStorage.
