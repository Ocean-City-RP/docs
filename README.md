# Advanced FiveM Core Framework

> [!WARNING]
> **DEVELOPMENT STATUS: PRE-ALPHA**
> 
> This framework is currently under heavy development and is NOT ready for production use.
> Many features are incomplete, untested, or may change significantly.
> Using this in a live server environment is NOT recommended at this time.
> 
> Please check back later for a stable release.

A robust and modular core framework for FiveM servers that provides essential functionality for building custom scripts and resources.

## Features (WIP)

### Player Management
- Persistent player data storage
- Secure money management system
- Job system with grades
- Position tracking
- Character info management
- Admin system with permission levels
- Status system (Health, Stamina, Hunger, Thirst)
- Death system with admin revive

### Admin System
- Multiple admin levels (User, Helper, Moderator, Admin, Superadmin)
- Permission-based commands
- Admin management commands
- Persistent admin storage
- Status management commands
- Revive system

### Economy System
- Server-side money operations
- Safe transaction handling
- Support for multiple currency types (cash, bank)
- Built-in anti-exploit measures

### Job System
- Multi-grade job support
- Salary system
- Job verification
- Easy job registration

### Client Utilities
- Modern notification system using ox_lib
- Progress bar system
- Progress circle system
- Context menu system
- Input dialog system
- Alert system
- Radial menu system
- Marker system
- Text UI system
- Skill check system

## Dependencies

