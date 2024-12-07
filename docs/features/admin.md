---
layout: default
title: Admin System
parent: Features
nav_order: 4
---

# Admin System

## Overview

The admin system provides comprehensive server management tools with multiple permission levels.

## Features

- Multiple admin levels
- Permission-based commands
- Persistent admin storage
- Admin action logging

## Admin Levels

```lua
Admin.Levels = {
    USER = 0,
    HELPER = 1,
    MODERATOR = 2,
    ADMIN = 3,
    SUPERADMIN = 4
}
```

## Commands

### Player Management
```lua
/addadmin [id] [level]     -- Add new admin
/removeadmin [id]          -- Remove admin
/kick [id] [reason]        -- Kick player
/ban [id] [duration]       -- Ban player
/unban [license]           -- Unban player
```

### Player Assistance
```lua
/revive [id]              -- Revive player
/heal [id]                -- Heal player
/teleport [id]            -- Teleport to player
/bring [id]               -- Bring player to you
```

### Server Management
```lua
/announce [message]        -- Server announcement
/setweather [type]        -- Set weather
/settime [hour]           -- Set time
```

## API Usage

### Server-side
```lua
-- Check admin level
local level = exports[Config.CoreName]:GetAdminLevel(source)

-- Verify permission
if exports[Config.CoreName]:HasPermission(source, 'admin.kick') then
    -- Can kick players
end

-- Add admin
exports[Config.CoreName]:AddAdmin(license, Admin.Levels.ADMIN)
```

### Client-side
```lua
-- Check if player is admin
local isAdmin = exports[Config.CoreName]:IsAdmin()

-- Get admin level
local level = exports[Config.CoreName]:GetAdminLevel()
``` 