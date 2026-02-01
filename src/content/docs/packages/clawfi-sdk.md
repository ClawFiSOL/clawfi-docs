---
title: clawfi-sdk
description: Official ClawFi TypeScript SDK
---

# @clawfi/sdk

Official TypeScript SDK for ClawFi crypto intelligence.

## Installation

```bash
npm install @clawfi/sdk
```

## Features

- 🔐 Token analysis with risk scoring
- 📡 Real-time signals
- 🛡️ Honeypot detection
- 📊 Market data
- 🔔 Webhook subscriptions
- ⚡ Works offline (Dexscreener + GoPlus fallback)

## Quick Start

```typescript
import { ClawFi } from '@clawfi/sdk';

const clawfi = new ClawFi();

// Full analysis
const analysis = await clawfi.analyzeToken('ethereum', '0x...');
console.log('Risk Score:', analysis.data?.riskScore);

// Quick honeypot check
const check = await clawfi.checkHoneypot('bsc', '0x...');
if (check.data?.isHoneypot) {
  console.log('DANGER: Honeypot detected!');
}
```

## Signal Utilities

```typescript
import { 
  calculateRiskScore,
  filterBySeverity,
  isHighRisk,
  formatSignal,
} from '@clawfi/sdk';

const score = calculateRiskScore(signals);
const critical = filterBySeverity(signals, 'critical');

if (isHighRisk(signals)) {
  console.log('⚠️ High risk token!');
}
```

## Market Utilities

```typescript
import {
  formatPrice,
  formatMarketCap,
  getMomentum,
  detectPumpPattern,
} from '@clawfi/sdk';

console.log(formatPrice(0.00001234));  // "$0.000012"
console.log(formatMarketCap(1500000)); // "$1.50M"
console.log(getMomentum(marketData));  // "bullish"
```

## Links

- [Full Documentation](/api/sdk/)
- [GitHub](https://github.com/ClawFiAI/clawfi-sdk)
