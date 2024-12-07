---
layout: default
title: Configuration
parent: Setup
nav_order: 2
---

# Configuration Guide

## Core Configuration

The main configuration file (`config.lua`) contains all core settings:

### Status System
```lua
Config.Status = {
    UpdateInterval = 10000,      -- Server status update interval (ms)
    UIUpdateInterval = 1000,     -- UI update interval (ms)
    
    DecreaseRates = {
        hunger = 0.3,
        thirst = 0.5
    },
    
    Health = {
        min = 0,
        max = 200,
        regenThreshold = 80,
        regenRate = 1,
        damageThreshold = 20,
        damageMultiplier = 0.5
    }
}
```

### Debug Options
```lua
Config.Debug = {
    enabled = true,
    status = {
        showUpdates = true,
        showThreads = true,
        showEffects = true,
        showAnimations = true
    },
    logLevel = 'DEBUG'
}
```

## Admin Configuration

Configure admin levels in `config/admin.lua`:

```lua
Config.AdminLevels = {
    USER = 0,
    HELPER = 1,
    MODERATOR = 2,
    ADMIN = 3,
    SUPERADMIN = 4
}
```

## Inventory Settings

Modify inventory integration in `config/inventory.lua`. 