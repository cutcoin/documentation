
# Cutcoin CryptoNote Tokens (CNT1) User Manual

## Introduction

Cutcoin Token is the named entity representing a specific value. Once created, tokens can be owned or sent to another owner. No duplicate token names are allowed.

CryptoNote Tokens implemented in the Cutcoin eco-system are an extension of the CryptoNote protocol that allows users to create uniquely-named privacy-focused assets on the Cutcoin chain. Tokens are very similar to the native coin itself and It is one of their advantages: a well-known and time-proven protocol that guarantees reliable privacy and security. The only place where the token information stored is the Cutcoin blockchain, and this means no additional centralization is added.

Tokens have unique names and corresponding unique IDs. The Cutcoin ID is '0' (zero). Each transaction output in the system has its own token ID which is not encrypted and visible on the block explorer. When a transaction with tokens has been generated, anyone can notice that the tokens with a specific ID are in circulation, but the sender and receiver are not known because of the one-time addresses protocol. Transaction amounts also remain hidden due to Ring Confidential Transaction (RCT), so overall privacy is not worse than that of the Cutcoin.

A CNT1 token can be one of the two possible types: (1) with the visible supply (2) with the hidden supply.
For the hidden supply kind of tokens, the total supply is hidden for the public and only the token creator knows the exact supply of the specific token.

## User operations

### To create a new token, command line (CLI) wallet can be used. The requirements for this operation are:

-token name must be unique, i.e. no other token with the same name has been created and persists in the Cutcoin blockchain. Token name can consist of English capitalized letters, and digits. Token name length is 1 - 8 characters. CUT and CUTCOIN names are not allowed for security reasons.

-token creation fee (TCF) + transaction fee must be payed in cutcoins, so the user must have enough balance. Current TCF is 100CUT, it's a flat rate that doesn't depend on name, token supply or anything else. Transaction fee is estimated dynamically during the process of transaction creation, but in most of the cases it is less then 1CUT. So, one should have 101CUT to create a token. TCF goes to so called 'coinburn address' which is public, but all funds it receives become unspendable for any user.

Coin burn address has the following keys:

```
address           cutbEUhEhaWeG3dRDmWGy8UGLeDsU9EHcEhXGRrXi47NSj2PXpjaMKoce411rzhwggYGFy7MyTy27BMrQm55NNhF5yAm4c1ADi
view public key  <cb610f52bad51212e0ec4aa205bae8e0fe0df555b03def7ca332fbd29a831bbc>
view secret key  <86364a7a4e558ca836cd57aa0e54129d343b3d4347494f53596165676b6d710f>
spend public key <869fa358dfdec268a32fea169ba300e8da06ad0e4751e61daea5429a4599cc0a>
```

The token creation command is

```
create_token <token_name> <token_supply> [token_type]
```

'token_name', as described before, is the user defined name of the token. It has integer representation called 'token id'. Token id and token names have one-to-one relation: 'token name' -> 'token id', 'token id' -> 'token name'. This means, consequently, that token id is also unique.

'token_supply' is the total number of tokens with the 'token_name'. For tokens with public supply it can be value in the range 1 .. 1 844 674 407, the latter value is 

```
max(uint_64t) / COIN, COIN = 10 000 000 000.
```

For tokens with private supply it can also be in the range 1 .. 1 844 674 407, but the daemons don't check the exact value (as they don't see it) and give no garantees about it.

'token_type' is the optional parameter that defines token supply visibility. Supported token types are 'hidden' for tokens with the hidden supply and 'public' for tokens with publicly visible supply.

The transaction that creates new token is called 'token genesis transaction' (tgtx). It has a specific structire and acceptance rules since, figurally, tokens are being created out of thin air.

Tokens have same default spendable age (10 blocks) as Cutcoin, so they can be transferred in approximately 20 minutes after their creation.


### Information about token balance in cli wallet.
Command that lists tokens with their balance is 

```
token_balance [token_name] [detail]
```

'token_balance' without arguments lists all tokens form the current balance, you can see an example below

