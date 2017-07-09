You can set default options such as the server, nick and other options directly in the URL to Kiwi IRC. This is great if you are using Kiwi IRC to a specific channel you have.

Kiwi IRC supports the standard `irc://server.com/#channel` link format to set the default IRC network and other settings. Eg. https://kiwiirc.com/nextclient/#irc://irc.freenode.net/#kiwiirc

Notice the `irc://...` comes *after* a `#` character. That is important for your browser!

## Examples
* irc.freenode.net, channel #kiwiirc

  > https://kiwiirc.com/nextclient/#irc://irc.freenode.net/#kiwiirc

* irc.freenode.net on port 7002, channel #kiwiirc

  > https://kiwiirc.com/nextclient/#irc://irc.freenode.net:7002/#kiwiirc

* irc.freenode.net on port 6697 with SSL, channel #kiwiirc

  > https://kiwiirc.com/nextclient/#irc://irc.freenode.net:+6667/#kiwiirc

* irc.freenode.net on port 6697 with SSL, multiple channels

  > https://kiwiirc.com/nextclient/#irc://irc.freenode.net:+6667/#kiwiirc,#freenode

A few notes:
* If not set, the default port is 6667. If using SSL, 6697.
* SSL can be provided by `+` before the port, or by using `ircs://` instead of `irc://`


## Options
The server and channels are not the only things you can set. You can also set extra options by adding a `?`
to the end of the URL and then adding any of the following:

* `nick=prawnsalad`

  Sets the default nickname to prawnsalad

  Tip: add a ? to insert a random number, eg. "prawnsalad?". Great for public IRC channels.
* `encoding=utf8`

  Sets the connection encoding to utf8 (default)

### Option Examples

* irc.freenode.net, channel #kiwiirc, with the nickname of prawnsalad

  https://kiwiirc.com/nextclient/#irc://irc.freenode.net/#kiwiirc?nick=prawnsalad

* irc.freenode.net, channel #kiwiirc, with the nickname of prawnsalad, encoding of utf8

  https://kiwiirc.com/nextclient/#irc://irc.freenode.net/#kiwiirc?nick=prawnsalad&encoding=utf8




## ZNC support
Running a ZNC host or just want a fancy bookmark to your own ZNC server? Then you can simply add the `type=znc` option to your Kiwi URL. This will prompt you for your ZNC password - it is not stored in the URL or browser.

https://kiwiirc.com/nextclient/#irc://znc.server.com/?type=znc&nick=username&network=networkname

If you are running an older version of ZNC that does not support multiple networks per user then set `network` to an underscore, `_`.