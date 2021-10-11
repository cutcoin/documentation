# General questions
## What is CUTcoin? 
CUTcoin is a CryptoNote-inspired privacy cryptocurrency. The CUT users can enjoy enhanced privacy of their personal data and confidentiality of transactions. CUT can be purchased on various exchanges.

Besides CUTcoin, CUTcoin Staking Pool and the first privacy-centric tokens CNT-1 were developed.

## What's a privacy cryptocurrency? 

Privacy coins focus on keeping transactions anonymous and untraceable. Anonymity disassociates your identity from your wallet and specific transactions while untraceability prevents outside parties from piecing together your blockchain activity. They do this in a process called chain analysis.

## How does it differ from Monero?

First off, CUT makes use of Proof of Stake instead of Proof of Work consensus, and that means less electricity use and eco-friendliness. Besides, the traditional block timing algorithm has been modified and modulated by a nonlinear function so blocks are following target time more closely than the usual Poisson distribution. Also some minor fixes were made.

## Where can one get CUT?

CUT is currently listed on [STEX](https://app.stex.com/en/trade/pair/BTC/CUT/1D), [CREX24](https://crex24.com/exchange/CUT-BTC), [P2PB2B](https://p2pb2b.io/trade/CUT_BTC) and [Tradeogre](https://tradeogre.com/exchange/BTC-CUT).

# Technical questions

## Network settings for Cutcoin

Cutcoin nodes establish a distributed P2P single layer network and rely on the standard TCP/IP protocols. Most often, you don't need to make any special settings in your network environment. 

In some cases network providers or OS may partially block network traffic and you need to dive into technical details. Cutcoin daemon is the crucial part of the network infrastructure. It does multiple exchanges with other daemons when sharing the current blockchain state, pool of the new transactions, data about nodes in the network etc. You can check several things that may go wrong.

1. Seed nodes. Our team supports a bunch of seed nodes which help to explore the network as the daemon is started.

The seed nodes for testnet are

```
94.130.65.238:25257
23.111.23.171:25257
```

and for mainnet

```
94.130.65.238:24247
23.111.23.171:24247
173.0.156.248:24247
103.23.208.219:24247
```

We use 'ip_address':'port' format to specify them.

[Ping](https://en.wikipedia.org/wiki/Ping_(networking_utility)) these nodes to check that your node can reach them: 

```
ping ip_address
```

If the nodes are unreachable, it is likely that your daemon won't be able to establish the connection with the Cutcoin network.

You may also need to open the ports (25257 for testnet and 24247 for mainnet) or ask the provider to do it.

2.Network speed. 

When dutcoin daemon is running, type

```
print_cn
```

in the terminal and you will get the network stats per connected peer. 'Recv/Sent' column shows the traffic.

After that, use any online [Network speed measurement tool] (https://www.speedtest.net) to find the entire connection throughout. If it is much bigger than the cutcoin daemon traffic, it is likely that your connection speed is enough for Cutcoin network.

## Is CUT a PoW or PoS coin? 
CUTcoin started out as a PoW coin that used CUTcoin's own hashing algorithm. On March 7th, 2019 at block 52 000, CUTcoin switched to PoS.

## Is CUT vulnerable to 51% attack?
As known, 51% attack is when a miner or mining pool controls 51% of the computational power of the network and creates fraudulent blocks of transactions for himself while invalidating the transactions of others in the network. With a PoS, the attacker would need to obtain 51% of the cryptocurrency to carry out a 51% attack, which becomes very costly with the growth of the network, let alone it will require quite some coding both in daemon and in the wallet.

Let's assume you need 40 confirmation to deposit to exchange. Even if you have a group of 75% of the stake that signs "official" and "alternative" chain, chances that 75% can grow a heavier chain than 100% are quite low. The 75% are much better doing classical attack — leave the other 25% alone to build a weaker chain. Eventually it boils down to convincing more than half of the anonymous stake to perform an attack that will in fact discredit the chain and the coin. It’s neither feasible nor reasonable.

We've added more detailed investigation of the possible scenario [here](https://github.com/cutcoin/documentation/blob/master/51-percent-attack.md).

## What was a premine?
There was a premine of 2% (4M coins). 9.3% of the coins were minted during the PoW phase (18 506 411 CUT) which leaves 88.7% for the PoS era, or 179 493 589 CUT. About 250 CUT are minted every 2 minutes, and after a total supply of 200M is reached, tail emission of 0.6 CUT per block will begin.

## How was premine distributed?
The premine was locked up in a custody solution not associated with the CUTcoin team. This was done based on the reasoning that the team may need to pay for development of core features. The use of funds can only be decided by unanimous decision of the core team members, and the CUT community be notified.

## What PoS algorithm does CUTcoin use?
CUTcoin uses a significantly revised version of Nxt Proof of Stake protocol. The updated version is called Byzantine Berserker. More details in the original [whitepaper](https://static.cutcoin.org/cutcoin-whitepaper-v1.0.pdf).

## How does staking work?
The explanation can be found [here](https://cutcoin.org/stakingguide).

## Is the CNT-1 token standard the same as ERC20? 
Not exactly. While ERC-20 is used for all smart contracts on the Ethereum blockchain for token implementation, CNT-1 tokens are designed to be used in the CUTcoin blockchain for privacy-enhanced tokenization. With a growth of DeFi protocols, privacy becomes a domain of high importance, and we believe CNT-1 can be the laying ground of new projects and applications.

## Do CNT-1 tokens support smart contracts?
In the particular implementation there’s no smart contract support.

## What is the coin burn address and how can I explore transfers to it?
Cutcoin has a special 'coin burn addres' which can be used to burn coins. If somebody sends coins to this address they can never be spent as the private spend key is not known. [Here](https://github.com/cutcoin/documentation/blob/master/coin-burn-address.md) is the short document about it.

# Privacy questions
## “I have nothing to hide”
The "nothing to hide" argument argues that surveillance does not threaten confidentiality if they do not disclose illegal activity, and that if they do disclose illegal activity, the person doing the activity has no right to keep it confidential.

And we strongly disagree with it. Privacy is an essential human right. Privacy is about respecting individuals. If a person has a reasonable desire to keep something private, it is disrespectful to ignore that person’s wishes without a compelling reason to do so.

## Is there any way I can hide my node IP address?
In order to mitigate the risk of linking the personal information such as IP addresses or other to transactions and addresses on the blockchain, TOR/I2P/VPN can be used.

## Is there any place where we can list all available nodes in the cutcoin network?
No, as the network is decentralized. 
