## Overview
Kiwi IRC supports being themed by a CSS file and being changed at runtime. This gives you full access to modify colours, paddings, margins, etc. The core client layout is handled for you internally so you only need to think about the looks you want.

There are some community created themes that can be found [here](Community-Created-Themes)

## Creating a theme
A theme is a folder containing a file called `theme.css`. This may be placed anywhere on the web or in the `static/themes/` folder within Kiwi IRC. To create your own theme:

- Copy an existing theme folder from `static/themes/` and name it however you like. For example, `mytheme`.
- Edit the `mytheme/theme.css` file with your theme styles.
- Add the theme to your config file [as shown here](https://github.com/kiwiirc/kiwiirc/wiki/Configuration#themes) or share the link to others to try out.

Once these 3 steps are completed, refresh Kiwi IRC in your browser and you should now see your theme in the themes list in the settings window.

*Tip: You can click the refresh button next to the themes list to re-load your theme CSS without refreshing the page*

## Online theme builder
There is an online theme builder that lets you test out new theme ideas quickly right in your browser. You can find there here: https://kiwiirc.com/nextclient-themebuilder

## CSS tips
Kiwi IRC uses a class naming scheme very similar to BEM. Classes are named in the format `.kiwi-scope-identifier--optional-modifier`. For example, the [message list component](https://github.com/kiwiirc/kiwiirc/blob/master/src/components/MessageList.vue) contains classes such as `.kiwi-messagelist-message` and `.kiwi-messagelist-message--highlight`.

If you're unsure which CSS classes to be styling, you can use your browsers developer tools to inspect the element and view the relevant classes as you see them on the page.

## Hidden secrets
There are some hidden ways to style specific parts of the interface.
#### Styling messages from a specific user
~~~css
/* Change all of a users messages to red */
.kiwi-messagelist-message[data-nick="a_user"] {
    color: red;
    font-weight: bold;
}

/* Or add a bell icon infront of nickserv messages */
.kiwi-messagelist-message[data-nick="nickserv"] .kiwi-messagelist-body::before {
    content: "\f0f3";
    font-family: fontawesome;
    margin-right: 5px;
}
~~~

#### Styling channel or query tabs
~~~css
/* Add a help icon infront of a #help channel tab */
.kiwi-statebrowser-channel[data-name="#help"]::before {
    content: "\f128";
    font-family: fontawesome;
    margin-right: 5px;
}
~~~

#### Styling the application depending on the active channel or buffer
~~~css
/* Add a `?` background image when in a help channel */
.kiwi-wrap[data-activebuffer="#help"] .kiwi-workspace-background {
    background-image: url(big_questionmark.png);
}
~~~