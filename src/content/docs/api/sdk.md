---
title: SDK Reference
description: Complete SDK documentation
---

# SDK Reference

The `@clawfi/sdk` package provides a TypeScript client for ClawFi functionality.

## Installation

```bash
npm install @clawfi/sdk
```

## Quick Start

```typescript
import { ClawFi } from '@clawfi/sdk';

const clawfi = new ClawFi();

// Analyze a token
const analysis = await clawfi.analyzeToken('ethereum', '0x...');
console.log('Risk Score:', analysis.data?.riskScore);
```

## Configuration

```typescript
const clawfi = new ClawFi({
  apiKey: 'your-api-key',      // Optional
  baseUrl: 'https://...',       // Custom API URL
  timeout: 30000,               // Request timeout (ms)
});
```

## Methods

### Token Analysis

#### analyzeToken(chain, address)
Full token analysis with market data, signals, and contract info.

```typescript
const result = await clawfi.analyzeToken('base', '0x...');
if (result.success) {
  console.log(result.data.riskScore);
  console.log(result.data.signals);
}
```

#### getToken(chain, address)
Quick token info only.

```typescript
const token = await clawfi.getToken('ethereum', '0x...');
console.log(token.data?.symbol);
```

### Signals

#### getSignals(chain, address)
Get risk signals for a token.

```typescript
const signals = await clawfi.getSignals('bsc', '0x...');
signals.data?.forEach(s => console.log(s.title));
```

#### getRecentSignals(limit?)
Get recent signals across all tokens.

```typescript
const recent = await clawfi.getRecentSignals(100);
```

#### subscribeSignals(webhookUrl, filters?)
Subscribe to signal notifications.

```typescript
await clawfi.subscribeSignals('https://my-server/webhook', {
  chains: ['ethereum', 'base'],
  severity: ['high', 'critical'],
});
```

### Market Data

#### getMarketData(chain, address)
Get market data for a token.

```typescript
const market = await clawfi.getMarketData('ethereum', '0x...');
console.log('Price:', market.data?.price);
console.log('Volume:', market.data?.volume.h24);
```

#### getTrending(chain?)
Get trending tokens.

```typescript
const trending = await clawfi.getTrending('base');
```

### Security

#### getContractAnalysis(chain, address)
Get contract security analysis.

```typescript
const contract = await clawfi.getContractAnalysis('bsc', '0x...');
console.log('Verified:', contract.data?.verified);
console.log('Mintable:', contract.data?.mintable);
```

#### checkHoneypot(chain, address)
Quick honeypot check.

```typescript
const check = await clawfi.checkHoneypot('bsc', '0x...');
if (check.data?.isHoneypot) {
  console.log('WARNING: Honeypot detected!');
}
```

### Search

#### search(query)
Search for tokens.

```typescript
const results = await clawfi.search('PEPE');
results.data?.forEach(t => console.log(t.symbol, t.price));
```

### Watchlist

#### addToWatchlist(chain, address)
#### getWatchlist()
#### removeFromWatchlist(id)

```typescript
await clawfi.addToWatchlist('ethereum', '0x...');
const list = await clawfi.getWatchlist();
await clawfi.removeFromWatchlist('some-id');
```

## Types

```typescript
import type {
  ClawFiConfig,
  Signal,
  TokenData,
  MarketData,
  TokenAnalysis,
  ApiResponse,
  ChainId,
} from '@clawfi/sdk';
```

## Error Handling

All methods return `ApiResponse<T>`:

```typescript
interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: string;
  timestamp: number;
}
```

Usage:

```typescript
const result = await clawfi.analyzeToken('ethereum', '0x...');

if (!result.success) {
  console.error('Error:', result.error);
  return;
}

// Safe to use result.data
const { riskScore, signals } = result.data;
```

## Fallback Mode

The SDK automatically falls back to public APIs (Dexscreener, GoPlus) when:
- No API key is provided
- ClawFi API is unavailable

This ensures basic functionality always works.
