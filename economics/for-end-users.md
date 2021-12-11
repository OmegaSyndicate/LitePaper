# For end users

{% hint style="info" %}
**Good to know:** depending on the product you're building, it can be useful to explicitly document use cases. Got a product that can be used by a bunch of people in different ways? Maybe consider splitting it out!
{% endhint %}

The way that DefiPlaza can achieve significantly lower costs is by using a different economic model. Rather than having trading pairs like in UniSwap (2 tokens per pair), DefiPlaza uses a multi-token pool with 16 of the highest volume tokens in the DeFi space. By doing all this in a single smart contract and highly optimizing for gas consumption, the costs of a swap transaction to the end-user can be significantly reduced.

Effectively, we’re trying to do for DeFi what the low cost brokers did for the stock market: tremendously bring down the barrier for entry and the costs to the end-user. The idea is to leverage a superior economic model to the pair based exchanges that currently dominate the DeFi space. In this post we’ll dive a little deeper into DEX transaction economics when viewed from the end-user side. In the next article we’ll explore the economics from the liquidity provider side of things.

### Total end-user cost of a DEX transaction <a href="#e925" id="e925"></a>

If we look closely at any DEX transaction, we find that the total cost of a swap to the consumer can be broken down into three components:

1. **Gas fees**. This is the most visible cost, as it is explicitly shown for each transaction. A swap between two ERC20 tokens which are directly pooled together in UniSwap usually costs in the order of 100.000–150.000 gas. This amount is independent of the amount swapped, and is thus disproportionally effecting users who are swapping relatively small amounts. Since the Ethereum network is congested this issue is not expected to go away anytime soon. Ethereum 2.0 will not solve it either, since that breaks composability and thus is not suitable for DeFi.
2. **Exchange fees**. Every exchange uses their own fee model. The benchmark fee as set by UniSwap is 0.3% of the amount exchanged for pairs of dissimilar tokens. This fee directly goes into the pool and thus into the pockets of the liquidity providers. To make a swapping pair between two tokens economically attractive for the LPs, a 0.3% is roughly what’s required to get an appropriately balanced risk/reward ratio for dissimilar tokens.
3. **Bonding curve slippage**. The spot price on a UniSwap pair is given by the ratio of the tokens held in reserve. When a trade is executed, the pair moves along the invariant curve x\*y=k. Therefore, the price is changing as trades happen and the actual price paid for tokens in a swap will always be slightly worse than the spot price, which results in an additional cost to the user. Slippage is small for small trades but increases rapidly when the size of the trade grows relative to the liquidity in the pool.

As an example cost breakdown, let’s consider the UniSwap V2 pool for USDC/ETH, which contains roughly $240m in total liquidity as I’m writing this. Since DefiPlaza only launched last week, it doesn’t have the same liquidity yet. For an apples to apples comparison, let’s consider what would happen if DefiPlaza would contain the same $240m in total liquidity ($15m for each of the 16 tokens). For a swap of $10k in USDC to ETH, we would get the following cost breakdown (assuming gas at 100 GWei and ETH at $3500 as we have today).

![](https://miro.medium.com/max/1400/1\*TZybHjqAuS7C3DFRcyA80w.png)

We can observe that the total cost to the user for a DefiPlaza transaction is lower than just the gas costs for a UniSwap transaction. That means that DefiPlaza will be cheaper, regardless of what fees/slippage are used on UniSwap! For the $240m total liquidity example, a trade of 10k$ USDC to ETH would be \~45% cheaper than the same trade on UniSwapV2 is today.The above cost breakdown is just for the USDC/ETH pair on DefiPlaza, but with in DefiPlaza the same $240m liquidity is split over 16 tokens, allowing **119** other pairs to trade on top of the USDC/ETH pair, all at the similar low total transaction costs. The multi-token pool model is vastly more economical than the pair-based model, especially in congested networks like Ethereum.Reference transactions for gas costs:\
1\. [DefiPlaza USDC to ETH](https://etherscan.io/tx/0xc3cdbfc58b1e57b4e8eed7be70dff9c1f11e9e35f4883e58830558a4d50f9603), spending all USDC (59,844 gas)\
2\. [UniSwapV2 USDC to ETH](https://etherscan.io/tx/0x2ddf1cd9585a6af36e19111e4161f4dad4ce1cc0a865fd20a1bbf432b51fe338), spending all USDC (118,150 gas)

### Non-direct pairing swaps

The comparison for USDC to ETH transaction above focused on a type of transaction that UniSwap specialises in: swaps between two tokens that are directly paired together in a liquidity pool. As shown above, even under those conditions Defi Plaza comfortably offers the better value proposition at the same level of liquidity.

However, if a transaction involves two tokens which are not paired directly, the UniSwap router will automatically create a transaction which makes multiple hops. These additional hops introduce additional trading fees and additional gas costs. A 2-hop transaction will cost around 170k gas (±60$) on UniSwap v2 and around 250k gas (±87.5$) on UniSwap v3 in pure gas consumption.

In contrast, DefiPlaza doesn’t need hops for any of the 120 trading pairs, so it will result in the same low gas costs for all pairs. Swapping two ERC20 tokens costs around 77k gas (±26.5$) for most tokens, with swaps against ETH costing even less!\
