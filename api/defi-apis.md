# DeFi API Reference

ClawFi integrates with multiple DeFi data providers to deliver comprehensive token analysis. This reference documents the external APIs available through ClawFi and how to use them directly.

## Overview

ClawFi aggregates data from 10+ DeFi platforms:

| Provider | Chains | Auth Required | Use Case |
|----------|--------|---------------|----------|
| DexScreener | 80+ | No | Price, volume, liquidity |
| GeckoTerminal | 200+ | No | Pool data, OHLCV |
| Jupiter | Solana | Optional | Swap quotes |
| Birdeye | Solana | Yes | Token analytics |
| Dextools | 80+ | Yes | DEXTScore, analytics |

---

## DexScreener API

Free public API for DEX pair data across 80+ chains.

### Base URL
```
https://api.dexscreener.com
```

### Rate Limits
- Token profiles, boosts: 60 req/min
- Pairs, search, tokens: 300 req/min

### Endpoints

#### Search Pairs
```bash
curl "https://api.dexscreener.com/latest/dex/search?q=PEPE"
```

#### Get Token Data
```bash
curl "https://api.dexscreener.com/tokens/v1/ethereum/0x6982508145454Ce325dDbE47a25d4ec3d2311933"
```

#### Get Pair by Address
```bash
curl "https://api.dexscreener.com/latest/dex/pairs/ethereum/0xA43fe16908251ee70EF74718545e4FE6C5cCEc9f"
```

#### Get Token Pools
```bash
curl "https://api.dexscreener.com/token-pairs/v1/solana/JUPyiwrYJFskUPiHa7hkeR8VUtAeFoSYbKedZNsDvCN"
```

### Response Example
```json
{
  "pairs": [{
    "chainId": "ethereum",
    "dexId": "uniswap",
    "pairAddress": "0xA43fe16908251ee70EF74718545e4FE6C5cCEc9f",
    "baseToken": {
      "address": "0x6982508145454Ce325dDbE47a25d4ec3d2311933",
      "name": "Pepe",
      "symbol": "PEPE"
    },
    "priceUsd": "0.00001234",
    "volume": { "h24": 125000000 },
    "liquidity": { "usd": 45000000 },
    "priceChange": { "h24": 15.5 },
    "txns": {
      "h24": { "buys": 12500, "sells": 11200 }
    }
  }]
}
```

---

## GeckoTerminal API

Free API from CoinGecko for DEX data across 200+ networks.

### Base URL
```
https://api.geckoterminal.com/api/v2
```

### Rate Limits
- Public: 10-30 calls/minute

### Endpoints

#### Get Trending Pools
```bash
curl "https://api.geckoterminal.com/api/v2/networks/trending_pools"
```

#### Get Pool Data
```bash
curl "https://api.geckoterminal.com/api/v2/networks/eth/pools/0x88e6a0c2ddd26feeb64f039a2c41296fcb3f5640"
```

#### Get Token Price
```bash
curl "https://api.geckoterminal.com/api/v2/simple/networks/eth/token_price/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2"
```

#### Get OHLCV Data
```bash
curl "https://api.geckoterminal.com/api/v2/networks/eth/pools/0x88e6a0c2ddd26feeb64f039a2c41296fcb3f5640/ohlcv/day"
```

#### Search Pools
```bash
curl "https://api.geckoterminal.com/api/v2/search/pools?query=PEPE"
```

#### Get New Pools
```bash
curl "https://api.geckoterminal.com/api/v2/networks/base/new_pools"
```

### Network IDs
`eth`, `bsc`, `polygon_pos`, `arbitrum`, `optimism`, `base`, `solana`, `avalanche`

---

## Jupiter API (Solana)

Leading Solana DEX aggregator for swap quotes and execution.

### Base URL
```
https://api.jup.ag
```

### Rate Limits
- Free: 60 req/min
- Pro: 600-3000 req/min

### Authentication (Optional)
```
Header: x-api-key: YOUR_API_KEY
```

### Endpoints

#### Get Swap Quote
```bash
curl "https://api.jup.ag/swap/v1/quote?inputMint=So11111111111111111111111111111111111111112&outputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v&amount=1000000000&slippageBps=50"
```

#### Get Token Price
```bash
curl "https://api.jup.ag/price/v2?ids=So11111111111111111111111111111111111111112"
```

#### Build Swap Transaction
```bash
curl -X POST "https://api.jup.ag/swap/v1/swap" \
  -H "Content-Type: application/json" \
  -d '{
    "quoteResponse": { ... },
    "userPublicKey": "YOUR_WALLET_ADDRESS"
  }'
```

### Quote Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `inputMint` | Yes | Input token mint |
| `outputMint` | Yes | Output token mint |
| `amount` | Yes | Amount in smallest units |
| `slippageBps` | No | Slippage in basis points |
| `onlyDirectRoutes` | No | Skip multi-hop |

### Response Example
```json
{
  "inputMint": "So11111111111111111111111111111111111111112",
  "outputMint": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
  "inAmount": "1000000000",
  "outAmount": "149500000",
  "priceImpactPct": "0.001",
  "routePlan": [{
    "swapInfo": {
      "label": "Raydium",
      "inAmount": "1000000000",
      "outAmount": "149500000"
    },
    "percent": 100
  }]
}
```

---

