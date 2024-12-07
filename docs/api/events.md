---
layout: default
title: Events
parent: API Reference
nav_order: 2
---

# Events

## Server Events

### Player Events
```lua
-- Player loaded
RegisterNetEvent('core:playerLoaded', function(source, playerData)
    -- Handle player load
end)

-- Player disconnected
RegisterNetEvent('core:playerDisconnected', function(source)
    -- Handle disconnect
end)

-- Player data updated
RegisterNetEvent('core:playerDataUpdated', function(source, key, value)
    -- Handle data update
end)
```

### Money Events
```lua
-- Money changed
RegisterNetEvent('core:moneyUpdate', function(source, type, amount)
    -- Handle money update
end)

-- Transaction completed
RegisterNetEvent('core:transactionComplete', function(source, target, type, amount)
    -- Handle transaction
end)
```

### Job Events
```lua
-- Job changed
RegisterNetEvent('core:jobChanged', function(source, job, grade)
    -- Handle job change
end)

-- Salary paid
RegisterNetEvent('core:salaryPaid', function(source, amount)
    -- Handle salary payment
end)
```

## Client Events

### Player Events
```lua
-- Local player loaded
RegisterNetEvent('core:onPlayerLoaded', function(playerData)
    -- Handle local player load
end)

-- Player data sync
RegisterNetEvent('core:onPlayerDataUpdate', function(key, value)
    -- Handle data sync
end)
```

### UI Events
```lua
-- Menu item selected
RegisterNetEvent('core:onMenuSelect', function(id, selected)
    -- Handle menu selection
end)

-- Progress complete
RegisterNetEvent('core:onProgressComplete', function(id)
    -- Handle progress completion
end)
```

### Status Events
```lua
-- Status update
RegisterNetEvent('core:statusUpdate', function(status, value)
    -- Handle status update
end)

-- Death state changed
RegisterNetEvent('core:onPlayerDeath', function(isDead)
    -- Handle death state
end)
``` 