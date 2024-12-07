---
layout: default
title: Job System
parent: Features
nav_order: 2
---

# Job System

## Overview

The job system provides comprehensive job management with multiple grades and salaries.

## Features

- Multi-grade job support
- Salary system
- Job verification
- Easy job registration

## Usage

### Registering Jobs
```lua
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
```

### Job Management
```lua
-- Check job
if Jobs.JobExists('police') then
    -- Job exists
end

-- Get job info
local jobLabel = Jobs.GetJobLabel('police')
local gradeLabel = Jobs.GetGradeLabel('police', 1)
local salary = Jobs.GetSalary('police', 1)
```

## Commands

- `/setjob [jobname] [grade]`: Set player job
- `/job`: View current job info 