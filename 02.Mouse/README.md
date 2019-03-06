
**EN** | [RU][ru]

| < Back | Index | Next > |
|-|-|-|
| [01. Background color][01.BackgroundColor] | [Tutorials][index] | [03. Sphere][03.Sphere] |

## 02. Mouse

In this tutorial we are going to set background color on mouse button press.

Estimated completion time: 5 minutes.

## Table of contents

* [Mouse buttons](#buttons)
* [Toggle background color](#toggle)
* [Summary](#summary)

<a name="buttons"/>

# Mouse buttons

Let's detect mouse buttons' presses and releases:

```lua
local mouse = main.application.mouse
mouse.pressedButtonsChanged:addCallback(
    function()
        print("Mouse buttons have been pressed or released")
        print("Pressed buttons:", #mouse.pressedButtons)
    end
)
```
**[Run in `ogse`][run-buttons]**

Let's see into API we used:

* `main.application.mouse` instance lets you get current mouse (finger)
properties like position, pressed mouse buttons and subscribe to changes of
the properties
* `main.application.mouse.pressedButtons` is an array of pressed mouse buttons
* `main.application.mouse.pressedButtonsChanged` is a notification instance
(`core.Reporter`) that reports notifications when mouse buttons are pressed
or released
    * **to subscribe** to all notifications, we use `core.Reporter`'s `addCallback()` method:
        ```lua
        main.application.mouse.pressedButtonsChanged:addCallback(
            function()
                print("Mouse buttons have been pressed or released")
            end
        )
        ```

**Notes**:

* `pressedButtonsChanged` is a notification instance we subscribe to
* `addCallback()` is a method of `pressedButtonsChanged` instance
* `pressedButtonsChanged` and `addCallback` are separated by `:` because it's a
method call
* `function() ... end` block represents a callback function (closure) to be
executed each time notification is reported
* `#` operator returns number of items of an array

Have a look at the debug console. You should see output similar to this when
you press mouse button(s):

```
Mouse buttons have been pressed or released
Pressed buttons:    1
Mouse buttons have been pressed or released
Pressed buttons:    0
Mouse buttons have been pressed or released
Pressed buttons:    1
Mouse buttons have been pressed or released
Pressed buttons:    2
Mouse buttons have been pressed or released
Pressed buttons:    1
Mouse buttons have been pressed or released
Pressed buttons:    0
```

<a name="toggle"/>

# Toggle background color

Let's set background color to red when at least one mouse button is pressed,
and revert background color back to default `0.2, 0.2, 0.4` when
none of mouse buttons is pressed:

```lua
local DEFAULT_COLOR = {0.2, 0.2, 0.4}
local PRESSED_COLOR = {1.0, 0.0, 0.0}

local mouse = main.application.mouse
local camera = main.application.camera

mouse.pressedButtonsChanged:addCallback(
    function()
        if (#mouse.pressedButtons > 0)
        then
            camera.clearColor = PRESSED_COLOR
        else
            camera.clearColor = DEFAULT_COLOR
        end
    end
)
```
**[Run in `ogse`][run-toggle]**

Now background color is red when you hold mouse button(s).

<a name="summary"/>

# Summary

You have successfully detected mouse buttons' presses/releases and toggled
background color.

| < Back | Index | Next > |
|-|-|-|
| [01. Background color][01.BackgroundColor] | [Tutorials][index] | [03. Sphere][03.Sphere] |

[ru]: README-ru.md

[index]: ../README.md
[01.BackgroundColor]: ../01.BackgroundColor/README.md
[03.Sphere]: ../03.Sphere/README.md

[run-buttons]: https://ogstudio.github.io/ogse/?base64code=bG9jYWwgbW91c2UgPSBtYWluLmFwcGxpY2F0aW9uLm1vdXNlCm1vdXNlLnByZXNzZWRCdXR0b25zQ2hhbmdlZDphZGRDYWxsYmFjaygKICAgIGZ1bmN0aW9uKCkKICAgICAgICBwcmludCgiTW91c2UgYnV0dG9ucyBoYXZlIGJlZW4gcHJlc3NlZCBvciByZWxlYXNlZCIpCiAgICAgICAgcHJpbnQoIlByZXNzZWQgYnV0dG9uczoiLCAjbW91c2UucHJlc3NlZEJ1dHRvbnMpCiAgICBlbmQKKQ==
[run-toggle]: https://ogstudio.github.io/ogse/?base64code=bG9jYWwgREVGQVVMVF9DT0xPUiA9IHswLjIsIDAuMiwgMC40fQpsb2NhbCBQUkVTU0VEX0NPTE9SID0gezEuMCwgMC4wLCAwLjB9Cgpsb2NhbCBtb3VzZSA9IG1haW4uYXBwbGljYXRpb24ubW91c2UKbG9jYWwgY2FtZXJhID0gbWFpbi5hcHBsaWNhdGlvbi5jYW1lcmEKCm1vdXNlLnByZXNzZWRCdXR0b25zQ2hhbmdlZDphZGRDYWxsYmFjaygKICAgIGZ1bmN0aW9uKCkKICAgICAgICBpZiAoI21vdXNlLnByZXNzZWRCdXR0b25zID4gMCkKICAgICAgICB0aGVuCiAgICAgICAgICAgIGNhbWVyYS5jbGVhckNvbG9yID0gUFJFU1NFRF9DT0xPUgogICAgICAgIGVsc2UKICAgICAgICAgICAgY2FtZXJhLmNsZWFyQ29sb3IgPSBERUZBVUxUX0NPTE9SCiAgICAgICAgZW5kCiAgICBlbmQKKQ==
