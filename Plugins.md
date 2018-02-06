*Note: Plugins are currently experimental and may change at any point!*

This document briefly outlines how to create, register and make use of plugins. Further in depth descriptions will be included once the API has been officially implemented.

## Creating a plugin
A plugin is a single myplugin.js file that can be loaded over HTTP from any location.

Adding the following into your config.json file will instruct Kiwi IRC to load the .js URL into the page just before Kiwi is ready to show its UI.
~~~
"plugins": [
    {"name": "myplugin", "url": "/static/plugins/myplugin.js"}
]
~~~

Inside your .js file, you must register a plugin using the `kiwi.plugin()` call, such as:
~~~javascript
kiwi.plugin('plugin_name', function(kiwi, log) {
    // Plugin code here
});
~~~

Your plugin function will be called once Kiwi IRC has been loaded and ready to start. You can listen for events and use any of the below API in your plugin.

As a very simple example, this plugin will listen for any new networks being created and set the default server address to `irc.freenode.net`:

~~~javascript
kiwi.plugin('plugin_name', function(kiwi) {
    kiwi.state.$on('network.new', function(event) {
        event.network.connection.server = 'irc.freenode.net';
        event.network.connection.port = 6667;
    });
});
~~~

## API

### window.kiwi.*
~~~javascript
.Vue
.themes
plugin(pluginName, fn)
addUi(type, element)
addTab(name, component, props)
showTab(name)
addStartup(name, ctor)
~~~


### window.kiwi.state.*
~~~javascript
$on(eventName, fn)
$once(eventName, fn)
$off(eventName, fn)
$emit(eventName, arg1, arg2)

exportState(includeBuffers)
importState(stateStr)
resetState()

setting(name, val)
getSetting(name)
setSetting(name, newVal)

getActiveNetwork()
getNetwork(networkid)
getNetworkFromAddress(netAddr)
addNetwork(name, nick, serverInfo)
removeNetwork(networkid)

getActiveBuffer()
setActiveBuffer(networkid, bufferName)
openLastActiveBuffer()
updateBufferLastRead(networkid, bufferName)
getOrAddBufferByName(networkid, bufferName)
getBufferByName(networkid, bufferName)
addBuffer(networkid, bufferName)
removeBuffer(buffer)

addMessage(buffer, message)
getMessages(buffer)

getUser(networkid, nick, usersArr_)
usersTransaction(networkid, fn)
addUser(networkid, user, usersArr_)
removeUser(networkid, user)
addMultipleUsersToBuffer(buffer, newUsers)
addUserToBuffer(buffer, user, modes)
removeUserFromBuffer(buffer, nick)
getBuffersWithUser(networkid, nick)
changeUserNick(networkid, oldNick, newNick)

getStartups()
~~~


### kiwi.state events
These events can be listened for via `kiwi.state.$on('event.name', function() {})`. For events marked that they can be fired from plugins, you may do so via `kiwi.state.$emit('event.name', arg1, arg2)`.

| Event name | Event arguments | Can be fired from plugins | Description
| --- | --- | --- | --- |
| `document.clicked` | mouseEvent | no | The page has its `click` event triggered |
| `document.keydown` | mouseEvent | no | The page has its `keydown` event triggered |
| `active.component` | VueComponent | yes | Set the active component in the main view |
| `statebrowser.toggle` | | yes | Hide / Show the state browser |
| `statebrowser.hide` | | yes | Hide the state browser |
| `statebrowser.show` | | yes | Show the state browser |
| `sidebar.toggle` | | yes | Hide / Show the sidebar |
| `sidebar.hide` | | yes | Hide the sidebar |
| `sidebar.show` | | yes | Show the sidebar |
| `network.settings` | network | yes | Show the settings for the given network |
| `input.raw` | rawText | yes | Simulate user input |
| `input.command.[command]` | event, command, params | no | An input command is being executed |
| `mediaviewer.hide` | | yes | Hide the media viewer |
| `mediaviewer.show` | url | yes | Open the media viewer with the given URL |
| `mediaviewer.opened` | | no | Media viewer has been opened |
| `userbox.show` | user | yes | Open the user information panel for the given user |
| `irc:raw` | command, event, network | no | Raw IRC line from the IRC server |
| `irc:[command]` | event, network, ircEventObj | no | A parsed IRC message from the IRC server |
| `network.new` | eventObj | no | A new network has been added |
| `network.removed` | eventObj | no | A network has been deleted |
| `network.connecting` | eventObj | no | A network connection is about to start |
| `buffer.new` | eventObj | no | A new buffer has been added |
| `buffer.close` | eventObj | no | A buffer has been closed |
| `server.tab.show` | tabName | yes | When a server buffer is open, show the given tab |
| `theme.change` | | yes | Notify the application that the theme has been changed |
