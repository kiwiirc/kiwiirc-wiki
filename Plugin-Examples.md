Quick and dirty plugin examples.

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