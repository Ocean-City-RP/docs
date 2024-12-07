---
layout: default
title: Exports
parent: API Reference
nav_order: 1
---

# Exports

## Server Exports

### Player Management
```lua
-- Get player data
exports[Config.CoreName]:GetPlayerData(source)

-- Set player data
exports[Config.CoreName]:SetPlayerData(source, key, value)

-- Save player data
exports[Config.CoreName]:SavePlayer(source)
```

### Money Management
```lua
-- Add money
exports[Config.CoreName]:AddMoney(source, type, amount)

-- Remove money
exports[Config.CoreName]:RemoveMoney(source, type, amount)

-- Set money
exports[Config.CoreName]:SetMoney(source, type, amount)

-- Get money
exports[Config.CoreName]:GetMoney(source, type)
```

### Job Management
```lua
-- Set job
exports[Config.CoreName]:SetJob(source, job, grade)

-- Get job
exports[Config.CoreName]:GetJob(source)

-- Register job
exports[Config.CoreName]:RegisterJob(name, data)
```

### Admin System
```lua
-- Add admin
exports[Config.CoreName]:AddAdmin(license, level)

-- Remove admin
exports[Config.CoreName]:RemoveAdmin(license)

-- Check admin level
exports[Config.CoreName]:GetAdminLevel(source)
```

## Client Exports

### Player Data
```lua
-- Get local player data
exports[Config.CoreName]:GetPlayerData()

-- Get specific player data
exports[Config.CoreName]:GetPlayerDataKey(key)
```

### UI Elements
```lua
-- Show notification
exports[Config.CoreName]:ShowNotification(message, type)

-- Progress bar
exports[Config.CoreName]:ProgressBar(data)

-- Create menu
exports[Config.CoreName]:CreateMenu(data)

-- Show text UI
exports[Config.CoreName]:ShowTextUI(message, options)
```

### Utility Functions
```lua
-- Draw marker
exports[Config.CoreName]:DrawMarker(data)

-- Play animation
exports[Config.CoreName]:PlayAnimation(dict, anim, flags)

-- Request model
exports[Config.CoreName]:RequestModel(model)
``` 