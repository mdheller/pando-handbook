# Demo

This is the script that was used to give the demo during the Demo and Poster Session that was held during [SASO 2017](https://saso2017.telecom-paristech.fr/).

The demo consists in showing distribution of computation between two different laptops: a MacBook Air 2011 running OS X using an Intel processor and a Novena laptoprunning Debian Linux on an Arm processor. The MacBook Air uses Chrome as an execution environment for computations  while the Novena laptop uses Firefox ESR for the same purpose.

# Creation of an Ad hoc Network

Novena laptop

1. Install wireless-tools

    ````sudo apt-get install wireless-tools````

2. Setup the Wifi Network
  2.0 Stop the current wifi services

     ````sudo service network-manager stop
         sudo ip link set wlan0 down````

  2.1 Switch the card into ad hoc mode

     ````sudo iwconfig wlan0 mode ad-hoc````

  2.2 Set the channel

     ````sudo iwconfig wlan0 channel 4````

  2.3 Add the name of the network

     ````sudo iwconfig wlan0 essid 'Novena Wifi'````

  2.4 Add a WEP encryption key

     ````sudo iwconfig wlan0 key 1234567890````

3. Activate the Wifi Network

  3.1 Bring the interface up

    ````sudo ip link set wlan0 up````

  3.2 Setup two IP addresses for the STUN server
    ````sudo ip addr add 192.168.1.1/24 dev wlan0
        sudo ip addr add 192.168.1.2/24 dev wlan0
    ````

  3.3 Start dhclient to get an address

    ````sudo dhclient wlan0````

MBA Laptop

1. Click Wireless Network -> Select Novena Wifi
2. Type the password

Test

1. MBA: Get the ip address
  
    ````ifconfig en0````

2. Novena: Get the ip addresses, check that the two are listed

    ````ip addr````

3. Ping each other

    From MBA: ````ping <novena-ip>````
    From Novena: ````ping <mba-ip>````

Start the STUN server

0. Install the STUN server

   ````nmp install -g node-stun````

1. Run the STUN server (using the node-stun.ini configuration file)
   
   ````node-stun-server````

    If successful, you should see the following on your console:

    ````Complete(0): Open NB=I EF=I (Open to internet) mapped=127.0.0.1:61072 rtt=0````

# Demo

## Squaring Test

   asplos18

## Raytracer example

   examples/raytracer
