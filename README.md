# Linux System Service Scripts for Liberty

There are two main methods: systemd unit files and traditional init.d scripts. This covers both approaches

## systemd unit file

The systemd unit file approach involves declarative .service files in `/lib/systemd/system/`.

The unit file contains some declarative blocks which define information about the service, how to control it and where to install it in the system start up sequence.
```
[Unit]
...

[Service]
...

[Install]
...
```

### Declaration & Use

Put the `liberty.service` file in /lib/systemd/system/ to define the service. Update the paths for your installation and target server.

Run `systemctl daemon-reload` - this reloads systemctl to cause it to process the various service files

Once the systemctl is reloaded you can then start, stop and query status for the liberty service:
* `systemctl start liberty`
* `systemctl status liberty`
* `systemctl stop liberty`

### Registration

You can enable the service to be started at boot:
`systemctl enable liberty`

### Customize

If you are running Liberty on slow hardware, such as a Raspberry pi, you may need to increase the timeout for the service to start: `TimeoutSec=5min`

## init.d files

init.d files are the traditional form of daemon or system service control files.

### Declaration & Use

Copy etc/init.d/liberty to /etc/init.d

You can then run start and stop:
`/etc/init.d/liberty start`
`/etc/init.d/liberty stop`


#### Deeper reading
https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sect-Managing_Services_with_systemd-Unit_Files.html