```
token_balance
Currently selected account: [0] Primary account
Tag: (No tag assigned)
           Name               Balance      Unlocked balance
        CUTCOIN        449.7591874800        449.7591874800
             Z1      10000.0000000000      10000.0000000000
             Z2        100.0000000000        100.0000000000
             Z3   33333333.0000000000   33333333.0000000000
```

If the 'token_name' is specified, the output contains an information for a single token:

```
token_balance ALPHA
Currently selected account: [0] Primary account
Tag: (No tag assigned)
           Name               Balance      Unlocked balance
             Z1      10000.0000000000      10000.0000000000
```

'detail' is the optional flag that enables extended output with splits by subaddresses

```
token_balance detail
Currently selected account: [0] Primary account
Tag: (No tag assigned)
           Name               Balance      Unlocked balance
             Z1      10000.0000000000      10000.0000000000

Z1 balance per address:
        Address               Balance      Unlocked balance Outputs                 Label
       0 TCU1ZN      10000.0000000000      10000.0000000000      11       Primary account
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

Users can list all tokens ever created in the blockchain using the command 'get_tokens':

```
get_tokens [token_name_prefix]
```
The output looks like this:

```
get_tokens
           Name              Token ID                Supply                  Unit           Type
          ALPHA   4705223981953712128                   100           10000000000  public supply
           BETA   4775315618045886464                   200           10000000000  public supply
           BONG   4778123796513030144                   650           10000000000  public supply
          DELTA   4919422092723617792                   400           10000000000  public supply
          GAMMA   5134470044377415680                   300           10000000000  public supply
         REBONG   5928217392886251520                    15           10000000000  public supply
             Z1   6498975737272336384                 10000           10000000000  public supply
             Z2   6499257212249047040                   100           10000000000  public supply
             Z3   6499538687225757696              33333333           10000000000  public supply
         T02249   6066403889273962496                     0           10000000000 private supply
```

This command has an optional mask 'token_name_prefix' that filters output. The example of this command usage:

```
get_tokens D
Name    	Supply	Unit
   DELTA	400	10000000000
```

### List payments including tokens.

Cutcoin has the command that lists transfers in the wallet, it is 'show_transfers'. It supports tokens so that each transfer has a specific token name in its outline that clarify what exactly was transferred. The example output is below:

```
show_transfers
  368114     in       2020-07-09 09:48:30  CUTCOIN        10.0000000000 578da8fa5af7cb41e4366c9b571504f5114a7238c889833121104b9f089554b8 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07  CUTCOIN       100.0000000000 187f11c56e75545ca82cf01fcc14238e6fa985aa1c53dae77259e21588789ddd 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07  CUTCOIN        10.0000000000 f5cfb6c0705c5fac52764bca3df57afcf1833a8df5d7fe523632384d8e817ab0 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07  CUTCOIN        10.0000000000 44736fffd8168a2414706112fd98fd34c6a480c88828abbf8634ea8fe530d975 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07  CUTCOIN        10.0000000000 0222e6079f42fb2e2ee447950560e090b9cc141157adfdb8f6242aff1c40b73b 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07  CUTCOIN       100.0000000000 d469868314a53bf678bffa282cb49b06b3b7a14caf2c9ef8bfd116e2b0f6455e 0000000000000000 0 - 
  368115     in       2020-07-09 09:50:07  CUTCOIN        10.0000000000 023f17b872aa33322824e647424fdccc3b5cfe4a7c05c1b805449930aa68571c 0000000000000000 0 - 
  368116     in       2020-07-09 09:52:06  CUTCOIN       500.0000000000 2d88ecda0fab96bdcc21b36c41ace49794bead1fc9cc12399526a5968240c642 0000000000000000 0 - 
  368130     in       2020-07-09 10:20:16       Z3  33333333.0000000000 9c9fca8b6bf3841f116461d819d6a9ba3b9a6b054f751bd12b1bd243d646cab0 0000000000000000 0 - 
  368130    out       2020-07-09 10:20:16  CUTCOIN       100.0000000000 9c9fca8b6bf3841f116461d819d6a9ba3b9a6b054f751bd12b1bd243d646cab0 0000000000000000   0.0709820600  0 - 
  368131     in       2020-07-09 10:22:00       Z2       100.0000000000 0515e38b86e07003f048f985b7ba0b51553066a9087c67cd7f71f422147352d2 0000000000000000 0 - 
  368131    out       2020-07-09 10:22:00  CUTCOIN       100.0000000000 0515e38b86e07003f048f985b7ba0b51553066a9087c67cd7f71f422147352d2 0000000000000000   0.0709450100  0 - 
  368132     in       2020-07-09 10:23:49       Z1     10000.0000000000 5a54bb956c7ee45c7b01815cb0a927c631c0cfb52ded095419fcfd015bfb285e 0000000000000000 0 - 
  368132    out       2020-07-09 10:23:49  CUTCOIN       100.0000000000 5a54bb956c7ee45c7b01815cb0a927c631c0cfb52ded095419fcfd015bfb285e 0000000000000000   0.0709635300  0 - 
  368807    out       2020-07-10 09:05:06       Z3         0.0000000000 0ea2183cf89304da580f42ddf1b584a04dbff759d494c87258986577714ba555 0000000000000000   0.0279219200  0 - 
