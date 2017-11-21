***Note: This page needs typing up properly***

Quick and dirty overview. Select the best scenario below, and enter that startup screen name into your config.json like so: `"startupScreen": "welcome"`

### welcome screen
The welcome startup is essentially for single networks. Connecting to a single network address and supports automatically connecting if you're into that. Anything after the `#` character in the URL is entered into the channel box.

### customServer screen
For public gateways that let users connect to any IRC network. A full irc:// URI can be given after the `#` character in the URI, with multiple URIs supported by separating them with `;`.

### personal screen
The personal screen makes it act like a personal IRC client, in that it lets you connect anywhere and remembers your networks for next time you load the page.

### znc
For hosts that provide a ZNC service or just as a frontend to your self hosted ZNC instance, the znc startup screen provides a simplified username, password, and optional network box that logs into your ZNC instance.