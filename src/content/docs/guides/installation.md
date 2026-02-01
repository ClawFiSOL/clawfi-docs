---
title: Installation
description: How to install ClawFi components
---

# Installation Guide

ClawFi consists of multiple components. Install what you need:

## Browser Extension

### Chrome Web Store
*(Coming Soon)*

### Manual Installation

1. Download the latest release:
   ```bash
   git clone https://github.com/ClawFiAI/clawfi-extension.git
   cd clawfi-extension
   npm install
   npm run build
   ```

2. Load in Chrome:
   - Go to `chrome://extensions`
   - Enable "Developer mode"
   - Click "Load unpacked"
   - Select the `dist` folder

## SDK / Libraries

### @clawfi/sdk

```bash
npm install @clawfi/sdk
# or
yarn add @clawfi/sdk
# or
pnpm add @clawfi/sdk
```

### dexscreener-ts

```bash
npm install dexscreener-ts
```

### @clawfi/signals

```bash
npm install @clawfi/signals
```

### chain-utils

```bash
npm install chain-utils
```

### defi-hooks (React)

```bash
npm install defi-hooks
```

## CLI Tools

### token-scanner

```bash
npm install -g token-scanner

# Or use npx
npx token-scanner scan 0x...
```

## Self-Hosted Services

### rugcheck-api

```bash
git clone https://github.com/ClawFiAI/rugcheck-api.git
cd rugcheck-api
npm install
npm run build
npm start
```

Docker:
```bash
docker build -t rugcheck-api .
docker run -p 3001:3001 rugcheck-api
```

## Requirements

- **Extension**: Chrome/Brave/Edge (Manifest V3 compatible)
- **SDK/Libraries**: Node.js 18+, TypeScript 5+
- **CLI**: Node.js 18+

## Next Steps

- [Quick Start Guide](/guides/quickstart/)
- [Extension Features](/extension/features/)
- [SDK Documentation](/api/sdk/)
