# Naming variables

Naming variables helps improve code readability by letting the programmer have more information on what a variable is supposed to represent.

## What makes a variable easy to read?

Variables are easy to read when they have a clear and consise name, such as `currentMap`, `hasUpgrade` or `isEnemyActive`. Here's an example of what *NOT* to do:

```luau
local m = "The Manager"

local function g()
    return ...
end

if g() == e then
    print("e is 'The Manager'")
end
```

**Why this is bad:** Every variable and function is identified with one letter. If someone were to read this script, they wouldn't understand what `g()` and `e` are supposed to represent.

### Let's rewrite it!

```luau
local manager = "The Manager"

local function getEntity()
    return ...
end

if getEntity() == manager then
    print("entity is 'The Manager'")
end
```

Now, let's talk about how the code looks. Variables and function names are easy to understand. Compared to `g()`, `getEntity()` tells the programmer what the function does. **Don't be afraid to use long names.** As long as variable names aren't too complex, a long function name would be preferred over a vague one.
