---
layout: default
title: Economy System
parent: Features
nav_order: 3
---

# Economy System

## Overview

The economy system provides secure money management with anti-exploit measures and support for multiple currency types.

## Features

- Server-side money operations
- Multiple currency types (cash, bank)
- Transaction logging
- Anti-exploit protection

## Usage

### Server-side Operations
```lua
-- Add money
exports[Config.CoreName]:AddMoney(source, 'cash', 1000)

-- Remove money
exports[Config.CoreName]:RemoveMoney(source, 'bank', 500)

-- Check balance
local balance = exports[Config.CoreName]:GetMoney(source, 'cash')

-- Transfer money
exports[Config.CoreName]:TransferMoney(source, target, 'bank', amount)
```

### Client-side Usage
```lua
-- Get current balance
local cash = exports[Config.CoreName]:GetMoney('cash')
local bank = exports[Config.CoreName]:GetMoney('bank')

-- Request payment
exports[Config.CoreName]:RequestPayment(amount, 'Purchase Item')
```

## Events

### Server Events
- `moneyUpdate`: Triggered when player money changes
- `transactionComplete`: Triggered after successful transaction

### Client Events
- `onMoneyChange`: Triggered when player's money updates
- `onTransactionFailed`: Triggered when a transaction fails 