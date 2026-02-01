---
title: Extension Features
description: Detailed feature guide for ClawFi extension
---

# Extension Features

## Signals Tab

The Signals tab shows risk alerts for the current token.

### Signal Types

| Type | Icon | Description |
|------|------|-------------|
| Honeypot | 🍯 | Token cannot be sold |
| Rug Pull Risk | ⚠️ | Multiple contract red flags |
| Whale Movement | 🐋 | Large holder activity |
| Liquidity Change | 💧 | Significant LP changes |
| Contract Risk | 📜 | Unverified, mintable, etc. |
| Holder Concentration | 👥 | Top holders control too much |

### Severity Levels

- 🔴 **Critical** - Avoid this token
- 🟠 **High** - Significant risk
- 🟡 **Medium** - Proceed with caution
- 🟢 **Low** - Minor concern
- ℹ️ **Info** - Informational

## Market Tab

Real-time market data from Dexscreener.

### Metrics Shown

- **Price** - Current USD price
- **24h Change** - Price change percentage
- **Volume** - 24h trading volume
- **Liquidity** - Available liquidity
- **Market Cap** - Total market capitalization
- **FDV** - Fully diluted valuation

### Transaction Activity

- Buy/Sell counts (5m, 1h, 6h, 24h)
- Buy/Sell ratio indicator

## Assist Tab

Quick actions and useful links.

### Available Actions

- 📋 **Copy Address** - Copy token contract
- 🔗 **Dexscreener** - Open on Dexscreener
- 🦄 **Uniswap** - Trade on Uniswap
- 🔍 **Explorer** - View on block explorer
- 🐦 **Twitter Search** - Search token on Twitter

### Safety Warning

The Assist tab shows a warning about verifying transactions:

> Always verify contract addresses before trading. ClawFi provides data but cannot guarantee safety.

## FAB (Floating Action Button)

The 🦀 button shows at-a-glance status:

- **Badge** - Number of active signals
- **Red dot** - Critical/high risk detected
- **Position** - Bottom-right, draggable

## Settings

Access via extension popup or options page:

- **API Key** - Optional premium access
- **Kill Switch** - Disable all overlays
- **Notifications** - Browser notifications

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Escape` | Close overlay panel |
| Click outside | Collapse to FAB |

## Supported Data Sources

- **Dexscreener** - Market data
- **GoPlus** - Security analysis
- **Block Explorers** - Contract verification
