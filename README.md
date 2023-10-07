Nostalgia bucklespring / Cherry MX Blue keyboard sound
==========================================================================

This project emulates the sound of my old faithful IBM Model-M space saver
bucklespring keyboard while typing on my notebook, mainly for the purpose of
annoying the hell out of my coworkers.

You can also use Cherry MX Blue sounds, pulled from the keyclacker
project.

![Model M](img/model-m.jpg)
![Buckle](img/buckle.gif)

Bucklespring runs as a background process and plays back the sound of each key
pressed and released on your keyboard, just as if you were using an IBM
Model-M. The sound of each key has carefully been sampled, and is played back
while simulating the proper distance and direction for a realistic 3D sound
palette of pure nostalgic bliss.

To temporarily silence bucklespring, for example to enter secrets, press
ScrollLock twice (but be aware that those ScrollLock events _are_ delivered to
the application); same to unmute. The keycode for muting can be changed with
the `-m` option. Use keycode 0 to disable the mute function.

Installation
------------

[![Packaging status](https://repology.org/badge/tiny-repos/bucklespring.svg)](https://repology.org/project/bucklespring/versions)

#### Building
```
$ make
$ ./buckle
```

The default Linux build requires X11 for grabbing events. If you want to use
Bucklespring on the linux console or Wayland display server, you can configure
buckle to read events from the raw input devices in /dev/input. This will
require special permissions for buckle to open the devices, though. Build with

```
$ make libinput=1
```

### MacOS

I've heard rumours that bucklespring also runs on MacOS. I've been told that
the following should do:

```
$ brew install alure pkg-config
$ git clone https://github.com/jamescherti/bucklespring-cherrymxblue && cd bucklespring
$ sed -i '' 's/-Wall -Werror/-Wall/' Makefile
$ make
$ ./buckle
```

Note that you need superuser privileges to create the event tap on Mac OS X.
Also give your terminal Accessibility rights: system preferences -> security -> privacy -> accessibility

If you want to use buckle while doing normal work, add an & behind the command.
```
$ sudo ./buckle &
```

### Windows

I think the windows build is currently broken, it seems that switching from
Freelut to Alure broke windows, I might fix this one day.

I suspect there is something wrong with `alureCreateBufferFromFile()` getting
called from another thread in the key capture callback, but my knowledge of the
win32 platform is so poor I'm not even able to run a debugger to see what is
happening. Help from an expert is much appreciated.


Usage
-----

````
usage: ./buckle [options]

options:

  -d DEVICE use OpenAL audio device DEVICE
  -f        use a fallback sound for unknown keys
  -g GAIN   set playback gain [0..100]
  -m CODE   use CODE as mute key (default 0x46 for scroll lock)
  -M        start the program muted
  -h        show help
  -l        list available openAL audio devices
  -p PATH   load .wav files from directory PATH
  -s WIDTH  set stereo width [0..100]
  -v        increase verbosity / debugging
````

OpenAL notes
------------


Bucklespring uses the OpenAL library for mixing samples and providing a
realistic 3D audio playback. This section contains some tips and tricks for
properly tuning OpenAL for bucklespring.

* The default OpenAL settings can cause a slight delay in playback. Edit or create
  the OpenAL configuration file `~/.alsoftrc` and add the following options:

 ````
 period_size = 32
 periods = 4
 ````

* If you are using headphones, enabling the head-related-transfer functions in OpenAL
  for a better 3D sound:

 ````
 hrtf = true
 ````

* When starting an OpenAL application, the internal sound card is selected for output,
  and you might not be able to change the device using pavucontrol. The option to select
  an alternate device is present, but choosing the device has no effect. To solve this,
  add the following option to the OpenAL configuration file:

 ````
 allow-moves = true
 ````

Authors
------------
This version of bucklespring is maintained by [James Cherti](https://www.jamescherti.com/).

Ico Doornekamp (Original author)
Egor
Ico Doornekamp
Jakub Wilk
Peter Hofmann
Marco Trevisan
nofal (Cherry MX sounds the options)
Marco Trevisan
Member1221
mirabilos
Alex Bertram
Alexander Willner
Anjan Momi
Anton Karmanov
Clipsey
Dominik George
Emanuel Haupt
Jan Chren (rindeal)
Jan Chren
Jeroen Knoops
Jeroen Knoops
Nisker
Peter Tonoli
Sebastian Morr
Stephen Gelman
Vladislav Khvostov
jeromenerf
qu1gl3s
rabin-io
somini
tensorknower69
tnagorra
