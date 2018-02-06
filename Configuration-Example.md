Below is a complete example of configuration that Kiwi IRC expects. More information can be found on the [[Configuration]] page.

~~~JSON
{
	"windowTitle": "Kiwi IRC - The web IRC client",
	"startupScreen": "customServer",
	"kiwiServer": "http://example.com/webirc/kiwiirc/",
	"restricted": false,
	"theme": "default",
	"themes": [
		{ "name": "Default", "url": "static/themes/default.css" }
	],
	"startupOptions" : {
		"server": "irc.freenode.net",
		"port": 6697,
		"tls": true,
		"channel": "",
		"nick": ""
	},
	"embedly": {
		"key": ""
	},
	"plugins": []
}
~~~