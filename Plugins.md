*Note: This is a living and breathing document. It is still changing and being completed*

This document briefly outlines how to create, register and make use of plugins. Some small plugin examples can be found on the [[Plugin-Examples]] page for a faster look.

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
    kiwi.on('network.new', function(event) {
        event.network.connection.server = 'irc.freenode.net';
        event.network.connection.port = 6667;
    });
});
~~~

## API

### window.kiwi.*
The main API interface

| Property | Description |
| --- | --- |
| `.version` | The Kiwi IRC version |
| `.Vue` | A Vuejs global instance |
| `.themes` | Theme manager |
| `.state` | The Kiwi internal application state. Described below |
| `plugin(pluginName, fn)` | Create a new plugin |
| `addUi(type, element)` | Extend the Kiwi UI |
| `addTab(name, component, props)` | Add a custom tab to a section of the UI |
| `addView(name, component, props)` | Add a custom view (page) |
| `showView(name)` | Show a view added via addView() |
| `addStartup(name, ctor)` | Add a new startup screen |
| `showInSidebar(component)` | Show a view in the sidebar |
| `replaceModule(module, new_module)` | Replace an module or component |
| `require(module)` | Get a Kiwi internal module instance |
| `on(eventName, fn)` | Listen for an application event |
| `once(eventName, fn)` | Listen for an application event one time only |
| `off(eventName, fn)` | Stop listening for an application event |
| `emit(eventName, arg1, arg2)` | Emit an event on the application event bus |



### window.kiwi.state.*
The Kiwi internal application state. The entire application uses this interface to modify state such as adding or removing networks, adding buffers / messages / users, getting the active network or buffer.

~~~javascript
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


### Event bus
This is the main event bus for the application. Events are emitted by many places and some allow you to emit your own so that you can interact with Kiwi.

These events can be listened for via `kiwi.on('event.name', function() {})`. For events marked that they can be fired from plugins, you can do so via `kiwi.emit('event.name', arg1, arg2)`.

| Name | Arguments | Can be fired from plugins | Description |
| --- | --- | --- | --- |
| `ready` | | no | Kiwi has loaded and ready to show the startup screen |
| `document.clicked` | MouseEvent | no | The page has its `click` event triggered |
| `document.keydown` | KeyboardEvent | no | The page has its `keydown` event triggered |
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
| `irc.raw` | command, event, network | no | Raw IRC message from the IRC server |
| `irc.raw.[command]` | command, event, network | no | A raw IRC message from the IRC server |
| `irc.[command]` | event, network, ircEventObj | no | A parsed IRC event from the IRC library |
| `network.new` | eventObj | no | A new network has been added |
| `network.removed` | eventObj | no | A network has been deleted |
| `network.connecting` | eventObj | no | A network connection is about to start |
| `buffer.new` | eventObj | no | A new buffer has been added |
| `buffer.close` | eventObj | no | A buffer has been closed |
| `server.tab.show` | tabName | yes | When a server buffer is open, show the given tab |
| `theme.change` | | yes | Notify the application that the theme has been changed |
| `message.render` | eventObj | no | A message is about to be rendered |
