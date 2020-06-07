Installing from the pre-built packages provide a stable and known version of the web client. Using the master branch will include the latest features but may not be as stable - use at your own risk.

This guide will explain updating the Kiwi IRC frontend client only.

*Note: Choose a location for your new Kiwi IRC client. This guide will use `/var/www/kiwiirc/`*

1. Download the latest Kiwi IRC client

   Either download and build from git, or download a pre-built version from [here](https://builds.kiwiirc.com/zips/kiwiirc_master.zip).
   Copy the new client (the folder containing the index.html file) to `/var/www/kiwiirc`.

2. Transfer your existing Kiwi IRC config files

   The new client files will have a clean config file so you must copy your existing files to keep your configuration. Copy `/etc/kiwiirc/client.json` to `/var/www/kiwiirc/static/config.json`. If you have any custom plugin or themes be sure to copy these over too.

   For any future changes to your config file, you must edit `/var/www/kiwiirc/static/config.json` and not `/etc/kiwiirc/client.json`.

3. Reconfigure the server webroot

   Edit `/etc/kiwiirc/config.conf` and change the `webroot` option to `/var/www/kiwiirc/`.
   Restart Kiwi IRC, usually with `systemctl restart kiwiirc`.
