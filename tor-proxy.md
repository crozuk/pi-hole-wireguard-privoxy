# Raspberry Pi - Local Network Tor Proxy Server

In this guide we’ll look at installing and configuring Tor on a Raspberry Pi to act as a proxy server providing access to Tor for any machine on the local network.

However - this is *not* using the Tor Browser so you will need to ensure the browser you are using is ‘safe’.
You’ll want a plug-in or settings change to disable JavaScript - and may want to look into various other privacy related extensions- for example blocking WebRTC.

Before we start any project -

	sudo apt-get update
	sudo apt-get upgrade

## Installing Tor
How to install the Tor software on your Raspberry Pi -

`sudo apt-get install tor`

Check your installation with -

`sudo systemctl status tor@default.service`

<img src="https://blog.richardcrosby.co.uk/content/images/2019/10/CXYvIeY.png">

## Configure Proxy Server
We need to configure Tor to open a SOCKS proxy on a port of our choosing.

1. Edit the ‘torrc’ file -

	`sudo nano /etc/tor/torrc`

2. Scroll to lines 18 and 19 which by default will be commented out.

3. Uncomment lines 18 and 19 and update accordingly -
  ```
	socksPort 666 # Desired port number
	SocksPort 192.168.1.112:666 # IP of Raspberry Pi
  ```
4. Uncomment and update line 49 as per the below -

	`RunAsDaemon 1`

4. Reload the Tor service with the updated settings -

	`sudo systemctl restart tor.service`

## Configure your clients

You've now got a proxy server running on your local network which allows any of the machines in your home to access the internet anonymously and visit .onion sites.

I recommend using a Chrome plugin called [Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif) to quickly switch between proxy servers, and setup rules for auto switching. 

<img src="https://blog.richardcrosby.co.uk/content/images/2019/10/6pxX9fi.png">
<hr>
<img src="https://i.imgur.com/N2IQJ7A.png">
