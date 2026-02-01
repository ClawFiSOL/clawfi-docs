---
title: clawfi-signals
description: Signal detection and risk analysis library
---

# @clawfi/signals

Signal detection and risk analysis library for crypto tokens.

## Installation

```bash
npm install @clawfi/signals
```

## Features

- 🐋 Whale movement detection
- 💧 Liquidity monitoring
- 🍯 Honeypot detection
- ⚠️ Rug pull risk assessment
- 📊 Risk scoring (0-100)

## Quick Start

```typescript
import { detect, getRiskSummary } from '@clawfi/signals';

const context = {
  metrics: {
    address: '0x...',
    chain: 'ethereum',
    price: 0.001,
    liquidityChange24h: -0.3,
    // ...
  },
  contract: {
    verified: true,
    mintable: true,
    // ...
  },
};

const result = detect(context);

console.log('Risk Score:', result.riskScore);
console.log('Signals:', result.signals.length);
```

## Built-in Detectors

| Detector | Description |
|----------|-------------|
| WhaleMovementDetector | Whale holder concentration |
| LiquidityChangeDetector | Liquidity drops |
| HoneypotDetector | Honeypot contracts |
| RugPullRiskDetector | Contract risks |
| VolumeSpikeDetector | Unusual volume |

## Custom Detectors

```typescript
import { Detector, Signal } from '@clawfi/signals';

class MyDetector implements Detector {
  name = 'My Detector';
  type = 'custom';
  
  detect(ctx: DetectionContext): Signal[] {
    // Your logic here
    return [];
  }
}
```

## Risk Scoring

```typescript
import { calculateRiskScore, getRiskLevel } from '@clawfi/signals';

const score = calculateRiskScore(signals);  // 0-100
const level = getRiskLevel(score);          // 'safe' | 'low' | 'medium' | 'high' | 'critical'
```

## Links

- [GitHub](https://github.com/ClawFiAI/clawfi-signals)
