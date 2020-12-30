## Creating a multisig wallet

**Warning: It’s best to start this process with a new wallet. Making a wallet that’s in use into a multisig wallet will cause all the wallet’s existing funds to be subject to the multisig wallet requirements.**

Let’s make a 2/3 multisig wallet- meaning a wallet that is shared between 3 parties and requires the signature of 2 of the parties in order to send a transaction. After generating a new wallet (or 3 in the case of this tutorial example) we start by doing:

    prepare_multisig
    
![1](https://github.com/Satori-Nakamoto/images/blob/master/1.png)

The output will be:

    [wallet cutbGa]: prepare_multisig
    Wallet password: 
    MultisigV1DSRJR65GdN77VNucxD3RK6iFEqLfHuADSJVMtQkbesE3Ez6HvPhoC3GWf1uFngsH1dRsnUyTAnwL9KxV7y9tpE8dPqpjadXcDryP2ECp8wq1fx37q5Vb4aYVWbuf49jo1MCUgPXAb43PSzc5ppRhhYPzGoBbsajRCbeMwbVZrRRcL3mb
    Send this multisig info to all other participants, then use make_multisig <threshold> <info1> [<info2>...] with others' multisig info
    This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants

All parties involved need to run this command and share their respective output line (MultisigV1DSRJR65GdN77 in our case) with all other parties, so make sure to save that output line somewhere for easy access.

Let’s say that our 2 friends gave us their multisig info as follows:

    MultisigV1hkLReF9FjaPBaqmP7BVoJvUjYkMk6BLKRJ4L5537TapGbE851PdayfKcKD4RwHKcURYiYAVpZYVFs2JHFJVpXpjNghRrBVbtDgTKxcBSvTD8YaBYzjGyQFATDHEktEYXdFLfefDg9V7FuhFLEPD1gY5ENoQpnndG7LQqbA5QLHXj5DkV

    MultisigV15dPoYDwZygZ7UQCB2qvxA4erVwo6iEs2WgFHgZivL2xEYvkzMhtg2S4CYNghK2ghTkAAPju2ZXs1xX8TJx9HCb2Z6gbAt71WTtiQ6u8kqHgeB5W8Ttku1UxNZXMvUmgfgMgFG3JmXo9P91iJCBZbZnxrz2MdsZVP6V8Qj2gYAALCDan7

Now we do *make_multisig <# of signatures needed to send funds> <friends’ multisig info>*

    make_multisig 2 MultisigV1hkLReF9FjaPBaqmP7BVoJvUjYkMk6BLKRJ4L5537TapGbE851PdayfKcKD4RwHKcURYiYAVpZYVFs2JHFJVpXpjNghRrBVbtDgTKxcBSvTD8YaBYzjGyQFATDHEktEYXdFLfefDg9V7FuhFLEPD1gY5ENoQpnndG7LQqbA5QLHXj5DkV MultisigV15dPoYDwZygZ7UQCB2qvxA4erVwo6iEs2WgFHgZivL2xEYvkzMhtg2S4CYNghK2ghTkAAPju2ZXs1xX8TJx9HCb2Z6gbAt71WTtiQ6u8kqHgeB5W8Ttku1UxNZXMvUmgfgMgFG3JmXo9P91iJCBZbZnxrz2MdsZVP6V8Qj2gYAALCDan7

![2](https://github.com/Satori-Nakamoto/images/blob/master/2.png)

Each friend does the same. You can see in this example the different terminal tabs represent different friends, 3 in total + the daemon.

![3](https://github.com/Satori-Nakamoto/images/blob/master/3.png)

Note that there’s a space between the 2 strings of multisig info from our friends, and we do not include our own multisig info in this command. The output will be something like:

    Another step is needed
    MultisigxV1TCGmNkpcSb8SENuNmDEAx6b6Be67Z1TicNFeQQ3J8KKCUUuxvk2ajuQT94vAa6RBbwZyJ1WbwtEVeNQ8B6MT63Wr96cnQCxBHyYbLvbA5exGkdBAyMD3AKyLQLBjv22KYs2H2w2zNPd2CKNZWSMXvoZ38U492UUrJh51ScdxiyLvgEnsBp5oPRH4Uu8CJ5DJXMLtUXZGnbPi3KyJCbVE76Kd4igz
    Send this multisig info to all other participants, then use exchange_multisig_keys <info1> [<info2>...] with others' multisig info

This is telling us to do almost the exact same thing one more time. Each person does finalize_multisig with the output line of the other 2 friends. Our output line was [MultisigxV1TCG...d4igz] and our friends gave us the output lines [MultisigxV1esM...6G55E] and [MultisigxV1TNB...rZ46h], so for this example:

    finalize_multisig MultisigxV1esMjZa49V2Z6v2ba6py9hcjdix9MMGJd6eaLsX4fdVX3UUuxvk2ajuQT94vAa6RBbwZyJ1WbwtEVeNQ8B6MT63Wrf4NwsddmnrQb9dG25S3WmqYPm71R6Eq9Q96mdfsXL7QFbomjWnjLrMrCi1Pfnwpnh9ToxiGCYt84g3nF59BqyRfHEvobVC2XP62EesGgLJFHev7DC1NMrU4TyG7XU5g6G55E MultisigxV1TNBskx8eLvaJ9ceS4R1b64N57X67j5BeDU75ngzGGa5c96cnQCxBHyYbLvbA5exGkdBAyMD3AKyLQLBjv22KYs2Hf4NwsddmnrQb9dG25S3WmqYPm71R6Eq9Q96mdfsXL7QFKhiyQ8cGsshBW9UoAjvppQS2FHD6wTwzfZushb45Tz6nMJk3WBREJW8a7Q36E3NEQW6rKgGsvk33yUAoSdorZ46h

Remember to put a space between the sets of multisig info. There should be no output, but you will notice that the wallet address has changed.

Your new, multisig wallet address can be found by doing

    address

and you will notice that now all 3 parties have the same wallet address:

![4](https://github.com/Satori-Nakamoto/images/blob/master/4.png)
![5](https://github.com/Satori-Nakamoto/images/blob/master/5.png)
![6](https://github.com/Satori-Nakamoto/images/blob/master/6.png)


## Spending from a multisig wallet

After our multisig wallet has some funds on it, let’s spend them. Upon receiving funds, the wallet will show the message

    (Some owned outputs have partial key images - import_multisig_info needed)

If the input is received while the wallet is open, it will look like this

![s1](https://github.com/Satori-Nakamoto/images/blob/master/s1.png)

and should it receive an input while closed, the next time the wallet is opened it will display this

![s2](https://github.com/Satori-Nakamoto/images/blob/master/s2.png)

To proceed to spending, we first need to exchange multisig info with our friends. Since this is a 2/3 multisig wallet, we need the info from 1 friend to complete a transaction. Alternatively, we could get the info from both friends and decide later which info to sign with. First we’ll export our multisig info by using the command export_multisig_info and any file name, like:

    export_multisig_info multis1

![s3](https://github.com/Satori-Nakamoto/images/blob/master/s3.png)

The exported file will be in the same folder as your wallets, in this case /home/cut/cutcoin/build/Linux/master/release/bin. We need to send this to our 2 friends so they can sign a transaction, and they need to send their exported multisig info to us.

Now we’ll import our friends’ multisig info files. By default, the wallet will look in the shell working folder for the files (that was /home/cut/cutcoin/build/Linux/master/release/bin in this case, but can vary if you have an advanced setup), so make sure the files are there. The file “multis 2” should be in friend #2’s wallet folder since he exported it there, same for “multis 3”. After we have all 3 multisig info files, we use the import_multisig_info command:

    import_multisig_info multis2 multis3

![s4](https://github.com/Satori-Nakamoto/images/blob/master/s4.png)

The output will tell us the balance our multisig wallet has to work with, and that multisig info was imported. See the photo above for reference.

Now let’s spend!

Any of the 3 friends can start the transaction, and will need to get the signature from 1 of the other 2 friends. Start the transaction as usual

    transfer ctsFE4koe1VjaM5qm6GNGd7oCT26j5xAtMgDopVFV7NCKFhAV8Be5SXXaiLD1v9RD3RDrvnbSGdS26Rjw4tYFu1r3SjE9Qoxuf 1

![s5](https://github.com/Satori-Nakamoto/images/blob/master/s5.png)

This will generate a file called multisig_cutcoin_tx in your shell working folder, the same folder mentioned earlier. (The screenshots in this guide are from an early version of the software, before rebranding, so they show instead multisig_monero_tx). For peace of mind, let’s do one transaction at a time. Let’s choose friend #2 to complete the signature for this transaction. If we choose a friend that we did not import the multisig file info from, we will get the error

    Error: Failed to sign multisig transaction: Final signed transaction not found: this transaction was likely made without our export data, so we cannot sign it

Also, if our friend will send the transaction, he needs to have our file multisig_cutcoin_tx in his shell working folder and then he can use sign_multisig with the file multisig_cutcoin_tx. Whoever will send the transaction will do

    sign_multisig multisig_cutcoin_tx

![s7](https://github.com/Satori-Nakamoto/images/blob/master/s7.png)

After verifying the address, amount, fees, ring size, and change address, our friend will press y and the transaction will be successfully signed to the file multisig_cutcoin_tx. Now the transaction is ready to be relayed to the network. Our friend can send the file back to us or broadcast it himself by doing:

    submit_multisig multisig_cutcoin_tx

![s8](https://github.com/Satori-Nakamoto/images/blob/master/s8.png)

Congratulations, transaction successfully submitted!

To recap, the sending process went like:

- At least 2 friends export_multisig_info and share their file with the other one (or both).
- The other friend (or both) uses import_multisig_info with at least 1 other multisig info file.
- Any of the friends with imported multisig info can start the transaction using the normal transfer command and generate a file called “multisig_cutcoin_tx”, which should be sent to at least 1 other friend for signing.
- At least 1 of the other 2 friends needs to sign this file by doing sign_multisig multisig_cutcoin_tx on the file
- The signed file is submitted to the network with submit_multisig multisig_cutcoin_tx

If the friends want to send another transaction, they should go back to step 1 and start the process again. If you don’t delete the file multisig_cutcoin_tx it will just be overwritten next time a multisig transaction is created.
