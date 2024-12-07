---
layout: default
title: Installation
parent: Setup
nav_order: 1
---

# Installation Guide

## Prerequisites

Before installing, ensure you have:

1. A running FiveM server
2. MySQL database server
3. Required dependencies:
   - [oxmysql](https://github.com/overextended/oxmysql)
   - [ox_lib](https://github.com/overextended/ox_lib)
   - [ox_inventory](https://github.com/overextended/ox_inventory)

## Installation Steps

1. Clone the repository into your resources folder:
```bash
cd resources
git clone https://github.com/yourusername/fivem-core-framework.git core
```

2. The database structure will be automatically created on first run

3. Add to your server.cfg:
```cfg
ensure oxmysql
ensure ox_lib
ensure ox_inventory
ensure core

# Framework settings
set inventory:framework "ox"
```

## Database Structure

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

## Verification

1. Start your server
2. Check console for any errors
3. Try connecting and using `/myinfo` 