The client configuration is a JSON object loaded before Kiwi IRC starts. If a config cannot be found or an error loading it occurs, an error message will be displayed on the page and the client will not start.

## Loading the config file

A config can be loaded from a number of places depending on which best suits your environment. If you have an existing website in PHP, Ruby, NodeJS, Java, or any other dynamic language, you can even generate the config on the fly to better integrate the client into your website.

The following locations are checked in order.

### Use a javascript function
The javascript function `window.kiwiConfig` is checked before anything else. If it exists, it will be called and the return value should be the config object - exactly the same as the config.json structure.

### Specify a URL location
You can specify the URL to your JSON config file in a meta tag named `kiwiconfig` on the client page (index.html). Example: `<meta name="kiwiconfig" content="http://example.com/path/to/config.json">`

### JSON string directly in the page
If generating the JSON config yourself then you can include it directly into the client page (index.html) in a script tag named `kiwiconfig`. As an added bonus this will save a HTTP request making it faster to load.
Example:
~~~html
<script name="kiwiconfig">
{"startupScreen": "customServer", "startupOptions": { "server": "irc.freenode.net", "port": 6697, "tls": true, "direct": false, "nick": "" }}
</script>
~~~

### Plain config.json
Loads the JSON file from `static/config.json`


## Config format

Config options are in JSON format using a plain object. Example: `{"option1": "value", "option2": true}`.

You may either use nested JSON objects or simple dotted notation. These two config files are equivalent:
~~~json
{
    "startupOptions": {
        "server": "irc.example.com"
    }
}
~~~
~~~json
{
    "startupOptions.server": "irc.example.com"
}
~~~

#### Dotted notation

Dotted notation is parsed **after** the config is loaded. This makes it easy for configurations that are generated on the fly and overwrite a default configuration.

This means that this:
~~~json
{
    "startupOptions": {
        "server": "irc.example.com"
    },
    "startupOptions.server": "irc.otherserver.com"
}
~~~
ends up being this:
~~~json
{
    "startupOptions": {
        "server": "irc.otherserver.com"
    }
}
~~~

## Misc config options

A full listing of config options can be found [[here|Configuration-Options]]

##### `windowTitle`
Example: "My IRC network"

The title of the webpage. This appears in the browser tab and bookmark managers when bookmarked.

##### `startupScreen`
Example: "customServer"

The screen that is first shown. More information on this can be found [[here|startup-screens]]

##### `kiwiServer`
Example: "http://example.com/config.json"

The URL to your kiwi server. More information on this can be found [[here|kiwi-server]]

##### `restricted`
Example: `true` or `false`

If set to `true`, Kiwi IRC will only be allowed to connect to the network that you specify.

##### `themes`
The themes listed here will be available in the client. There must be at least one theme here. The URL should only point to the folder of your theme that contains your `theme.css` file.
Example:
~~~json
[
  { "name": "Default", "url": "static/themes/default/" },
  { "name": "Theme2", "url": "static/themes/theme2/" },
  { "name": "Other Theme", "url": "http://example.com/kiwi_theme/" }
]
~~~

If you add a theme named `custom`, this will allow the user to temporarily set their own theme URL. Handy for designers and trying out different themes.

##### `theme`
Example: "default"

The name of the default theme to use. This name must be in the available themes list.

##### `embedly.key`
Example: "embedly API key"

Kiwi IRC uses the embedly service to show a preview of links directly within the client. If you have an embedly API key to custom the previews or remove its branding, you can enter your API key here.

##### `startupOptions`
Object / configuration for the first screen of the client. Eg. the connection screen

##### `startupOptions.server`
Example: "irc.freenode.net"

This will be the default IRC server the client will connect to. May be left empty to force the user to enter a server.

##### `startupOptions.port`
Example: 6667

This will be the default port for the IRC server the client will connect to. By default it uses 6667, or 6697 if using SSL/TLS.

##### `startupOptions.tls`
Example: `true` or `false`

If set to `true`, Kiwi IRC will enable SSL/TLS by default for the IRC server connection. If set to `false`, an un-secure plain-text connection will be used.

##### `startupOptions.password`
Example: "mypassword"

This is the password sent to the IRC server using `PASS`.

##### `startupOptions.direct`
Example: `true` or `false`

Kiwi IRC supports connecting directly to IRC servers that support websockets. Setting this to `true` will connect directly instead of using a Kiwi server. (Note: this may be more unstable depending on the users browser, network, anti virus, proxies, amongst other situations)


##### `startupOptions.channel`
Example: "#channel,#channel2"

This will be the default channel that the client will automatically join.


##### `startupOptions.nick`
Example: "a_nick"

This will be the default nick that the client will use. A `?` character may be used to specify a random number to help reduce conflicting nicks.


##### `startupOptions.autoConnect`
Example: `true` or `false`

If using the `welcome` startup screen, this will tell the client to automatically connect with the connection settings you have given.


##### `startupOptions.state_key`
Example: "kiwi-state"

The state key is the name for the user session. The default is "kiwi-state". Users IRC connections and channels will be remembered in their browser for the next time they open the webpage. If set to an empty string (`""`) then nothing will be remembered.


##### `startupOptions.remember_buffers`
Example: `true` or `false`

When the user session is saved via `startupOptions.state_key` only the user settings are saved. Set this option to true to also save the users networks and channels.


##### `startupOptions.greetingText`
Example: "Hello!"

The header that is shown on the startup page. HTML may also be used here.


##### `startupOptions.buttonText`
Example: "Start"

The text that is shown on the connect button on the startup page. HTML may also be used here.


##### `startupOptions.infoContent`
Example: `"Welcome to my network! Please visit my <a href='/home' target='_blank'>homepage</a> for help."`

The HTML content that is shown on the right side of the startup page.


##### `startupOptions.infoBackground`
Example: "/info_background.jpg"

The background image for the right side of the startup page.