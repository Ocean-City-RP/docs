---
layout: default
title: Status System
parent: Features
nav_order: 6
---

# Status System

## Overview

The status system manages player states including health, hunger, thirst, and stamina.

## Features

- Automatic status decrease over time
- Configurable decrease rates
- Health regeneration system
- Status effects
- Death system integration

## Configuration

```lua
Config.Status = {
    -- Update intervals
    UpdateInterval = 10000,      -- Server status update interval (ms)
    UIUpdateInterval = 1000,     -- UI update interval (ms)
    
    -- Decrease rates per minute
    DecreaseRates = {
        hunger = 0.3,
        thirst = 0.5
    },
    
    -- Health settings
    Health = {
        min = 0,
        max = 200,
        regenThreshold = 80,     -- Minimum hunger/thirst for health regen
        regenRate = 1,           -- Health points restored per interval
        damageThreshold = 20,    -- Start taking damage below this hunger/thirst
        damageMultiplier = 0.5   -- Damage multiplier for low status
    }
}
```

## Usage

### Server-side
```lua
-- Update player status
exports[Config.CoreName]:UpdatePlayerStatus(source, 'hunger', 100)

-- Get player status
local thirst = exports[Config.CoreName]:GetPlayerStatus(source, 'thirst')

-- Set multiple statuses
exports[Config.CoreName]:SetPlayerStatuses(source, {
    hunger = 100,
    thirst = 100
})
```

### Client-side
```lua
-- Get local player status
local hunger = exports[Config.CoreName]:GetStatus('hunger')

-- Register status effect
exports[Config.CoreName]:RegisterStatusEffect('hunger', function(value)
    if value < 20 then
        -- Apply screen effect
        SetPedMoveRateOverride(PlayerPedId(), 0.8)
    end
end)
```

## Events

### Server Events
```lua
-- Status updated
RegisterNetEvent('core:statusUpdated', function(source, status, value)
    -- Handle status update
end)

-- Player died
RegisterNetEvent('core:playerDied', function(source, killer)
    -- Handle player death
end)
```

### Client Events
```lua
-- Status sync
RegisterNetEvent('core:onStatusUpdate', function(status, value)
    -- Handle status sync
end)

-- Death state changed
RegisterNetEvent('core:onPlayerDeath', function(isDead)
    -- Handle death state
end)
```

## Commands

### Admin Commands
```lua
/setstatus [id] [status] [value] -- Set player status
/heal [id]                       -- Heal player
/revive [id]                     -- Revive player
``` 