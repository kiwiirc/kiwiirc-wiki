## Overview
Kiwi IRC supports being themed by a CSS file and being changed at runtime. This gives you full access to modify colours, paddings, margins, etc. The core client layout is handled for you internally so you only need to think about the looks you want.

## Creating a theme
A theme is a folder named as your theme name, containing a file called `theme.css`. This may be placed anywhere on the web or in the `static/themes/` folder within Kiwi IRC. To create your own theme:

- Copy an existing theme folder from `static/themes/` and name it however you like. For example, `mytheme`.
- Edit the `mytheme/theme.css` file with your theme styles.
- Add the theme to your config file [as shown here](https://github.com/kiwiirc/kiwiirc/wiki/Configuration#themes)

Once these 2 steps are completed, refresh Kiwi IRC in your browser and you should now see your theme in the themes list in the settings window.

*Tip: You can click the refresh button next to the themes list to re-load your theme CSS without refreshing the page*

## CSS tips
Kiwi IRC uses a class naming scheme very similar to BEM. Classes are named in the format `.kiwi-scope-identifier--optional-modifier`. For example, the [message list component](https://github.com/kiwiirc/kiwiirc/blob/master/src/components/MessageList.vue) contains classes such as `.kiwi-messagelist-message` and `.kiwi-messagelist-message--highlight`.

If you're unsure which CSS classes to be styling, you can use your browsers developer tools to inspect the element and view the relevant classes as you see them on the page.