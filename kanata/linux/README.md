# Linux

## Changes from Video

Some linux users will encounter issues by just using the `tap-hold` behavior by itself.

This has been resolved with #7 which is the [recommended workaround from the kanata documentation](https://github.com/jtroo/kanata/blob/main/docs/config.adoc#tap-hold).


## Systemd daemon process

Add this to: `~/.config/systemd/user/kanata.service`:

```
[Unit]
Description=Kanata keyboard remapper
Documentation=https://github.com/jtroo/kanata

[Service]
Environment=PATH=/usr/local/bin:/usr/local/sbin:/usr/bin:/bin:%h/.cargo/bin
Environment=DISPLAY=:0
Type=simple
ExecStart=/usr/bin/sh -c 'exec $$(which kanata) --cfg $${HOME}/.config/kanata/config.kbd'
Restart=no

[Install]
WantedBy=default.target
```

Then run

```
systemctl --user daemon-reload
systemctl --user enable kanata.service
systemctl --user start kanata.service
systemctl --user status kanata.service   # check whether the service is running
```

For more information use the following install guide found at:

https://github.com/jtroo/kanata/blob/main/docs/setup-linux.md
