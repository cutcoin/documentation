## Staking CUT on a Raspberry pi



Model: Raspberry Pi 3+

OS: ubuntu-mate-18.04.2

The first thing we need to do is load the OS onto our SD card. Get Ubuntu Mate [from here](https://ubuntu-mate.org/raspberry-pi/)
and flash it onto the SD card. Now boot up, and make sure the system is up to date with

    sudo apt-get update
    sudo apt-get upgrade
    
This will take a long time.

Since Raspberry Pis all have MAC addresses starting with `b8:27:eb`, it will protect our privacy even more to spoof the address. This can be done easily in Ubuntu mate by going to Network Connections -> Edit Connections -> Settings and setting "Cloned MAC address" to random.

Next we will increase the size of the swap file so we can build CUTcoin. An explanation of the steps can be [found here](https://askubuntu.com/questions/1075505/how-do-i-increase-swapfile-in-ubuntu-18-04), but here are the commands in
order for those who want to get right to it:

    sudo swapoff /swapfile
    sudo rm  /swapfile
    sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
    sudo chmod 600 /swapfile
    sudo mkswap /swapfile
    sudo swapon /swapfile

You can verify that it worked by doing

    swapon -s
    
First we will install the dependencies with

    sudo apt update && sudo apt install build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev doxygen graphviz libpgm-dev
    
And then we will build the libgtest-dev library binary with

    sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake . && sudo make && sudo mv libg* /usr/lib/
    
After we return to the home folder with

    cd ~
    
we are finally ready to clone the repository and build CUTcoin!

    git clone --recursive https://github.com/cutcoin/cutcoin
    cd cutcoin
    git checkout master
    make
    
Building takes about 12 hours. After it's built, we can navigate to the CUTcoin folder and launch the daemon with

    cd /home/pi/cutcoin/build/Linux/master/release/bin
    ./cutcoind
    
And now we have to wait to synch the blockchain. This also takes a long time. After it's ready, open a new tab with `shift + control + t` and do

    ./cutcoin-wallet-cli
    
in the new terminal tab. From this point on we will be working in the new terminal window.
We can now create our cutcoin wallet, get our coins, and let them age for 800 blocks (approx 26 hours) before we can stake.
In order to stake most efficiently, we should break up our stash of CUTcoin into groups of 1/10/100/1000. This can be done by 
generating new subaddresses with

    address new

and sending coins to the new address. For example, if I have 1321 CUT then I would generate 7 new addresses and send 1000 CUT to
 address 1, 100 CUT to address 2, 100 CUT to address 3, 100 CUT to address 4, 10 CUT to address 5, 10 CUT to address 6 and 1 CUT
 to address 7 (1000 + 100 + 100 + 100 + 10 + 10 + 1 = 1321). The transaction would look something like this:
 
    transfer address_1 1000 address_2 100 address_3 100 address_4 100 address_5 10 address_6 10 address_7 1
 
An in depth CLI wallet guide can be [found here](https://github.com/Satori-Nakamoto/simplewallet-guide/blob/master/guide.md).

Now we have to wait those 800 blocks, and then we can start staking with 

    start_staking
    
If you want to see staking updates in the console, use

    start_staking verbose

That’s it! Now we are an active part of the CUTcoin network. 
Congratulations, and keep on staking in the free world!
