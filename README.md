squeezebox-googlemusic
======================

This is an attempt to re-start development of the googlemusic plugin for squeezebox. hectus' excellent plugin has some problems with the latest API, and appears to have ceased development, so I've forked it into this organisation. 

At this point, I'm only really working on this if it's broken on my home installation. If anyone would like to contribute or lead this, please let me know - I won't have heaps of time, but I figure that if we have a number of people partially active, and a single starting point, then we might keep this thing rolling.

This is a [Squeezebox](http://www.mysqueezebox.com/) (Logitech Media
Server) Plug-in for playing music from your [Google Play
Music](https://play.google.com/music/) library and All Access. It is
based on the Python [Unofficial Google Play Music
API](http://unofficial-google-music-api.readthedocs.org/) and the
ability of inlining Python in Perl programs.

Dev Resources
-------------

* http://forums.slimdevices.com/showthread.php?98526-Google-Music-Plugin
* https://github.com/hechtus/squeezebox-googlemusic/issues

Development setup (Deb-based Linux)
-------------------------
*First install the required libraries*
```
sudo pip2 install gmusicapi==10.0.1  #depening on your installed python version, you might have to use pip
sudo apt-get install python-dev
sudo cpan App::cpanminus
sudo cpanm --notest Inline
sudo cpanm --notest Inline::Python
```
*then configure permissions and clone the repo*
```
sudo addgroup squeezeboxserver
sudo adduser YOURUSERNAME squeezeboxserver
# Now log out and log back in again, or do something like `sudo su YOURUSEFNAME`
cd /var/lib/squeezeboxserver/Plugins
sudo mkdir GoogleMusic
sudo chgrp squeezeboxserver GoogleMusic
sudo chmod g+wx GoogleMusic
cd GoogleMusic
git clone https://github.com/squeezebox-googlemusic/squeezebox-googlemusic.git .  #don't forget the dot at the end
sudo service logitechmediaserver restart
```


Installation
------------

This installation procedure will only work on Linux based systems. At
the moment I do not know if this will ever work on Windows. If you
want to install this plugin on OSX have a look at the How-To
below. Please let me know if you found a way to get this plugin
running on non-Linux systems to extend this How-to.

1. You will need a Google account and some music and/or playlists in
   your library. If you want to use Google Music All Access features
   you will need a subscription to this service.

1. Install Python and [Python pip](http://www.pip-installer.org).

1. Install the [Unofficial Google Play Music
   API](https://github.com/simon-weber/Unofficial-Google-Music-API>)
   by running:

         sudo pip install gmusicapi==10.0.1

1. To be able to build the Perl package Inline::Python (see below) you
   will need the Python developer package. The name of the package and
   the way how to install it depends on your Linux distribution. On
   **Debian** based systems you will have to do:

         sudo apt-get install python-dev

   On **redhat** systems do:

         sudo yum install python-devel

1. Install the Perl CPAN package
   [Inline](http://search.cpan.org/~ingy/Inline/) and
   [Inline::Python](http://search.cpan.org/~nine/Inline-Python/) by
   running:

         sudo cpan App::cpanminus
         sudo cpanm --notest Inline
         sudo cpanm --notest Inline::Python
         sudo cpanm --notest IO::Socket::SSL

1. To install the plugin, add the repository URL
   https://squeezebox-googlemusic.github.io/squeezebox-googlemusic/repository/repo.xml
   to your squeezebox plugin settings page.

Installation on OSX
-------------------

The installation on OSX is quite similar to Linux. According to the
reports for issue #28 you will have to do the following:

1. Open Terminal by typing ```Terminal``` in Spotlight. A command line
   interface should open.
1. Install pip. To do that, type
   sudo easy_install pip
   Note: for this to work you need to have XCode (the Mac developer
   tools) installed, you will also need the Xcode command line tools,
   but XCode will prompt you to install them if you don't.
   Then go to step 5 below. 

1. Alternatively, if you don't have and don't want to install XCode
   you can also download the ```get-pip.py``` script from here:
   https://raw.github.com/pypa/pip/master/contrib/get-pip.py
   But please be aware that you are doing this at your own risk. You
   are installing a binary through a script downloaded from the internet
   without any verification...

1. Change to the ```Downloads``` directory

   		  cd Downloads

1. Install the [Unofficial Google Play Music
   API](https://github.com/simon-weber/Unofficial-Google-Music-API>)
   by running:

         sudo pip install gmusicapi
         
   **Important Note**: At the moment you will need the developer
     version of gmusicapi. Install this version by doing:

         sudo pip install git+https://github.com/simon-weber/Unofficial-Google-Music-API.git@develop

1. Install the Perl CPAN package
   [Inline](http://search.cpan.org/~ingy/Inline/) and
   [Inline::Python](http://search.cpan.org/~nine/Inline-Python/) by
   running:

         sudo cpan App::cpanminus
         sudo ARCHFLAGS="-arch i386 -arch x86_64" cpanm --notest Inline
         sudo ARCHFLAGS="-arch i386 -arch x86_64" cpanm --notest Inline::Python

1. Go to the Logitech Media Server with your browser. Visit the
   Plugins page and insert the repository URL for this Plugin at the
   bottom of the page:
   http://squeezebox-googlemusic.github.io/squeezebox-googlemusic/repository/repo.xml

1. Save and restart the Logitech Media Server. Provide your All Access
   information on the settings page.

1. Enjoy!

Thanks to @jamesray2 for this How-To.

Usage
-----

1. Go to the plug-in settings page and set your Google username and
   password for the Google Music plug-in. You can also use an
   application-specific password also known as 2-Step Verification
   which is desribed in detail on this [support
   page](https://support.google.com/accounts/answer/185833).

1. The mobile device ID is a 16-digit hexadecimal string (without a
   '0x' prefix) identifying an Android device or a string of the form
   `ios:01234567-0123-0123-0123-0123456789AB` (including the `ios:`
   prefix) identifying an iOS device you must already have registered
   for Google Play Music. On Android you can obtain this ID by dialing
   `*#*#8255#*#*` on your phone (see the aid) or using this
   [App](https://play.google.com/store/apps/details?id=com.evozi.deviceid)
   (see the Google Service Framework ID Key). You may also use the
   script `mobile_devices.py` to list all registered devices. If your
   Android or iOS device is already registered, you may leave the
   field `Mobile Device ID` empty. It will be filled in automatically
   after setting the username and password.

   **Note**: A registered PC MAC address will not work as a mobile
     device ID.

1. Enable All Access if you have an All Access subscription.

1. You will find the plug-in in the 'My Apps' section of the
   squeezebox menu.

Donate for this Plugin
----------------------

This plugin was originally written by hechtus. If you are enjoying this plugin feel free to
[donate](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=Z2KE8W5HW9F8W)
to him.


ToDo
----

I'm looking forward to your help. Feel free to
[contribute](https://help.github.com/articles/fork-a-repo) or to
[report
bugs](https://github.com/squeezebox-googlemusic/squeezebox-googlemusic/issues). Here
are some things you may help on:

* Get this plugin running on non-Linux systems
* Add or improve
  [translations](https://github.com/hechtus/squeezebox-googlemusic/blob/master/GoogleMusic/strings.txt)
  to other languages
* Test the plugin with various Android or iOS Apps. Is it working with
  iPeng?
* Support for creating and deleting radio stations
* Improve Track and Album Info
