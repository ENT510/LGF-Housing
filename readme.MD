# Client Exports

## Crate Temporany Shell

### Parameters:

```lua
---@param params table A table containing parameters for shell creation
---@field ShellId string The ID of the shell for identification
---@field HouseHash number The hash/model ID of the house to be spawned
---@field InteriorShell string The name or hash of the interior shell model
---@field CreationHouse vector4 The coordinates (x, y, z, heading) where the house should be created
---@field Heading number The heading (rotation) angle for the house's orientation
---@field onCreation function (optional) A callback function to be triggered after the shell creation

exports["LGF_Housing"]:createTemporanyShell(params)
```

## Return Values

The `export` returns three values, which represent:

- `ShecreatedHouselCreated`: The created house entity `(prop)` in the game world.
- `interiorObject`: The created interior shell entity inside the house.
- `interiorCoords`: The coordinates where the interior shell is placed (below the house).

## Example Usage

```lua
exports["LGF_Housing"]:createTemporanyShell({
    ShellId = "test_house",            -- ID of the shell
    HouseHash = 0x2d801f35,            -- House model hash
    InteriorShell = "shell_v16low",     -- Interior shell model name
    CreationHouse = vector4(1526.3882, 1399.6998, 101.2882, 136.1783), -- Spawn position for the house
    Heading = 180.0,                    -- Heading (rotation) of the house
    onCreation = function(createdHouse, interiorObject, interiorCoords)
        -- Callback function triggered after shell creation
        print("House created at:", interiorCoords)  -- Confirmation message
    end
})

```

## Delete Temporany Shell

### Parameters:

```lua
---@param shellId string The ID of the shell to be deleted


exports["LGF_Housing"]:deleteTemporanyShell(shellId)
```

## Return Values

The `export` does not return any values but will print a message indicating the success or failure of the deletion operation. Specifically:

- If the shell with the provided ID exists and is deleted, it will log: "Temporary shell and interior deleted for ID: [shellId]".
- If no shell is found with the provided ID, it will log: "No shell found with ID: [shellId]".

## Example Usage

```lua
RegisterCommand("deleteshell", function()
    exports["LGF_Housing"]:deleteTemporanyShell("test_house") -- Command to delete the temporary shell
end)
```


## Initialize All Zones

### Parameters:

```lua
---@any
exports["LGF_Housing"]:initializeAllZones()
```

## Return Values

The `initializeAllZones` export  does not return any values, but it performs the following actions:

- Loads all house data.. retrieved from the database
- Creates necessary entities for each house..
- Sets up interaction interactions based on the configuration of each house.

## Example Usage

```lua
AddEventHandler("onResourceStart", function(res)
    if GetCurrentResourceName() == res then
        InitializeAllZone()
    end
end)
```

## Delete All Temporany Shells

### Parameters:

```lua
---@any
exports["LGF_Housing"]:deleteAllTemporanyShells()
```

## Return Values

The `deleteAllTemporanyShells` export  does not return any values but will print messages indicating the status of the deletion operation for each temporary shell. Specifically:

- If a temporary shell is successfully deleted, it will log: "Temporary shell and interior deleted for ID: [shellId] during deleteAllTemporanyShells."
- After deleting all shells, it will log: "All temporary shells have been deleted.

## Example Usage

```lua
RegisterCommand("deleteallshells", function()
    exports["LGF_Housing"]:deleteAllTemporanyShells() 
end)
```