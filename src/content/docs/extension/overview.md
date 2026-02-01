---
title: Extension Overview
description: ClawFi browser extension capabilities
---

# Extension Overview

ClawFi Extension provides real-time crypto intelligence directly on the DeFi sites you use.

## Capabilities

### Injected UI Overlay
Non-intrusive floating interface that appears on supported sites without disrupting the page.

### Content Script UI Injection
Uses Shadow DOM for style isolation - no conflicts with the host page.

### DOM Overlay Toolbar/Panel
Expandable panel with tabs for different views:
- **Signals** - Risk alerts and notifications
- **Market** - Price, volume, liquidity data
- **Assist** - Quick actions and links

### Augmented Page UI
Enhances existing pages with additional context and data.

### Client-side Page Augmentation
All processing happens locally in your browser. No data sent to third parties.

## How It Works

```
1. You visit a supported site (e.g., dexscreener.com)
2. Extension detects token addresses on the page
3. Fetches market data and security info
4. Displays the floating ClawFi button (🦀)
5. Click to expand and view signals
```

## Architecture

```
┌─────────────────────────────────────────────┐
│                  Content Script              │
│  ┌─────────────────────────────────────┐    │
│  │           Shadow DOM Host           │    │
│  │  ┌─────────────────────────────┐    │    │
│  │  │     ClawFi Overlay (React)  │    │    │
│  │  │  ┌────┐ ┌────┐ ┌────┐       │    │    │
│  │  │  │FAB │ │Panel│ │Toast│     │    │    │
│  │  │  └────┘ └────┘ └────┘       │    │    │
│  │  └─────────────────────────────┘    │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
         ↓ Messages ↓
┌─────────────────────────────────────────────┐
│            Background Service Worker         │
│  - API Communication                         │
│  - Settings Storage                          │
│  - Cross-tab coordination                    │
└─────────────────────────────────────────────┘
```

## Data Flow

1. **Detection**: Content script extracts token addresses from page
2. **Lookup**: Background worker fetches data from APIs
3. **Analysis**: Signals library processes data for risks
4. **Display**: Overlay renders results in Shadow DOM

## Privacy

- ✅ Local processing only
- ✅ No tracking or analytics
- ✅ No data collection
- ✅ Open source
- ✅ No third-party scripts injected

## Permissions

The extension requests minimal permissions:

| Permission | Purpose |
|------------|---------|
| `storage` | Save your settings |
| `activeTab` | Access current tab's URL |
| Host permissions | Inject content scripts on supported sites |
