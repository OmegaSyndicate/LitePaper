# Impermanent loss

{% hint style="info" %}
**What is impermanent loss?** as the market value of the liquidity reserves held by the DEX changes, arbitrage swaps occur along the x\*y=k bonding curve to keep the spot prices on the exchange in balance with prices on the external market. As this happens the tokens held in reserve by the exchange slightly loose value as compared to the same portfolio held outside of the exchange.

The loss is called impermanent because if the _**relative price**_ between the tokens listed at the AMM returns to the same ratio as it was initially, these losses vanish completely. After one supplies liquidity to an AMM, the impermanent loss for that liquidity position moves up and down over time as the relative token prices change.
{% endhint %}

When supplying liquidity to DefiPlaza or any other AMM, there is impermanent loss (IL) to consider. When one supplies liquidity to an AMM, the impermanent loss for that liquidity position moves up and down over time as the relative token prices change. When the liquidity is withdrawn the impermanent loss is realised into an actual loss. What we need to understand is how IL is likely to develop over time for our liquidity providers.

Mathematically, it is possible to compute exactly how much the impermanent loss is as a function of the relative prices. If we take beta to be the price change for each token as compared to when the liquidity position was opened, one can work out the formula for generalised impermanent loss when N tokens are paired together (UniSwap N=2, DefiPlaza N=16) to the below:

![Impermanent loss generalised for N pooled tokens with beta price change per token](https://miro.medium.com/max/1400/1\*FtuO0piINxYwL3Arwld6FA.png)

Suppose we add $1000 in liquidity to DefiPlaza today. Then we will receive a certain amount of liquidity tokens XDP2 which represent our share in the reserves of all tokens held by the exchange. If we check back a month later, we might find that 2 tokens fell by 20% (beta=0.8), 4 tokens stayed the same price (beta=1), 8 tokens went +20% (beta=1.2) and 2 tokens went +50% (beta=1.5) in price. Then if we withdraw the liquidity tokens we initially received for our $1000 investment from DefiPlaza, we now would receive tokens worth ±$1120.70 on the external market.

However, someone who held the same $1000 split over the same 16 tokens without providing them as liquidity would now have $1137.50 worth of tokens. The Impermanent Loss is the relative difference between these two amounts. It can be calculated with the formula above for arbitrary pool sizes and token price changes. For the example numbers above the resulting impermanent loss is ±1.48%.

![Impermanent loss example calculation](https://miro.medium.com/max/1400/1\*TRSt5eaCmbzJee-XgTvOYg.png)

The impermanent loss is zero if all betas are the same. Thus, if all tokens move up and down at the same rate, no impermanent loss will occur at all. If part of the tokens increase significantly in price while others fall in price the impermanent loss will be large. The more correlation there is in price movement between the listed tokens, the smaller will be the impermanent loss.

Crypto markets have historically shown a high degree of correlation between token prices. With a larger basket of tokens, the risk of IL is effectively spread over the whole basket. If one token multiplies by 10x on price relative to the others, the IL will be less in a pool with 16 tokens than a pool with 2 tokens. If most of the tokens have similar price action, impermanent loss remains relatively small.
