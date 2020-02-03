Quick and dirty plugin examples.

#### Add a custom ident / username to a clients connection
~~~html
<script>
kiwi.plugin('customident', function(kiwi, log) {
    kiwi.on('network.connecting', function(event) {
        event.network.ircClient.options.username = 'custom_ident';
    });
});
</script>
~~~

#### Show the nicklist when returning to a channel from closing a query buffer
~~~html
<script>
kiwi.plugin('shownicklist', function(kiwi, log) {
    kiwi.state.$watch('ui.active_buffer', function(){
        if (kiwi.state.getActiveBuffer().isChannel()) {
            kiwi.emit('sidebar.show', 'nicklist');
        }
    });
});
</script>
~~~

#### Replace reCaptcha with a custom captcha
~~~html
<div><button @click.prevent="$emit('ready', true)">Click me</button></div>
<script>
kiwi.plugin('mycaptcha', function(kiwi, log) {
    kiwi.replaceModule('components/Captcha', {
        template: '#mycaptcha'
    });
});
</script>
~~~

#### Show IRCCloud avatars
~~~html
<div id="irccloud_avatars" style="width:1px;height:1px;position:absolute;left:-1000px;"></div>
<script>
kiwi.on('irc.userlist', function(event, network) {
    var scratch = document.querySelector('#irccloud_avatars');

    event.users.forEach(function(user) {
        var m = user.ident.match(/^uid|sid([0-9]+)$/);
        if (m) {
            var avatarUrl = 'https://static.irccloud-cdn.com/avatar-redirect/' + m[1];
            var img = document.createElement('img');
            img.src = avatarUrl;

            // irccloud replies with a 404 if an avatar doesn't exist, so this onload callback
            // will only be called for successful avatars
            img.onload = function() {
                kiwi.state.addUser(network.id, {nick: user.nick, avatar: {
                    small: avatarUrl,
                }});

                scratch.removeChild(img);
            };

            img.onerror = function() {
                scratch.removeChild(img);
            };

            scratch.appendChild(img);
        }
    });
});
</script>
~~~