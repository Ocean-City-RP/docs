---
layout: default
title: Basic Usage
parent: Examples
nav_order: 1
---

# Basic Usage Examples

## Creating a Simple Script

Here's an example of a basic script using the framework:

```lua
-- client.lua
local Core = exports[Config.CoreName]
local PlayerData = {}

-- Initialize when player loads
RegisterNetEvent('core:onPlayerLoaded', function(data)
    PlayerData = data
    
    -- Show welcome message
    Core:ShowNotification('Welcome ' .. PlayerData.name, 'success')
end)

-- Example command to check money
RegisterCommand('checkmoney', function()
    local cash = Core:GetMoney('cash')
    local bank = Core:GetMoney('bank')
    
    Core:ShowNotification(string.format('Cash: $%d\nBank: $%d', cash, bank))
end)

-- Example of using progress bar
RegisterCommand('repair', function()
    Core:ProgressBar({
        duration = 5000,
        label = 'Repairing Vehicle...',
        useWhileDead = false,
        canCancel = true,
        controlDisables = {
            disableMovement = true,
            disableCarMovement = true,
            disableMouse = false,
            disableCombat = true
        },
        animation = {
            animDict = "mini@repair",
            anim = "fixing_a_player"
        }
    }, function(cancelled)
        if not cancelled then
            -- Repair complete
            local vehicle = GetVehiclePedIsIn(PlayerPedId(), false)
            SetVehicleFixed(vehicle)
        end
    end)
end)
```

```lua
-- server.lua
local Core = exports[Config.CoreName]

-- Example of giving money to player
RegisterCommand('givemoney', function(source, args)
    if Core:GetAdminLevel(source) < 2 then return end
    
    local target = tonumber(args[1])
    local amount = tonumber(args[2])
    
    if target and amount then
        Core:AddMoney(target, 'cash', amount)
        Core:ShowNotification(source, 'Money given to player', 'success')
    end
end)

-- Example of registering a new job
Core:RegisterJob('mechanic', {
    label = 'Mechanic Shop',
    grades = {
        [0] = {
            label = 'Trainee',
            salary = 500
        },
        [1] = {
            label = 'Mechanic',
            salary = 750
        },
        [2] = {
            label = 'Senior Mechanic',
            salary = 1000
        }
    }
})
```

## Creating a Shop System

Here's an example of implementing a basic shop:

```lua
-- client.lua
local function OpenShop()
    Core:CreateMenu({
        id = 'shop_menu',
        title = 'General Store',
        options = {
            {label = 'Water - $5', value = 'water', price = 5},
            {label = 'Bread - $3', value = 'bread', price = 3},
            {label = 'Phone - $100', value = 'phone', price = 100}
        }
    })
end

-- Create shop marker
CreateThread(function()
    local coords = vector3(25.7, -1347.3, 29.5)
    
    while true do
        local sleep = 1000
        local playerCoords = GetEntityCoords(PlayerPedId())
        
        if #(playerCoords - coords) < 10.0 then
            sleep = 0
            Core:DrawMarker({
                coords = coords,
                type = 1,
                scale = vec3(1.0, 1.0, 1.0),
                color = {r = 0, g = 255, b = 0, a = 100}
            })
            
            if #(playerCoords - coords) < 1.5 then
                Core:ShowTextUI('Press [E] to open shop')
                if IsControlJustPressed(0, 38) then -- E key
                    OpenShop()
                end
            end
        end
        
        Wait(sleep)
    end
end)
``` 