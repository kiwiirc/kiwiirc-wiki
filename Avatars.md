Kiwi IRC supports showing avatars from existing services such as your wordpress or custom website with existing user profiles. Because there are so many different implementations and avatar services you will need to implement a plugin that generates an avatar URL for each user. An image upload plugin may be beneficial to upload avatars to your website also.

As a starting point, you may use this example plugin and change it to suit your needs. You will need to generate a URL based on the username, nick, and optional account name if they are logged in.

~~~javascript
kiwi.plugin('custom-avatars', function(kiwi, log) {
    kiwi.on('irc.userlist', function(event, network) {
        event.users.forEach(function(user) {
            var username = user.ident;
            var nick = user.nick;
            var account = user.account;

            kiwi.state.addUser(network.id, {nick: nick, avatar: {
                small: 'https://example.com/avatars/' + username + '.jpg',
            }});
        });
    });

    kiwi.on('irc.join', function(event, network) {
        var username = event.ident;
        var nick = event.nick;
        var account = event.account;

        kiwi.state.addUser(network.id, {nick: nick, avatar: {
            small: 'https://example.com/avatars/' + username + '.jpg',
        }});
    });
});
~~~