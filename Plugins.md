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

As a very simple example, this plugin will listen for nay new networks being created and set the default server address to `irc.freenode.net`:

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