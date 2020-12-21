In Cutcoin, we have quite a lot of questions about PoS consensus and resistance to 51% attacks. This may be related to the fact that PoS coins are the next generation of cryptocurrency (first were PoW) and often have more complicated machinery. Let's dive into details.

### Attack Planning

Many different types of fraud are hidden behind the name '51% attack', this is due to the fact that reaching the control over 51% of resources required to establish the consensus gives a wide range of possible manipulations with the blockchain. We would like to emphasise that, anyway, such types of attacks do not go unnoticed, it's basically related to their scale and also their nature: the affected persons are finally specific legal entities or individuals, not the system itself. This means that an attack should be planned in advance and implemented in the short term.

### Compare Scenarios and Initial Investments Required to Attack PoW and PoS Coins.

We need to compare scenarios and required resources to perform the attack on both types of the systems: PoW and PoS. Consider a coin with the smaller or medium capitalization. All data are taken on 12/15/2020.

If it is a PoW coin one needs to have the computational resources that cover ~50% of the typical hashrate. Look at Zcash, #36 in CMC rank with 37543BTC capitalization [1]. It has ~8.5MSol/s hashrate. Nicehash offers ~0.5Msol for approx. 0.5490BTC/MSol/day. We can use this data as a reference point to estimate the required financial investments to rent the mining facilities that allow to attack. The summary cost is approximately 4.7BTC per day. If an attacker prefers to buy the hardware instead it's also possible as it has good liquidity and its price has no correlation with the price of a specific coin.

Now let's take a look at Cutcoin. It has ~360BTC capitalization [3], ~80% of the coins, on average, are staking. An attacker needs to buy approximately 40% of the circulating supply on the market, and this activity may lead to significant price growth. In reality, it takes significant time to enlarge someone's share if use buying on the market. The circulating liquidity is limited due to the reason that coins should be staking, so buying of 1% - 5% of the total supply should empty exchanges and significantly drive the prices up. It has visible effect and the community defenitly note it. 

Even at the current prices half of the staking coins is approximately 144BTC that is 30 times more than in the case with Zcash.

```
Let's say it again: 
The initial investments to attack Cutcoin are ~40 times higher 
then those to attack Zcash that has 104 times bigger capitalization
```

### Strightforward 51 Percent Attack

The straightforward attack requires 3 main steps to be done:
- gain the control over the blockchain (buy 51% of the staking supply);
- successful realization of the fraud strategy (double spend, transaction rollback, etc);
- sell the coins back on the market (sell 51% of the staking supply).

Obviously, the market responds to events related to the specific coin. As we mentioned before, such types of attacks cannot remain undetected, so after step 2 the market price of a coin goes down. Historical data [4] let us expect at least a 30-50% price drop for PoS coin, that is approximately 20% of the total supply. To make a profit an attacker needs to double spend, or withdraw, at least 20% of the total supply (beyond those 40% that give him the control over the blockchain). In reality, this estimation is extremely optimistical, from the point of view of an attacker, as we didn't take into account multiple overheads, such as exchange fees, market response to the buying of 40% of total coin supply, lost profits from staking etc. This scenario demonstrates that big initial investments and multiple risks don't guarantee any profits.

### Short Selling Attack

This attack is the further development of 'Straightforward 51 Percent Attack'. An attacker follow this scheme:

- gain the control over the blockchain; (buy 51% of the staking supply);
- short sells of the (borrowed) coin on the market;
- public comprometation of the blockchain;
- sell the coins back on the market (sell 51% of the staking supply).

This strategy has been investigated for example in [4]. The attacker's profit can be estimated as [(short sold coins) - (coins being on stake)] * (coin price drop). Fees, price movements and other overheads are not taken into account. We can see that the profit is positive if (short sold coins) > (coins being on stake). As Cutcoin has a flat staking mechanism (not a delegated PoS or multi layered nodes with different ranks), short sold coins must be > 40% (and 40% are on stake at the same time). This looks theoretically possible, but in practice no exchange can borrow such a liquidity, as it brings significant risks for them, at least for the reason that someone could try to withdraw it. Worth to mention that at the moment we don't know any public exchange that allows to open short positions in Cutcoin at all.

### Takeaways

If applying non-cooperative game theory that describes the behaviour of actors, each plays independently to maximize his profit, to PoS protocol, it appears, that the system incentivizes them to follow 'honest strategy' as it gives stable profits and minimizes reputational losses and financial risks.


[1] https://coinmarketcap.com/currencies/zcash

[2] https://www.nicehash.com/my/marketplace/ZHASH

[3] https://coinmarketcap.com/currencies/cutcoin

[4] https://eprint.iacr.org/2020/019.pdf