```

### Coinburn address

Coinburn address is a special public address with the unknown secret spend key. 

```
Standard address: TCU1iqbfjH8eG3dRDmWGy8UGLeDsU9EHcEhXGRrXi47NSj2PXpjaMKoce411rzhwggYGFy7MyTy27BMrQm55NNhF5yAm5mSo7F
Secret view key:  86364a7a4e558ca836cd57aa0e54129d343b3d4347494f53596165676b6d710f
```

It is possible to generate the view wallet for this address:

```
./cutcoin-wallet-cli --testnet --generate-from-view-key ./wallet.bin
```

The example of balance output:

```
Starting refresh...
Height 356673, txid <6bf3189a5142acc514a12f72276c90fd33e740b8fead422ff823c8d1323dc8f0>, CUTCOIN 100.0000000000, idx 0/0
Height 356706, txid <3e9c74cde59ae025ebe4fb3ace810155b871fd4c6de139719aa4f33eceaf53df>, CUTCOIN 100.0000000000, idx 0/0
Height 358149, txid <4e2c3754afc45ccb6581bb4fcbd308df6996d1426996c224da33fa61a10b1dfe>, CUTCOIN 100.0000000000, idx 0/0
Height 361026, txid <814cfc6876e3b20bf8a362f44029c1a8c74e8a1762baf6c618c3baa71792ef1b>, CUTCOIN 100.0000000000, idx 0/0
Height 368130, txid <9c9fca8b6bf3841f116461d819d6a9ba3b9a6b054f751bd12b1bd243d646cab0>, CUTCOIN 100.0000000000, idx 0/0
Height 368131, txid <0515e38b86e07003f048f985b7ba0b51553066a9087c67cd7f71f422147352d2>, CUTCOIN 100.0000000000, idx 0/0
Height 368132, txid <5a54bb956c7ee45c7b01815cb0a927c631c0cfb52ded095419fcfd015bfb285e>, CUTCOIN 100.0000000000, idx 0/0
Height 371234, txid <aaff1ea4a102a5bb5a9018f81faffb2d0f63322abf921cef952d116afac82466>, CUTCOIN 100.0000000000, idx 0/0
Height 375545, txid <cef1e05c12f0d42156f505648a3f57894bc0b90575c6600fb31dc97d855c3970>, CUTCOIN 100.0000000000, idx 0/0
Refresh done, blocks received: 382890                           
Untagged accounts:
          Account               Balance      Unlocked balance                 Label
 *       0 TCU1iq        900.0000000000        900.0000000000       Primary account
----------------------------------------------------------------------------------
          Total        900.0000000000        900.0000000000
```
