---
layout: post
title:  "Improved multi-platform support in Veyon 4.1"
author: tobydox
date:   2018-02-20 07:12:31 +0100
categories: [Veyon 4.1, Platform support, Linux, Windows]
image: "/img/blog/platform-plugins.jpg"
---

[A recent change][4ddbc8a051214251e8e7a70acc947665db5fa992] in our source code repository looks small and trivial but marks the beginning of a new era for Veyon. We no longer have any platform-specific code in neither the Veyon Core library nor any of the application components. All existing platform-specific code has been refactored into the respective platform plugins for Windows and Linux. This basically means we can add support for more platforms and operating systems such as macOS, Android etc. in the future by only developing an appropriate platform plugin (and preferably also a VNC server integration plugin).

Let's have a more detailed look at the internals. Veyon itself is based on [Qt][qt], a software development framework which allows to write cross-platform applications by providing a unified API to most operating systems and platforms. In general any Qt-based application can be run on all platforms supported by Qt. However this only applies if the application solely makes use of functionalities offered by Qt. While Qt is extremely powerful and feature-rich not all kind of platform-specific functions are available and never will be. Veyon uses a couple of highly system specific functions and interfaces in order to implement advanced operations such as shutting down a computer, locking all input devices, managing system services, fetching all user groups or simply changing file permissions. A generic platform interface in the Veyon Core library provides now access to all these functions implemented within individual platform plugins.

While we now have the technical foundation to support more platforms we still need developers who deal with the actual implementation of new platform plugins for Veyon. These plugins are mostly independent of all other Veyon components so all you need is profound knowledge of the platform you are going to write the plugin for. If you are familiar with system programming especially on macOS or Android you are warmly invited to join us! Don't hesitate to tell your friends about the opportunities to support the Veyon project.

The development of the platform abstraction layer has been a lot of work. Therefore there have been less development capacities for new features visible to the end user. However we think that making Veyon available for more platforms and providing outstanding support for existing platforms is as important as the development of new features. This is why we focussed on implementing and finishing the platform abstraction layer for Veyon 4.1.

Thanks to the major refactorings the platform support especially for Linux has been improved significantly. Veyon 4.1 will come with full systemd integration so you don't have to start Veyon Server manually via XDG autostart or Xsetup/xinitrc any longer. The next blog article will have more technical details about the implementation.

[4ddbc8a051214251e8e7a70acc947665db5fa992]: https://github.com/veyon/veyon/commit/4ddbc8a051214251e8e7a70acc947665db5fa992
[qt]: https://www.qt.io/
