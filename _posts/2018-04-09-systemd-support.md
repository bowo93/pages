---
layout: post
title:  "Full systemd service support on Linux in Veyon 4.1"
author: tobydox
date:   2018-04-09 17:21:31 +0100
categories: [Veyon 4.1, systemd, Linux]
image: "/img/blog/systemd-support.jpg"
---

As you might have already read Veyon 4.1 will come with full systemd support. This means on Linux the Veyon Service can now be managed the same way as it has been possible on Windows for many years. Unlike typical Linux daemons/services such as SSH, HTTP or database servers the Veyon Service requires full access to graphical user sessions. Moreover it's recommended to run the process as a different user (usually root) in order to prevent users from killing the process to avoid control by the instructor. These requirements made things a bit complicated and required some fundamental changes in the implementation.

First of all the former Veyon Service has been split into two components: *Veyon Service* and *Veyon Server*. The Veyon Server works independently to system services and provides the actual network server and computer control implementation. It runs as a regular process like Veyon Service did before when launching without any additional arguments. You can always launch it manually or via autostart entries inside graphical user sessions on both Linux and Windows and it will serve all required functionalities. In contrast the Veyon Service has been reduced to a minimal component which monitors user sessions and manages Veyon Server instances. On Windows effectively nothing has changed while on Linux there's now a new and complete implementation for these tasks.

The Veyon Service is started by the corresponding systemd service unit and runs as a non-graphical process with root privileges. It performs session monitoring through DBus and `systemd-logind`. Whenever `systemd-logind` announces a new graphical user session the Veyon Service will start a new Veyon Server instance. A little magic is necessary to retrieve and forward the session environment. This includes environment variables such as `$DISPLAY` required by the Veyon Server to properly access the graphical environment. When a session is closed the Veyon Service gets notified by `systemd-logind` and stops the server process. The Veyon Service can also be started while a session is already open. In this case it will start the server for the existing session.

You can manage the service either via the Veyon Configurator or the command line tool. Both programs allow you to query the service status and start or stop the service. Additionally you can enable/disable autostart which will enable/disable the systemd unit for system boot. Some command line examples:

```shell
veyon-ctl service status
veyon-ctl service start
veyon-ctl config set Service/Autostart 1
```

At the command line you can also manage the service using systemd directly:

```shell
systemctl status veyon-service
systemctl start veyon-service
```

Please note that it's not recommended to enable or disable the systemd service manually. This setting will be overwritten the next time you change the configuration inside Veyon Configurator or using the command line tool as both will enforce the configured service autostart option. Instead alter the value of the `Service/Autostart` configuration key as shown above.

After updating to Veyon 4.1 make sure to enable service autostart in Veyon Configurator. Then you can remove your existing autostart entries and revert your Xsetup/xinitrc customizations. After the next reboot the Veyon Service should run regularly and launch Veyon Server for graphical user sessions. For the future we plan to extend the service by multi seat/session support which will start a dedicated server process for every session.
