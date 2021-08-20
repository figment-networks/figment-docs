---
description: Learn how Osmosis works and what makes it special
---

# ✏ Osmosis 101

## **What is Osmosis?**

Osmosis is an advanced AMM protocol built using the Cosmos SDK that will allow developers to design, build, and deploy their own customized AMMs.

Heterogeneity and sovereignty are two core tenets of the Cosmos ecosystem, and Osmosis takes these two values and extends them into core characteristics of this AMM protocol. Rather than aim for a one-size-fits-all homogeneous approach for AMMs and its liquidity pools, Osmosis is designed such that the most efficient solution is reachable through the process of experimentation and rapid iteration by leveraging the wisdom of the crowd. It achieves this by offering deep customizability to AMM designers, and a governance mechanism by which each AMM pool’s stakeholders \(i.e. liquidity providers\) can govern and direct their pools. ****_Source -_ ****[Osmosis Medium](https://medium.com/osmosis/vision-for-osmosis-e68e796ff1c2)

### **Why Osmosis?**

#### On customizability of liquidity pools

Most major AMMs limit the changeable parameters of liquidity pools. For example, Uniswap only allows the creation of a two-token pool of equal ratio with the swap fee of 0.3%. The simplicity of Uniswap protocol allowed quick onboarding of the average user that previously had little to no experience in market making.

However, as the DeFi market size grows and market participants such as arbitrageurs and liquidity providers mature, the need for liquidity pools to react to market conditions becomes apparent. The optimal swap fee for a AMM trade may depend on various factors such as block times, slippage, transaction fee, market volatility and more. There is no one-size-fits-all solution as the mix of characteristics of blockchain protocol, tokens in the liquidity pool, market conditions, and others can change the optimal strategy for the liquidity providers and the market makers to carry out.

The tools Osmosis provides allow market participants to self-identify opportunities and allow them to react by adjusting the various parameters. An optimal equilibrium between fee and liquidity can be reached through autonomous experiments and iterations, rather than setting a centrally planned 'most acceptable compromise' value. This extends the addressable market for AMMs and bonding curves beyond simple token swaps, as a limitation on the customizability of liquidity pools may have been the inhibiting factor for more experimental use-cases of AMMs.

#### Self-governing liquidity pools

As important as the ability to change the parameters of a liquidity pool is, the feature would mean very little without a method to coordinate a decision amongst the stakeholders. The Osmosis' pool governance feature allows a diverse spectrum of liquidity pools with risk tolerance and strategies to not only exist, but evolve.

On Osmosis, the liquidity pool shares are not only used to calculate the fractional ownership of a liquidity pool, but also the right to participate in the strategic decision making of the liquidity pool as well. To incentivize long-term liquidity commitment, shares must be locked up for an extended period. Longer term commitments are awarded by additional voting power / additional liquidity mining revenue. The long-term liquidity commitment by the liquidity providers prevent the impact of potential vampire attacks, where ownership of the shares are delegated and potentially used to migrate liquidity to an external AMM. This provides equity of power amongst liquidity providers, where those with greater skin-in-the-game are given their rightful power to steer the strategic direction of its pool in proportion to the risk they are taking with their assets.

As AMMs mostly guarantee a level of constant total value output, those who may disagree with the changes made to the pool are able to withdraw their funds with little to no loss of their principals. As Osmosis expects the market to self-discover the optimal value of each adjustable parameter, if a significant dissenting opinion exists–they are able to start a competing liquidity pool with their own strategy.

#### AMM as serviced infrastructure

The number and complexity of decentralized financial products are consistently increasing. Instruments such as pegged assets, derivatives, options, and tokenized leveraged positions each have their own characteristics that produce optimal market efficiency when paired with the correct bonding curve. That being said, the traditional notion of AMMs has evolved around putting the AMM first, and the financial product being traded second.

As AMMs substantially increase the market accessibility for these instruments, assets with diverse characteristics either had to:

1. Compromise efficiency and trade on existing AMMs with non-optimal bonding curves or
2. Take on the massive task of building one's own AMM that is able to maximize efficiency

To solve this issue, Osmosis introduces the idea of an 'AMM as a serviced infrastructure'. Fairly often, adjustment of the value function and a few additional parameters are all that's needed to provide a highly-efficient, highly-accessible AMM for the majority of decentralized financial instruments. By providing the ability for the creator of the pool to simply define the bonding curve value function and reuse the majority of the key AMM infrastructure, the barrier to creating a tailor-made and efficient automated market maker can be reduced. ****_Source -_ [Osmosis Github](https://github.com/osmosis-labs/osmosis)

## **Network Specifications**

### **Role of the OSMO token**

The OSMO token is a decentralized governance token that enables users to vote on protocol upgrades, allocate liquidity mining rewards for liquidity pools, and set the base network swap fee. The OSMO token will be supported on the Keplr wallet. 

The Osmosis Team is currently working on a system called “reverse staking derivatives” which will enable liquidity pools of OSMO pools to stake \(and also vote with\) their liquidity pool shares. With this being a new concept, the main consideration is properly assessing how the risk should be measured and bound to the chain itself. For example, if an LP holds 10 OSMO, and stakes 9 OSMO, there is a 10% risk-discount for volatility within a given epoch.



