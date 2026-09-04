# Requires

String requires are preferred over instance requires.

```luau
local package = require("@game/ReplicatedStorage/packages/package")
```

instead of

```luau
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local package = require(ReplicatedStorage.packages.package)
```