- [oxmysql](https://github.com/overextended/oxmysql) - MySQL database wrapper
- [ox_lib](https://github.com/overextended/ox_lib) - UI and utility library
- [ox_inventory](https://github.com/overextended/ox_inventory) - Inventory system

## Installation

1. Ensure you have the required dependencies installed
2. Clone this repository into your resources folder
3. Import the database structure (automatically created on first run)
4. Add the following to your server.cfg:
```
ensure oxmysql
ensure ox_lib
ensure ox_inventory
ensure core
```

## Framework settings
set inventory:framework "ox"

## Inventory Integration

The framework is built to work seamlessly with ox_inventory by implementing:

### Server-side
```lua
-- Get player data in ox format
exports('GetPlayerData', function(source)
    local player = Players[source]
    return {
        source = source,
        identifier = player.license,
        name = player.name,
        groups = player.groups,
        sex = player.charinfo.gender,
        dateofbirth = player.charinfo.birthdate
    }
end)

-- Get player groups/permissions
exports('GetPlayerGroup', function(source)
    return Players[source]?.groups or {}
end)
```

### Client-side
```lua
-- Player data structure matches ox expectations
PlayerData = {
    identifier = license,
    source = serverId,
    groups = {},
    ...
}

-- Notify ox when player loads
TriggerEvent('ox:playerLoaded', PlayerData)
```

For more information on using ox_inventory, see their [documentation](https://overextended.dev/ox_inventory).

## Database Structure

The framework automatically creates the following tables:

### Players Table
```sql
CREATE TABLE IF NOT EXISTS `players` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `cid` varchar(50) DEFAULT NULL,
    `license` varchar(50) DEFAULT NULL,
    `name` varchar(50) DEFAULT NULL,
    `money` longtext DEFAULT NULL,
    `charinfo` longtext DEFAULT NULL,
    `position` longtext DEFAULT NULL,
    PRIMARY KEY (`id`),
    UNIQUE KEY `license` (`license`)
);
```

### Admins Table
```sql
CREATE TABLE IF NOT EXISTS `admins` (
    `license` varchar(50) PRIMARY KEY,
    `name` varchar(50) NOT NULL,
    `level` int NOT NULL DEFAULT 0
);
```

## Usage Examples

### Player Management
```lua
-- Server-side
-- Get player data
local player = Players[source]

-- Set player money
exports[Config.CoreName]:SetPlayerMoney(source, 'cash', 1000)

-- Set player job
exports[Config.CoreName]:SetPlayerJob(source, 'police', 1)

-- Client-side
-- Get player data
local PlayerData = exports[Config.CoreName]:GetPlayerData()
```

### Admin System
```lua
-- Check admin level
local adminLevel = exports[Config.CoreName]:IsPlayerAdmin(source)

-- Add admin
exports[Config.CoreName]:AddAdmin(license, Admin.Levels.ADMIN)

-- Remove admin
exports[Config.CoreName]:RemoveAdmin(license)

-- Admin Commands
/addadmin [id] [level]    -- Add new admin
/removeadmin [id]         -- Remove admin
```

### Economy System
```lua
-- Add money
exports[Config.CoreName]:AddMoney(source, 'cash', 1000)

-- Remove money
exports[Config.CoreName]:RemoveMoney(source, 'bank', 500)

-- Economy Commands
/givemoney [cash/bank] [amount]     -- Give money
/removemoney [cash/bank] [amount]   -- Remove money
```

### Job System
```lua
-- Register new job
exports[Config.CoreName]:RegisterJob('police', {
    label = 'Police Department',
    grades = {
        [0] = {
            label = 'Cadet',
            salary = 500
        },
        [1] = {
            label = 'Officer',
            salary = 750
        }
    }
})

-- Check job
if Jobs.JobExists('police') then
    -- Job exists
end

-- Get job info
local jobLabel = Jobs.GetJobLabel('police')
local gradeLabel = Jobs.GetGradeLabel('police', 1)
local salary = Jobs.GetSalary('police', 1)

-- Job Commands
/setjob [jobname] [grade]   -- Set player job
```

### Client Utilities
```lua
-- Notifications
exports[Config.CoreName]:ShowNotification('Hello World', 'success')
exports[Config.CoreName]:ShowAdvancedNotification({
    title = 'Title',
    description = 'Description',
    type = 'info',
    duration = 5000
})

-- Progress Bar
exports[Config.CoreName]:ProgressBar({
    duration = 5000,
    label = 'Processing...',
    useWhileDead = false,
    canCancel = true
})

-- Progress Circle
exports[Config.CoreName]:ProgressCircle({
    duration = 5000,
    position = 'middle',
    label = 'Searching...'
})

-- Menu
exports[Config.CoreName]:CreateMenu({
    id = 'example_menu',
    title = 'Example Menu',
    options = {
        {label = 'Option 1', value = 1},
        {label = 'Option 2', value = 2}
    }
})

-- Input Dialog
local input = exports[Config.CoreName]:TextInput({
    title = 'Enter Name',
    label = 'Name'
})

-- Marker
local marker = exports[Config.CoreName]:CreateMarker({
    coords = vector3(100.0, 100.0, 100.0),
    type = 1,
    scale = vec3(1.0, 1.0, 1.0),
    color = {r = 255, g = 0, b = 0, a = 100}
})

-- Text UI
exports[Config.CoreName]:ShowTextUI('Press [E] to interact', {
    position = "right-center",
    icon = 'hand'
})
```

### Utility Commands
```
/myinfo    -- Show character info
/getpos    -- Get current position
/corehelp  -- Show available commands
```

### Status System
```lua
-- Server-side
exports[Config.CoreName]:UpdatePlayerStatus(source, 'hunger', 100)
exports[Config.CoreName]:GetPlayerStatus(source, 'thirst')

-- Client-side
-- Status is automatically synced and displayed in HUD
-- Health is managed through native GTA health system
```

### Death System
```lua
-- Server-side
-- Use admin command to revive
/revive [playerId]

-- Client-side
-- Death state is automatically handled
-- Players remain dead until revived by admin
```

## Configuration
```lua
Config.Status = {
    -- Update intervals
    UpdateInterval = 10000,      -- How often server updates status (ms)
    UIUpdateInterval = 1000,     -- How often UI updates (ms)
    
    -- Decrease rates
    DecreaseRates = {
        hunger = 0.3,
        thirst = 0.5
    },
    
    -- Health settings
    Health = {
        min = 0,
        max = 200,               -- GTA's health range
        regenThreshold = 80,     -- Hunger/Thirst must be above this for health regen
        regenRate = 1,           -- Health points restored per interval
        damageThreshold = 20,    -- Start taking damage when hunger/thirst below this
        damageMultiplier = 0.5   -- Damage multiplier for low hunger/thirst
    }
}
```

## Debug System
```lua
Config.Debug = {
    enabled = true,           -- Master switch for debug mode
    status = {
        showUpdates = true,   -- Show status value updates
        showThreads = true,   -- Show thread starts/stops
        showEffects = true,   -- Show when effects are applied
        showAnimations = true -- Show animation loading
    },
    logLevel = 'DEBUG'       -- Default log level when debug is enabled
}
```

## Admin Commands
```
/revive [id]          -- Revive a player (or self if no ID)
/sethunger [id] [value] -- Set player's hunger
/setthirst [id] [value] -- Set player's thirst
/setstamina [id] [value] -- Set player's stamina
```