## Birdeye API (Solana)

Comprehensive Solana DeFi data with real-time prices and analytics.

### Base URL
```
https://public-api.birdeye.so
```

### Authentication (Required)
```
Headers:
  X-API-KEY: your-api-key
  x-chain: solana
```

### Rate Limits

| Plan | Rate | Price |
|------|------|-------|
| Free | 1 rps | $0 |
| Starter | 15 rps | $99/mo |
| Premium | 50 rps | $199/mo |

### Endpoints

#### Get Token Price
```bash
curl -H "X-API-KEY: YOUR_KEY" -H "x-chain: solana" \
  "https://public-api.birdeye.so/defi/price?address=So11111111111111111111111111111111111111112"
```

#### Get Token Overview
```bash
curl -H "X-API-KEY: YOUR_KEY" -H "x-chain: solana" \
  "https://public-api.birdeye.so/defi/token_overview?address=JUPyiwrYJFskUPiHa7hkeR8VUtAeFoSYbKedZNsDvCN"
```

#### Get Trending Tokens
```bash
curl -H "X-API-KEY: YOUR_KEY" -H "x-chain: solana" \
  "https://public-api.birdeye.so/defi/token_trending"
```

#### Get OHLCV
```bash
curl -H "X-API-KEY: YOUR_KEY" -H "x-chain: solana" \
  "https://public-api.birdeye.so/defi/ohlcv?address=YOUR_TOKEN&type=15m"
```

### Response Example
```json
{
  "success": true,
  "data": {
    "address": "JUPyiwrYJFskUPiHa7hkeR8VUtAeFoSYbKedZNsDvCN",
    "symbol": "JUP",
    "price": 1.25,
    "priceChange24hPercent": -2.5,
    "liquidity": 50000000,
    "mc": 1500000000,
    "v24hUSD": 25000000,
    "holder": 150000
  }
}
```

---

## Clanker API (Base)

API for AI-driven token deployment on Base via Farcaster.

### Base URL
```
https://api.clanker.world
```

### Endpoints

#### Get Tokens
```bash
curl "https://api.clanker.world/tokens"
```

#### Get Tokens by Creator
```bash
curl "https://api.clanker.world/tokens/creator/0x..."
```

### Token Info
- ERC-20 on Uniswap V3
- 1B total supply per token
- Liquidity permanently locked
- Creators earn 0.4% trading fees

---

## DEX Aggregators

### 1inch API

```bash
# Get swap quote (Ethereum)
curl "https://api.1inch.io/v5.2/1/quote?fromTokenAddress=0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE&toTokenAddress=0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48&amount=1000000000000000000"
```

### 0x API

```bash
# Get swap price
curl -H "0x-api-key: YOUR_KEY" \
  "https://api.0x.org/swap/v2/price?chainId=1&sellToken=ETH&buyToken=USDC&sellAmount=1000000000000000000&taker=YOUR_WALLET"
```

---

## Using with ClawFi

ClawFi proxies these APIs through a unified interface:

### Via ClawFi API
```bash
# Get market data (aggregated from DexScreener + GeckoTerminal)
curl "https://api.clawfi.ai/api/v1/market/ethereum/0x6982508145454Ce325dDbE47a25d4ec3d2311933"
```

### Via ClawFi SDK
```typescript
import { ClawFi } from '@clawfi/sdk';

const clawfi = new ClawFi();

// Automatically fetches from best available source
const market = await clawfi.getMarketData('ethereum', '0x...');
const safety = await clawfi.checkHoneypot('bsc', '0x...');
const quote = await clawfi.getSwapQuote('solana', 'SOL', 'USDC', 1);
```

### Via Extension
The ClawFi extension automatically queries these APIs when you visit supported sites:
- Dexscreener
- GeckoTerminal
- Jupiter
- Pump.fun
- Clanker
- And more...

---

## Best Practices

### Rate Limiting
```javascript
async function fetchWithRetry(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    const response = await fetch(url);
    if (response.status === 429) {
      await new Promise(r => setTimeout(r, Math.pow(2, i) * 1000));
      continue;
    }
    return response;
  }
  throw new Error('Rate limited');
}
```

### Caching
```javascript
const cache = new Map();
const CACHE_TTL = 30000; // 30 seconds

async function getCachedData(key, fetcher) {
  const cached = cache.get(key);
  if (cached && Date.now() - cached.time < CACHE_TTL) {
    return cached.data;
  }
  const data = await fetcher();
  cache.set(key, { data, time: Date.now() });
  return data;
}
```

### Error Handling
```javascript
try {
  const data = await fetch(url);
  if (!data.ok) {
    if (data.status === 404) return null;
    if (data.status === 429) throw new Error('Rate limited');
    throw new Error(`API error: ${data.status}`);
  }
  return data.json();
} catch (error) {
  console.error('API request failed:', error);
  return null;
}
```

---

## Quick Reference

| API | Free Tier | Best For |
|-----|-----------|----------|
| DexScreener | 300/min | Price, volume, pairs |
| GeckoTerminal | 30/min | Pools, OHLCV |
| Jupiter | 60/min | Solana swaps |
| Birdeye | 1 rps | Solana analytics |
| 1inch | Unlimited | EVM swaps |
| 0x | With key | EVM aggregation |

---

*Last updated: February 2026*
