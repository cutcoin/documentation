# Cutcoin Staking Guide

### Coin emission schedule

Coin emission started at December 2018 with PoW mining stage. In 72 days a total of 18 506 411 CUT (9.3%) were mined.

After switching to PoS consensus there are 179 493 589 CUT left with block rewards of approximately 300 coins every 2 minutes.

As mentioned before, after total supply of 200 000 000 is reached a tail-emission will be operated. 

### Some technical information

A valid Proof of Stake block would have a miner (coinbase) transaction with block reward just as Proof of Work blocks have. 
However in addition to this the block has a coinstake transaction as first transaction in the block. 
This transaction needs to have exactly one unspent output as transaction input which must be confirmed by at least 800 blocks. 
In fact all the mixins (the true input and mixing decoys, see Ring signatures) must be confirmed by 800 blocks. 
Also the hash of concatenation of previous' block Proof of Stake hash and the key image of the output combined with the amount of the output must satisfy 
the current network difficulty. This coinstake transaction may have a zero transaction fee. 

1. Your (non-empty) wallet has number of so called "unspent outputs".
You can see the list of those by executing the command "unspent_outputs" in the wallet. 
Each output has some "amount" of coins. 
When sending coins, the wallet will pick some unspent outputs, enough to cover the desired transfer sum plus transaction fees, 
make them inputs for a transaction and send whatever is above desired sum back to your wallet as change.

2. Outputs must be confirmed by 800 blocks to be eligible to mint a block, therefore earning a staking reward.
While this basically just means that new coins need to stay roughly a day in your wallet to start competing for block reward, there is one more caveat. 
After being able to mint a block, the output will be recycled into another output of the same amount. 
Additional output with the block reward will also be received by the wallet. 
All those new outputs also need to mature for 800 blocks. 
This means that really big outputs will produce less rewards than their fair share. 
For example if you have output of 100000 coins and the sum of all staked coins is 20 million, this particular output is expected to get one block in 200. 
However due to maturity requirement it will get on average one in 1000. 
This is however solvable by just splitting your outputs into smaller ones (covered later). 
For amounts of 1000 and lower the maturity requirement will not have measurable impact.

3. For staking only the integer part of output amount is taken into consideration.
That is output of 2.89 coins has the same chance of earning a block reward as output of 2 coins.

4. When staking, your wallet address, the amount of coins in your possession remains private information.
However in order to make larger outputs more likely to earn rewards, the amount of coins in the coinstake transaction 
(that is the amount of coins in the single output that is the input in the transaction) is made public. 
That for example allows outside observer to bet that two blocks that are more than 800 blocks apart and have some specific number of coins 
(for example 4563.8943100131) in coinstake transaction belong to the same person/wallet. 
However if the amount of coins is less specific - say 100.0 and many blocks have coinstake transaction of 100.0 coins then practically no information is revealed.

5. After the fork to start earning staking rewards.
All you need to do is execute "start_staking" in the cli wallet, enter your wallet password and leave the wallet window open. 
You need to have daemon and the wallet running in order to earn stake rewards. You can do that on a remote Linux server by running inside a "screen" session.

6. The fork the "difficulty" of the network will have expected value of total number of coins on stake.
However the difficulty algorithm will need time to converge to that value. 
So it is expected that if sum of staked coins is significantly less than the Proof of Work difficulty at fork time - blocks will come slowly at first. 
The vice-versa is also true.

Based on the above information it is our suggestion to prepare wallets for staking that only have outputs with amounts 1000, 100, 10 and 1.

To do this, create new wallet and make transaction for said amounts to that wallet. Keep in mind that you can send up to 15 transfers with one command. 
For example if you have 183.56 coins in your wallet and want to send them split into the above amounts to a new wallet with address WAL 
(the real address will be longer so the command will be harder to read and operate with) with command:

transfer WAL 100 WAL 10 WAL 10 WAL 10 WAL 10 WAL 10 WAL 10 WAL 10 WAL 10 WAL 1 WAL 1 WAL 1 

You may need to do this several times and wait change from previous transactions if you have many inputs. 
Remember to do that more than 24 hours before the fork, so you can compete for stake rewards from the very first PoS block.

TL;DR: after fork to Proof of Stake, just open your cli wallet, type "start_staking" and leave the wallet open (maybe run it inside "screen").
