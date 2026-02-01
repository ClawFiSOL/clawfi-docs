---
title: dexscreener-ts
description: TypeScript wrapper for Dexscreener API
---

# dexscreener-ts

TypeScript wrapper for the [Dexscreener API](https://docs.dexscreener.com/) with full type safety.

## Installation

```bash
npm install dexscreener-ts
```

## Quick Start

```typescript
import { Dexscreener } from 'dexscreener-ts';

const dex = new Dexscreener();

// Get token data
const { pairs } = await dex.getTokenPairs('ethereum', '0x...');
console.log('Price:', pairs[0].priceUsd);

// Search tokens
const results = await dex.search('PEPE');

// Get trending
const trending = await dex.getTrending();
```

## API

### Constructor

```typescript
const dex = new Dexscreener({
  baseUrl: 'https://api.dexscreener.com',
  timeout: 10000,
  retries: 3,
  retryDelay: 1000,
});
```

### Methods

#### Token Profiles
```typescript
const profiles = await dex.getLatestProfiles();
```

#### Boosts/Trending
```typescript
const latest = await dex.getLatestBoosts();
const top = await dex.getTopBoosts();
const trending = await dex.getTrending(); // alias
```

#### Pairs & Tokens
```typescript
const { pairs } = await dex.getPair('ethereum', '0xPairAddress');
const { pairs } = await dex.getTokenPairs('base', '0xTokenAddress');
const { pairs } = await dex.getTokens('bsc', ['0x...', '0x...']);
```

#### Search
```typescript
const results = await dex.search('DOGE');
```

#### Convenience Methods
```typescript
const price = await dex.getTokenPrice('ethereum', '0x...');
const mcap = await dex.getTokenMarketCap('ethereum', '0x...');
const volume = await dex.getTokenVolume('ethereum', '0x...');
```

## Types

All types are exported:

```typescript
import type {
  Pair,
  Token,
  TokenProfile,
  TokenBoost,
  Volume,
  Liquidity,
  PriceChange,
  ChainId,
} from 'dexscreener-ts';
```

## Links

- [GitHub](https://github.com/ClawFiAI/dexscreener-ts)
- [npm](https://www.npmjs.com/package/dexscreener-ts)
- [Dexscreener API Docs](https://docs.dexscreener.com/)
