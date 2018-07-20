---
layout: post
title:  "Veyon 4.1 released"
author: tobydox
date:   2018-07-20 11:11:24 +0200
categories: [Veyon 4.1, release]
published: false
image: "/img/blog/veyon-4-1.jpg"
---

About 10 months after we launched Veyon 4.0.0 we're happy to announce Veyon 4.1.0. The new 4.1.x release series brings major improvements and changes, especially regarding platform integration and administration. We already blogged about the most notable ones in previous articles but of course we want to give you a summary of highlights you'll find in this new release:

* In Veyon Master you'll find new buttons at the bottom toolbar. You can hide powered off computers by toggling the button with the power switch icon next to the search bar. The new computer alignment control buttons on the right side allow to [customize the arrangement of computer thumbnails]({{ site.baseurl }}{% post_url 2018-05-16-arrange-computer-thumbnails %}) via drag and drop.

* Programs and websites can be predefined for the features *Run program* and *Open website*. The user can simply choose the program or website from a menu so it's not necessary to enter the information manually everytime.

* Appearence and behaviour of Veyon Master is more customizable. Both background color and the computer thumbnail caption can be changed. Also the refresh interval for thumbnails is configurable. At the same time we improved network connection timeouts leading to much faster detection of computers being on- or offline. Additionally remote control is more responsive now, especially on Linux.

* Veyon administrators who are based in the Linux world will be happy about [the newly introduced systemd support]({{ site.baseurl }}{% post_url 2018-04-09-systemd-support %}). The Veyon Service can be managed the same way on Linux as on Windows and there's no need to manually edit or create start files any longer.

* The [management of authentication keys]({{ site.baseurl }}{% post_url 2018-02-13-introducing-authkeys %}) is now much more easy and flexible. We replaced the old assistant with dedicated buttons for individual actions such as creating, removing, exporting and importing authentication keys. You can even let Veyon handle the key file permissions by simply assigning an user group whose members shall be allowed to access the key files.

* More administrative tasks can be performed using Veyon Control, our command line interface. There are three new CLI modules in total. The new `shell` module allows to enter commands interactively so it's not necessary to type `veyon-ctl` every time. It also can be used for running a list of commands from a file (batch mode). The builtin room and computer directory [can be managed at the command line]({{ site.baseurl }}{% post_url 2018-04-24-network-object-management-cli %}) using the new `networkobjects` module. You'll find this handy if you want to import or export CSV files and other types of simple structured text files. Authentication keys can be created, removed, assigned, imported or exported easily thanks to the new `authkeys` module.

* We finalized our [plugin-based platform abstraction concept]({{ site.baseurl }}{% post_url 2018-02-20-platform-abstraction %}). Even though this does not visibly affect end users it improves the overall code quality and thus stability and reliability of the whole software. Last but not least we can add support for other operating systems and platforms in the future more easily.

* The LDAP/AD plugin now supports encrypted connections via TLS or SSL. Additionally we changed the format for object filters to match well-known standards: `(foo=bar)` instead of `foo=bar`. When performing an upgrade from Veyon 4.0 to Veyon 4.1 all configured filters will be updated automatically when saving the configuration.

* All passwords are now stored encrypted in the configuration. This concerns the LDAP/AD bind passwords as well as VNC server passwords. Passwords will be automatically encrypted once the configuration is saved after an upgrade.

* The configuration of the authentication method has been simplified to only allow one method at a time. Access control uses computers and rooms from the globally configured network object directory while the user groups backend can be changed independently.

* Overall security has been improved by enabling appropriate hardening techniques and reworking code sequences with potential buffer overflows.

In order to implement the new features we had to change some details in the network protocol making Veyon 4.1 incompatible with Veyon 4.0. This means you'll have to update all computers in order to use Veyon 4.1. All Veyon 4.1 downloads are available at our [download page][download-page].

[download-page]: https://veyon.io/download/

