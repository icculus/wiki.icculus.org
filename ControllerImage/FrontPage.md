# ControllerImage 1.0

The latest version of this library is available from [GitHub](https://github.com/icculus/ControllerImage/releases).

A detailed overview, and a list of available APIs, can be viewed in [CategoryControllerImage](CategoryControllerImage).

This is a library, built on top of [SDL3](https://wiki.libsdl.org/SDL3),
that provides resolution-independent images for game
controller inputs, so games can show the correct visual markers for the
gamepad in the user's hand.

This is intended, for example, to let you show a "Press `[IMAGE]` to continue"
message, where `[IMAGE]` might be a yellow 'Y' if the user has an Xbox
controller and a green triangle if they have a PlayStation controller.

It is intended to work with whatever looks like a gamepad to SDL3, but it
requires artwork, in SVG format, for whatever controller the user happens to
be using. The standard ones (Xbox, PlayStation, Switch, among others) are supplied, and if
we can't offer anything better, we'll aim for a generic Xbox 360 controller,
under the assumption it _probably_ represents most generic third-party devices.

It is available under the zlib license, found in the file [LICENSE.txt](https://github.com/icculus/ControllerImage/blob/main/LICENSE.txt).

Enjoy!


