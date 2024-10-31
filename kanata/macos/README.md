# Kanata

This directory contains the kanata configuration for macOS, as well as a 
launchctl configuration to enable this to run as a LaunchAgent or LaunchDaemon.

To do so, make some modifications to the launch configuration or create your
own named `com.example.kanata.plist`

You'll need to replace the label string and the path to kanata and the config depeneding on your own system configuration.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.kanata</string>

    <key>ProgramArguments</key>
    <array>
        <string>{{ path to kanata }}</string>
        <string>-c</string>
        <string>{{ path to config }}</string>
    </array>

    <key>RunAtLoad</key>
    <true/>

    <key>KeepAlive</key>
    <true/>

    <key>StandardOutPath</key>
    <string>/Library/Logs/Kanata/kanata.out.log</string>

    <key>StandardErrorPath</key>
    <string>/Library/Logs/Kanata/kanata.err.log</string>
</dict>
</plist>
```

Then, copy this file to your LaunchDaemon folder.


```
sudo cp ./com.example.kanata.plist /Library/LaunchDaemons/
```

Once copied over, you can then load it using sudo 

```
sudo launchctl load /Library/LaunchDaemons/com.example.kanata.plist
sudo launchctl start com.example.kanata
```

Now, kanata should be running whenever your macbook starts up!

If you use multiple keyboards, you may want to limit this to only showing up on your MacBooks internal keyboard.
