---
layout: post
title:  "Introducing upcoming authentication key management"
author: tobias.junghans
date:   2018-02-13 08:02:30 +0100
image: "/img/keys.jpg"
---

In this blog post I want to introduce the *authkeys* plugin which will be part of Veyon 4.1.x. This plugin implements new mechanisms for managing authentication keys and replaces the assistant found in Veyon 4.0.x and previous products. The *authkeys* plugin provides both a graphical configuration page for the Veyon Configurator as well as a command line interface implementation for `veyon-ctl`. Both interfaces aim for full feature parity which means you can perform the same tasks via Veyon Configurator as well as the command line.

The following screenshot shows the configuration page for authentication keys:

![authkeys configuration page](/img/authkeys-configurator.png){: .blog-post-image-fluid }

The command line interface version provides the same functionalities as well as a similar visual appearance:

![authkeys command line interface](/img/authkeys-cli.png){: .blog-post-image-fluid }

As you can see we have focussed on simple operations which can be performed (and automated!) individually at any time. No need to walk through the assistant without the possibility to e.g. only export a previously created key pair. Instead keys can be exported or imported with just one click or one CLI command. Public and private keys are listed separately so they can be managed independently of each other. The key pair ID represents a hash which is identical for a public and a private key belonging together. By comparing the key pair ID you can identify mismatches easily e.g. after importing old keys or keys with a wrong name.

Why did we add this new management interfaces except for convenience? Until now you could only create keys for pre-defined user roles such as teachers, administrators or support team members. With Veyon 4.1.x you'll be able to create arbitrary key pairs and assign them to user groups. The latter task is now builtin and file permissions do not have to be adjusted manually any longer. With the help of the "set access group" function file owners and access permissions can be adjusted automatically. Upon start Veyon Master looks for accessible private keys so the key to be used does not have to be specified explicitely (which however is also possible through the environment variable `VEYON_AUTH_KEY_NAME`).

So how big will be the impact when updating Veyon? Due to the removal of fixed key roles we had to change the network protocol which means both client and masters will have to run Veyon 4.1.x and can't be mixed with old versions. However the update itself won't be a big deal as you can simply continue to use your existing authentication keys. You can possibly simplify or replace your mechanisms for deploying the authentication keys by using the appropriate CLI operations.

The next article will be about the improved platform abstraction and integration in Veyon 4.1.x, especially on Linux (full systemd support!).
