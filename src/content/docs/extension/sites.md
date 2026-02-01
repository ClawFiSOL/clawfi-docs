---
title: Supported Sites
description: Sites where ClawFi extension works
---

# Supported Sites

ClawFi extension automatically activates on these sites.

## Full Support

Sites with complete overlay functionality:

| Site | Chain | URL |
|------|-------|-----|
| **Dexscreener** | Multi-chain | dexscreener.com |
| **Clanker** | Base | clanker.world |
| **Pump.fun** | Solana | pump.fun |
| **Four.meme** | BSC | four.meme |

## Partial Support

Sites with basic token detection:

| Site | Chain | URL |
|------|-------|-----|
| **Etherscan** | Ethereum | etherscan.io |
| **Basescan** | Base | basescan.org |
| **Arbiscan** | Arbitrum | arbiscan.io |
| **BSCScan** | BSC | bscscan.com |
| **Polygonscan** | Polygon | polygonscan.com |
| **Solscan** | Solana | solscan.io |
| **Uniswap** | Multi-chain | app.uniswap.org |

## Chain Coverage

### EVM Chains
- Ethereum
- Base
- BSC (BNB Chain)
- Arbitrum
- Polygon
- Optimism
- Avalanche
- Fantom

### Non-EVM
- Solana

## Adding New Sites

Want support for another site? 

1. Open an issue on [GitHub](https://github.com/ClawFiAI/clawfi/issues)
2. Include the site URL and what chain it supports
3. We'll evaluate and potentially add it

## Site Detection

The extension uses URL patterns to activate:

```javascript
// Dexscreener - extracts chain and token from URL
// e.g., dexscreener.com/ethereum/0x...
const match = url.match(/dexscreener\.com\/(\w+)\/([a-zA-Z0-9]+)/);

// Clanker - extracts token address
// e.g., clanker.world/clanker/0x...
const match = url.match(/clanker\.world\/clanker\/(0x[a-fA-F0-9]{40})/);
```

## Troubleshooting

### Overlay Not Appearing

1. Ensure you're on a supported site
2. Navigate to a specific token page
3. Check extension is enabled in popup
4. Verify "Kill Switch" is off
5. Try refreshing the page

### Wrong Chain Detected

The extension detects chain from the URL. If incorrect:
- Check you're on the right chain's page
- Some sites require explicit chain selection
