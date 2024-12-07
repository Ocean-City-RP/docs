---
layout: default
title: Player Management
parent: Features
nav_order: 1
---

# Player Management

## Overview

The player management system handles all player-related data and operations.

## Features

- Persistent data storage
- Character information
- Money management
- Position tracking
- Status management

## Usage

### Server-side
```lua
-- Get player data
local player = Players[source]

-- Set money
exports[Config.CoreName]:SetPlayerMoney(source, 'cash', 1000)

-- Update character info
exports[Config.CoreName]:UpdateCharInfo(source, {
    firstname = "John",
    lastname = "Doe"
})
```

### Client-side
```lua
-- Get player data
local PlayerData = exports[Config.CoreName]:GetPlayerData()

-- Get specific info
local money = PlayerData.money.cash
local job = PlayerData.job
```

## Events

### Server Events
- `playerLoaded`: Triggered when player data is loaded
- `playerMoneyUpdate`: Triggered when money changes
- `characterUpdated`: Triggered when character info changes

### Client Events
- `onPlayerData`: Triggered when player data updates
- `onMoneyUpdate`: Triggered when money changes 