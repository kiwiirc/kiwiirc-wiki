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