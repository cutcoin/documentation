
# Cutcoin 3.0.2 testnet with CryptoNote Tokens (CNT1) User Manual.

## Introduction

Cutcoin Token is the named entity representing a specific value. Once created, token can be owned or sent to another owner. No token duplicates (tokens with the same names) are allowed.

CryptoNote Tokens implemented in Cutcoin is the extention of CryptoNote protocol that allows creating and manipulating named tokens. Tokens are very similar to the coin itself, and that's one of their advantages: well known and time proved protocol that guarantees reliable privacy and security. The only place where the information about tokens is stored is the Cutcoin blockchain, and this means no additional centralization were brought.

Tokens have unique names and the corresponding unique ids. Cutcoin id is 0 (zero). Each transaction output in the system has its id, and it's not encrypted, so users can see it. When a transaction with tokens has been sent, somebody can note that the tokens with specific id are circulating, but the sender and receiver are not known due to one time addreses protocol. Transaction amounts are also hidden thanks to Ring Confidential Transaction (RCT), so overall privacy is not worse than Cutcoin's one.

## User operations

### To create a new token comman line (cli) wallet can be used. The requirements for this operation are:

-token name must be unique, i.e. no other token with the same name has been created and persisted in Cutcoin blockchain. Token name can consist of English capitalized letters and digits, length is 1 - 8 symbols. CUT and CUTCOIN names are not allowed for security reasons.

-token creation fee (TCF) + transaction fee must be payed in cutcoins, so the user must have enaugh balance. Current TCF is 100CUT, it's a flat rate that doesn't depent on name, token supply or anything else. Transaction fee is estimated dinamically during the process of transaction creation, but in the most of the cases it is less then 1CUT. So, one should have 101CUT to create a token. TCF goes to so called 'coinburn address' which is public, but all funds it receives become unspendable for any user.

The token creation command is

```
create_token <token_name> <token_supply>
```

token_name, as described before, is the user defined name of the token. It has integer representation called 'token id'. Token id and token names have one-to-one relation: 'token name' -> 'token id', 'token id' -> 'token name'. This means, consequently, that token id is also unique.

token supply is the total number of tokens with the 'token_name'. It can be value in the range 1 .. 200 000 000, the latter is the total Cutcoin supply.

The transaction that creates new token is called 'token genesis transaction' (tgtx). It has a specific structire and acceptance rules as, figurally, tokens being created out of thin air.

Tokens have same default spendable age (10 blocks) as Cutcoin, so they can be transferred in approximately 20 minutes after their creation.


### Information about token balance in cli wallet.
Command that lists tokens with their balance is 

```
token_balance [token_name] [detail]
```

'token_balance' without arguments lists all tokens form the current balance, you can see an example below

```
Currently selected account: [0] Primary account
Tag: (No tag assigned)
           Name               Balance      Unlocked balance              Token ID
        CUTCOIN       9091.6249630036       9091.6249630036                     0
          ALPHA         20.0000000000         20.0000000000   4705223981953712128
             G3        890.0000000000        890.0000000000   5130444400505126912
          GAMMA        199.0000000000        199.0000000000   5134470044377415680
```

If the 'token_name' is specified, the output contains an information for a single token:

```
Currently selected account: [0] Primary account
Tag: (No tag assigned)
           Name               Balance      Unlocked balance              Token ID
          ALPHA         20.0000000000         20.0000000000   4705223981953712128
```

'detail' is the optional flag that enables extended output with splits by subaddresses

```
Currently selected account: [0] Primary account
Tag: (No tag assigned)
           Name               Balance      Unlocked balance              Token ID
          ALPHA         20.0000000000         20.0000000000   4705223981953712128

ALPHA balance per address:
        Address               Balance      Unlocked balance                 Label
       0 TCU1qy         20.0000000000         20.0000000000       Primary account
```

The major new features are beyond just three commands:


### Transferring tokens between accounts.

For token transfers 'transfer_token' command should be used:

```
transfer_token <token_name> <address> <amount>
```

It has 3 required parameters. 'token_name' is the name of the token that needs to be transferred, 'address' is the wallet address of the receiver and 'amount' is amount of tokens to transfer. This command cannot be used to transfer cutcoins. Multiple tokens / multiple destinations also cannot be specified (will be implemented in the future). This transaction, as any other cutcoin transaction, has its fee that depends on its size. This fee can by payed only in cutcoins, and it means one should have enaugh cutcoin balance (and cerainly token balance too) to transfer tokens.

