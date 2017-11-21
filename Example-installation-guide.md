## Installation
Installing Kiwi IRC is a case of downloading the correct package for your system and installing using your usual install methods. You can find the latest installers [here](https://kiwiirc.com/downloads/).

## Configuring
Once installed, you will find the configuration files in /etc/kiwiirc/ that you can edit to set the IRC network and other settings.

There are separate files for the server and the client. The server is purposely kept as simple as possible to keep it light and secure. This is where you will be limiting the IRC networks users can connect to and adding webirc/cgi:irc passwords. This is where all the IRC connections are made on behalf of the client sat in the users browser.

The client config file handles how the webpage looks, how it loads, and the default client settings that your users see.

### The server
**config.conf** is the sever configuration that lets you whitelist or lock down which IRC networks your users can connect to. This also where your webirc or cgi:irc passwords are set.

*Note: IRC networks are referred to as upstreams in the config file.*

If you are using Kiwi IRC for a single network then you can edit the example upstream called *[upstream.1]*. By default, users using this server will only be able to connect to this upstream and no others.

For this guide, we want this server available at chat.example.com, port 80 which is the standard HTTP port for websites to use. In the *[server.1]* section, make sure the port is set to 80 and change any other settings to suit your environment. For simple cases, the default should work out of the box.

Once you are happy with your settings, you can now restart the server via 'service kiwiirc restart' for the settings to take effect.

**Security considerations**

By default, anyone can connect to your server from any website. In most cases this will be undesirable as it opens your server up for abuse. E.g. Someone may put their own version of Kiwi IRC on a popular website that auto connects to your server causing a flood of spam.

To work around this, the sever allows you to whitelist specific websites that may connect to your server. This makes use of the browser "Origin" headers that all browsers use today.

In the config file is a section *[allowed_origins]* whereby you can list the website domain names that you want to allow to connect. You may use wild cards here. E.g. If you have a website example.com, you may want to allow *.example.com to allow all sub domains (and HTTP/HTTPS) on your website.

### The client
**client.json** is the client configuration. By default this json formatted file is loaded after the webpage has been loaded, but it may be found in a number of different ways to better integrate with your existing website. More information on this can be found [here](Configuration#loading-the-config-file).

For this quick guide we will assume that you are setting Kiwi IRC up for a single network. The example config file should get you running out of the box but you will need to change the IRC network address that you want users to connect to. Here you can also change the default nickname that users are greeted with, using a `?` character to insert a random number. Eg. "User?" will be changed to something like "User12".

*Note: While changing and testing the config file, remember to clear or disable your browsers cache so that you are getting your latest changes each time!*

More information on the settings available in this file cons be found [here](Configuration#config-options).

## Launching the web client
Once the 2 config files have been set, you should be ready to launch the client in your browser.

Since in this guide we set the server to listen on port 80, we can now go ahead and open http://yourserverip/ in our browser and watch it load with great success.

If it does not find the website, make sure your server port is not being blocked by any firewalls and that no other software was using the same port before starting the kiwi server.