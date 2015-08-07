I forked shairport so I could be sure of always having this software available.  Who knows, I may start hacking it someday.

What it is
----------
This program emulates an AirPort Express for the purpose of streaming music from iTunes and compatible iPods and iPhones. It implements a server for the Apple RAOP protocol.
ShairPort does not support AirPlay v2 (video and photo streaming).

Build Requirements
------------------
Required:
* OpenSSL

Optionally:
* libao
* PulseAudio
* avahi

Debian/Raspbian users can get the basics with
`apt-get install libssl-dev libavahi-client-dev libasound2-dev`


Runtime Requirements
--------------------
You must be running an mDNS (Bonjour) daemon. On a Mac, this will be running already. Otherwise, you must be running avahi-daemon or Howl.
As an alternative, you may use the tinysvcmdns backend, which embeds a lightweight mDNS daemon. It is, however, way less robust than bonjour or avahi.
Check the [mDNS Backends] section for more information.

How to get started
-------------
```
./configure
make
./shairport -a 'My Shairport Name'
```

The triangle-in-rectangle AirTunes (now AirPlay) logo will appear in the iTunes status bar of any machine on the network, or on iPod/iPhone play controls screen. Choose your access point name to start streaming to the ShairPort instance.

Audio Outputs
-------------
Shairport supports different audio backends.
For a list of available backends and their options, run `shairport -h`.
Note that options are supplied to backends at the end of the commandline, separated by --, for example:
```
shairport -o ao -- -d mydriver -o setting=thing
```

mDNS Backends
-------------
Shairport uses mDNS to advertise the service. Multiple backends are available to perform the task.
For a list of available backends, run `shairport -h`.
The backends prefixed by 'external' rely on external programs that should be present in your path.
By default, shairport will try all backends, in the order they are listed by `shairport -h`, until one works.
You can force the use of a specific backend using `shairport -m tinysvcmdns` for example.

Metadata
--------

The following metadata can be output for the currently playing track:

  * artist
  * title
  * album
  * artwork
  * genre
  * comment

To enable the output of metadata, the `-M <directory name>` flag must be set to
instruct `shairport` where to save the output. This directory must exist. A
fifo named `now_playing` will be created, and records will be written to it
when tracks are changed. The end of a set of metadata is delimited by a
zero-length line. Cover filenames are relative to the cover directory. Files
are not deleted.

An example::

    artist=Arcade Fire
    title=City With No Children
    album=The Suburbs
    artwork=cover-e6450a45ab900815e831434f5ee0499c.jpg
    genre=Rock
    comment=
