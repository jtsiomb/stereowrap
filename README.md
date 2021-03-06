#![logo](http://nuclear.mutantstargoat.com/sw/stereowrap/stereowrap_logo.png) stereowrap

About
-----
Stereowrap is an emulation layer implementing stereoscopic OpenGL visuals on
top of non stereo capable OpenGL implementations. To do that it overrides,
using `LD_PRELOAD`, the GLX visual selection functions (`glXChooseVisual` and
`glXChooseFBConfig`), `glDrawBuffer`, and `glXSwapBuffers` to capture and composite
the two stereo images rendered by the application, in a number of ways. 

Currently stereowrap supports presenting the stereo pair in the following ways:
 * parallel side-by-side (`-m parallel`)
 * side-by-side (`-m cross`)
 * color anaglyph:
   - red-cyan (`-m redcyan`)
   - red-blue (`-m redblue`)
   - green-magenta (`-m greenmagenta`)
   - colorcode3d, aka amber-blue (`-m colorcode`) 
 * sequential left/right sync-ed to vblank (`-m sequential`)

The sequential mode is there to support circuits that drive shutter glasses
from the VGA vsync signal, [like this one](http://codelab.wordpress.com/2012/03/02/vsync-driven-shutter-glasses/).

License
-------
Copyright (C) 2010 - 2011 John Tsiombikas <nuclear@member.fsf.org>
Stereowrap is free software, distributed under the terms of the GNU General
Public License version 3, or any later version published by the Free Software
Foundation. See COPYING file for details.

Installation and Usage
----------------------
Just type `make` to compile stereowrap, and `make install` to install it. In
order to run a stereoscopic OpenGL program just type stereowrap, followed by the
name of the program. The stereo presentation method can be chosen using the `-m`
option (see `stereowrap -h` for help regarding the various options).

Example:
```
$ stereowrap -m redcyan glxgears -stereo
```

Note: command-line options to stereowrap must preceed the name of the program
you wish to wrap, any argument after that is passed to the program itself.

Patent Issues
-------------
The ColorCode3D anaglyph method is patented (US Patent #6687003). I live in the
EU so I don't give a shit, but if you care you may compile stereowrap with
colorcode disabled. Just modify the Makefile and add `-DNOCOLORCODE` at the end of
the CFLAGS line to do that.
