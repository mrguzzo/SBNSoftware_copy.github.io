---
layout: page
title: VPN
---



Virtual Private Network (VPN) to Fermilab
====================================================================================================

Fermilab requires a token, either soft or hard. A hard token is a physical device. A soft token is very similar to two-factor authentication. Depending on your use case, you may opt for either but keep in mind a soft token will be easier to obtain. Instructions on how to initiate the process are below.

You need to get a token by opening a ticket [RSA Token Request
    form](https://fermi.servicenowservices.com/wp?id=evg_sc_cat_item&sys_id=99aecde66f172500c7743acf1e3ee401)
    (takes a while and both hard and soft tokens are limited).

If you are requesting a soft token, you need to set up a PIN and download an app. For information on how to do that, see this page and the links contained there: [Instructions](https://fermi.servicenowservices.com/kb_view.do?sysparm_article=KB0013361)

IMPORTANT NOTE: At the same time you are requesting the token, you should request to be added to the "VPN group" -- this is necessary to be able to log into the VPN once you have the token and software ("client"). To do this you may need to submit a generic request ticket to Service Desk. This is accomplished via [this ticket](https://fermi.servicenowservices.com/wp?id=evg_sc_cat_item&sys_id=69cd40d76fddd2005232ce026e3ee41e) (or from Service Now home page, going to "Request Something" then "Request Service").

------------------------------------------------------------------------

-   **Table of contents**
-   [Virtual Private Network (VPN) to
    Fermilab]
    -   [Cisco client installation]
        -   [Additional setup for Linux]
    -   [Free client installation]
        -   [OpenConnect for OSX]
        -   [OpenConnect for Linux]
        -   [OpenConnect for iOS (Apple
            mobile)]
        -   [OpenConnect for Android]
    -   [Log in the VPN]
        -   [Cisco AnyConnect]
        -   [OpenConnect (command line
            interface)]

Some resources can be accessed only from within Fermilab network. For
some, the access outside Fermilab network is still allowed but
crippled.\
To allow users to access these resources in full by connecting via a
Virtual Private Network (VPN), which needs to be set up on the client
node.

A quite understandable description of the system is documented in [CD
DocDB
3435](http://cd-docdb.fnal.gov/cgi-bin/ShowDocument?docid=3435)
.\
As stated in there, Fermilab has chosen Cisco \"AnyConnect\", which
provides a
[client](http://www.cisco.com/c/en/us/support/security/anyconnect-secure-mobility-client/tsd-products-support-series-home.html)
to connect to its VPN.\
Cisco provides also a client to \"enter\" the VPN. There is also a free
alternative.



Cisco client installation
----------------------------------------------------------------------

The [official Cisco AnyConnect
client](http://www.cisco.com/c/en/us/support/security/anyconnect-secure-mobility-client/tsd-products-support-series-home.html)
is supported for Linux, OSX and Windows.

That software is only available via Fermilab: visit
<https://vpn.fnal.gov> and log in with your Services account credential
(just the user name, without `@services.fnal.gov`). The web site will
guide you to install the software.

Once installed, you can start the client interface and fill in the
information in the table below.



### Additional setup for Linux

The web site will just download a \"script\" `vpnsetup.sh`. That is not
just the script (it contains the binary data of the package itself).\
To install that, run

    sudo sh vpnsetup.sh

or similar. In short: you need administrator privileges.\
The script will also install SysV scripts to start and stop the VPN. It
will also try to set it to start automatically (this failed on Gentoo
Linux).\
If your system uses systemd instead, it may still work\... or not (this
too failed on Gentoo Linux).\
When the sequence of failures is long enough, you are ready to give a
try to the free client.



Free client installation
--------------------------------------------------------------------

The
[free](https://www.gnu.org/licenses/oldsy-licenses/lgpl-2.1.html)
client [OpenConnect](http://www.infradead.org/openconnect) is
available for Linux, Windows, OSX, Android and many others.



### OpenConnect for OSX

Under OSX, OpenConnect is also via homebrew:

    brew install openconnect

It is also possible to install the AnyConnect app from the AppStore, originally developed for iPad but has been tested and works on Mac OS Sonoma 14.1.


### OpenConnect for Linux

To do (need it? please [ask](mailto:petrillo@fnal.gov)).

Chances are that your distribution has it prepackaged for you.



### OpenConnect for iOS (Apple mobile -- mobile app also works on Mac OSX)

The idea is that the AppStore offers an [official
client](https://itunes.apple.com/us/app/cisco-anyconnect/id1135064690?mt=8)
based on AnyConnect 4.6^[1]^.\
A [video from Northern Arizona
University](https://mediaspace.nau.edu/media/How+to+Connect+to+Cisco+AnyConnect+VPN+on+an+iOS+Device/0_wmaarq43)
may help through the next steps, using the information above.
Considering the experience with the OSX version of a similar software,
it is possible that the user name is required in the full format,
`user@services.fnal.gov`.

[Report your luck with it if you try it!](mailto:petrillo@fnal.gov)

### OpenConnect for Android

OpenConnect binary distribution is available via
[F-Droid](https://f-droid.org/repository/browse) .



Log in the VPN
------------------------------------------------

To start using the VPN, a login must be performed. The VPN \"split\"
mode will make sure that only the traffic to Fermilab network goes
through the VPN.\
The credentials for log in are:

  ------------ ----------------------------------------------------------------------
  Server:      `vpn.fnal.gov`
  User name:   plain user name (no `@fnal.gov`, `@services.fnal.gov` or such)
  Password:    Services password (same as for e-mail access, ServiceNow and others)
  ------------ ----------------------------------------------------------------------



### Cisco AnyConnect

Under OSX, a graphic user interface called \"Cisco AnyConnect Secure
Mobility Client\" will allow you to enter the information above.\
The user name might be required in its full glory:
`user@services.fnal.gov`.


### OpenConnect (command line interface)

The simplest command to start is:

    sudo openconnect --user=<USERNAME> vpn.fnal.gov

or equivalent. Superuser privileges are likely necessary to mess with
the network configuration.\
The `--user` argument, optional, is the one like in the table above. If
not specified, it will be asked interactively.\
Remember that if you use that command, the first password request comes
from `sudo` to gain administrator privileges on your own machine.\
Then, the VPN access password is requested (as in the table above).

The shell is occupied by `openconnect`, unless the `--background` option
is specified. If not, to disconnect it is enough to hit `<Ctrl>+<C>`.

Chances are that your Linux operating system is distributing convenience
scripts to manage the VPN\... check the standard places (e.g. something
in `/etc/init.d` for Debian, `service` for RedHat, `rc-service` for
Gentoo, \...).
