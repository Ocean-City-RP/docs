---
layout: default
title: Client Utilities
parent: Features
nav_order: 5
---

# Client Utilities

## Overview

The framework provides a comprehensive set of client-side utilities for UI and interaction.

## Notification System

```lua
-- Basic notification
exports[Config.CoreName]:ShowNotification('Hello World', 'success')

-- Advanced notification
exports[Config.CoreName]:ShowAdvancedNotification({
    title = 'Title',
    description = 'Description',
    type = 'info',
    duration = 5000
})
```

## Progress Systems

### Progress Bar
```lua
exports[Config.CoreName]:ProgressBar({
    duration = 5000,
    label = 'Processing...',
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
})
```

### Progress Circle
```lua
exports[Config.CoreName]:ProgressCircle({
    duration = 5000,
    position = 'middle',
    label = 'Searching...'
})
```

## Menu Systems

### Context Menu
```lua
exports[Config.CoreName]:CreateMenu({
    id = 'example_menu',
    title = 'Example Menu',
    options = {
        {label = 'Option 1', value = 1},
        {label = 'Option 2', value = 2}
    }
})
```

### Input Dialog
```lua
local input = exports[Config.CoreName]:TextInput({
    title = 'Enter Name',
    label = 'Name'
})
```

## Visual Elements

### Markers
```lua
local marker = exports[Config.CoreName]:CreateMarker({
    coords = vector3(100.0, 100.0, 100.0),
    type = 1,
    scale = vec3(1.0, 1.0, 1.0),
    color = {r = 255, g = 0, b = 0, a = 100}
})
```

### Text UI
```lua
exports[Config.CoreName]:ShowTextUI('Press [E] to interact', {
    position = "right-center",
    icon = 'hand'
})
``` 