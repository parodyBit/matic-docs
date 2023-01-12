---
id: witnet
title: Witnet
sidebar_label: Witnet
description: "Multichain Decentralized Oracle"
keywords:
  - docs
  - matic
  - witnet
  - oracle
image: https://matic.network/banners/matic-network-16x9.png 
---
import useBaseUrl from '@docusaurus/useBaseUrl';

The Witnet multichain decentralized oracle enables smart contracts to realize their true potential by giving them access to all sorts of valuable data sets, and by attesting and delivering that information securely thanks to its strong cryptoeconomic guarantees.

Witnet can power most DeFi primitives like price feeds, stablecoins, synthetics, etc., as well as acting as a reliable source of randomness for creating uniqueness in NFTs.

### Feeds supported
A complete list of publicly available Witnet data feeds on Polygon can be found in the Witnet Data Feeds website: [https://feeds.witnet.io/polygon](https://feeds.witnet.io/polygon)

[Request a new price feed on Polygon](https://tally.so/r/wMZDAn) or [Create your own data feed](https://docs.witnet.io/smart-contracts/witnet-web-oracle/make-a-get-request).

### How To Use Witnet Price Feeds

Witnet price feeds can be integrated into your own Polygon Mainnet contracts in two different ways:

1. [Integrate through proxy](https://docs.witnet.io/smart-contracts/witnet-data-feeds/using-witnet-data-feeds#reading-multiple-currency-pairs-from-the-router) Recommended for testing and upgradability.
   This is the preferred way to consume the Witnet-powered price feeds. Through using the ***Price Feeds Router***.  

2. [Integrate directly](https://docs.witnet.io/smart-contracts/witnet-data-feeds/using-witnet-data-feeds#reading-last-price-and-timestamp-from-a-price-feed-contract-serving-a-specific-pair) Optimized for gas cost and decentralization

The ***WitnetPriceRouter*** smart contract is deployed in all the [supported chains](https://docs.witnet.io/smart-contracts/witnet-data-feeds/addresses) and allows your own smart contracts and Web3 applications to get the latest price of any of the [supported currency pairs](https://docs.witnet.io/smart-contracts/witnet-data-feeds/price-feeds-registry#currency-pairs) by providing the identifier of the pair to a single Solidity method. This removes the need to know the actual contract addresses handling the price updates from the Witnet oracle.

### Reading multiple price pairs from the router

**WitnetPriceRouter**

*Mainnet*: [0x3806311c7138ddF2bAF2C2093ff3633E5A73AbD4](https://polygonscan.com/address/0x3806311c7138ddF2bAF2C2093ff3633E5A73AbD4#readContract)

*Mumbai*: [0x6d5544ca5b35bf2e7a78ace4E7B8d191fe5C9FAb](https://mumbai.polygonscan.com/address/0x6d5544ca5b35bf2e7a78ace4E7B8d191fe5C9FAb#readContract)

The Price Router contract is the easiest and most convenient way to consume Witnet price feeds on any of the [supported chains](https://docs.witnet.io/smart-contracts/supported-chains).

#### Solidity example

The example below shows how to read the price of two different assets from the Witnet Price Router:

```javascript
 // SPDX-License-Identifier: MIT
pragma solidity ^0.8.11;

import "witnet-solidity-bridge/contracts/interfaces/IWitnetPriceRouter.sol";

contract MyContract {
    IWitnetPriceRouter immutable public router;

    /**
     * IMPORTANT: pass the WitnetPriceRouter address depending on 
     * the network you are using! Please find available addresses here:
     * https://docs.witnet.io/smart-contracts/price-feeds/contract-addresses
     */
    constructor(IWitnetPriceRouter _router))
        router = _router;
    }

    /// Returns the BTC / USD price (6 decimals), ultimately provided by the Witnet oracle.
    function getBtcUsdPrice() public view returns (int256 _price) {
        (_price,,) = router.valueFor(bytes4(0x24beead4));
    }

    /// Returns the ETH / USD price (6 decimals), ultimately provided by the Witnet oracle.
    function getEthUsdPrice() public view returns (int256 _price) {
        (_price,,) = router.valueFor(bytes4(0x3d15f701));
    }

    /// Returns the BTC / ETH price (6 decimals), derived from the ETH/USD and 
    /// the BTC/USD pairs that were ultimately provided by the Witnet oracle.
    function getBtcEthPrice() public view returns (int256 _price) {
        return (1000000 * getBtcUsdPrice()) / getEthUsdPrice();
    }
}
```

For more information about Witnet please refer to: 

[website](https://witnet.io/) | [docs](https://docs.witnet.io/) | [github](https://github.com/witnet) | [twitter](https://twitter.com/witnet_io) | [telegram](https://t.me/witnetio) | [discord](https://discord.gg/witnet) 