The example of 'transfer_token' output:

```
transfer_token ALPHA TCU1qyPcrNfS1mnbYB6C5FfTc4yJqLN4kL1t3P3Bkr7SMBRcBzdYKkDUFDSQTfMzjTXEBzqu29bEZR91PKbWxmzY3ah3X5SDJs 5
Wallet password: 
No payment id is included with this transaction. Is this okay?  (Y/Yes/N/No): y
Transaction successfully submitted, transaction <a18a55f432cb21d1cfd10ce13967f9c40e9102952c205130a6de85e245aad361>
You can check its status by using the `show_transfers` command.
```

### Explore all CNT1 tokens.

Useres can list all tokens ever created in the blockchain using the command 'get_tokens':

```
get_tokens [token_name_prefix]
```

This command has an optional mask 'token_name_prefix' that filters output. The example of this command usage:

```
get_tokens
Name            Supply   Unit
   ALPHA        100      10000000000
    BETA        200      10000000000
 BITCOIN        21000000 10000000000
   DELTA        400      10000000000
      G7        7        10000000000
   GAMMA        300      10000000000
```

### List payments including tokens.

Cutcoin has the command that lists transfers in the wallet, it is 'show_transfers'. It supports tokens so that each transfer has a specific token name in its outline that clarify what exactly was transferred. The example output is below:

```
show_transfers
  368114     in       2020-07-09 09:48:30 CUTCOIN        10.0000000000 578da8fa5af7cb41e4366c9b571504f5114a7238c889833121104b9f089554b8 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07 CUTCOIN       100.0000000000 187f11c56e75545ca82cf01fcc14238e6fa985aa1c53dae77259e21588789ddd 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07 CUTCOIN        10.0000000000 f5cfb6c0705c5fac52764bca3df57afcf1833a8df5d7fe523632384d8e817ab0 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07 CUTCOIN        10.0000000000 44736fffd8168a2414706112fd98fd34c6a480c88828abbf8634ea8fe530d975 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07 CUTCOIN        10.0000000000 0222e6079f42fb2e2ee447950560e090b9cc141157adfdb8f6242aff1c40b73b 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07 CUTCOIN       100.0000000000 d469868314a53bf678bffa282cb49b06b3b7a14caf2c9ef8bfd116e2b0f6455e 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07 CUTCOIN        10.0000000000 023f17b872aa33322824e647424fdccc3b5cfe4a7c05c1b805449930aa68571c 0000000000000000 0 - 
  368116     in       2020-07-09 09:52:06 CUTCOIN       500.0000000000 2d88ecda0fab96bdcc21b36c41ace49794bead1fc9cc12399526a5968240c642 0000000000000000 0 - 
  368130     in       2020-07-09 10:20:16 Z3  33333333.0000000000 9c9fca8b6bf3841f116461d819d6a9ba3b9a6b054f751bd12b1bd243d646cab0 0000000000000000 0 - 
  368130    out       2020-07-09 10:20:16 CUTCOIN       100.0000000000 9c9fca8b6bf3841f116461d819d6a9ba3b9a6b054f751bd12b1bd243d646cab0 0000000000000000   0.0709820600  0 - 
  368131     in       2020-07-09 10:22:00 Z2       100.0000000000 0515e38b86e07003f048f985b7ba0b51553066a9087c67cd7f71f422147352d2 0000000000000000 0 - 
  368131    out       2020-07-09 10:22:00 CUTCOIN       100.0000000000 0515e38b86e07003f048f985b7ba0b51553066a9087c67cd7f71f422147352d2 0000000000000000   0.0709450100  0 - 
  368132     in       2020-07-09 10:23:49 Z1     10000.0000000000 5a54bb956c7ee45c7b01815cb0a927c631c0cfb52ded095419fcfd015bfb285e 0000000000000000 0 - 
  368132    out       2020-07-09 10:23:49 CUTCOIN       100.0000000000 5a54bb956c7ee45c7b01815cb0a927c631c0cfb52ded095419fcfd015bfb285e 0000000000000000   0.0709635300  0 - 
```
