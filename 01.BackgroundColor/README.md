
**EN** | [RU][ru]

| < Back | Index | Next > |
|-|-|-|
| Not available | [Tutorials][index] | [02. Mouse][02.Mouse] |

## 01. Background color

In this tutorial we start education by learning to set background color.

Estimated completion time: 5 minutes.

## Table of contents

* [Red background](#red)
* [Print background color](#print)
* [Summary](#summary)

<a name="red"/>

# Red background

Here's the line of code to set background color to red:

```lua
main.application.camera.clearColor = {1, 0, 0}
```
**[Run in `ogse`][run-red]**

**Note**: either paste this code yourself to `ogse`, or simply click **Run in `ogse`**.

Let's see into API we used:

* `main` namespace hosts `application` instance
* `main.application` instance hosts subsystems like `camera`, `mouse`, etc.
* `main.application.camera` instance is a viewport into application's scene
* `main.application.camera.clearColor` property is a clearing color (effectively background color) of the camera
    * **accepts** array of color components in RGB format
        ```lua
        main.application.camera.clearColor = {1, 0, 0}
        ```
    * **returns** array of color components in RGB format
        ```lua
        local color = main.application.camera.clearColor
        print("background color:", color[1], color[2], color[3])
        ```

<a name="print"/>

# Print default background color

It was fairly easy to set background color, right? Now let's find out what
color is used by default:

```lua
local color = main.application.camera.clearColor
print("Default background color:", color[1], color[2], color[3])
```
**[Run in `ogse`][run-print]**

**Notes**:

* `local` keyword means that declared variable is local to current
scope and will be garbage collected upon the scope's exit
* `Lua` indexes arrays starting from `1`, unlike `C` that does so from `0`

Have a look at the debug console. You should see the following line:

```
Default background color:  0.200000    0.200000    0.400000
```

Thus, default background color is `0.2, 0.2, 0.4`. Why that specific color,
you ask? Because `0.2, 0.2, 0.4` is default background color of
`OpenSceneGraph` used by `ogs`.

<a name="summary"/>

# Summary

You have successfully set background color to red and then printed default
background color.

| < Back | Index | Next > |
|-|-|-|
| Not available | [Tutorials][index] | [02. Mouse][02.Mouse] |

[ru]: README-ru.md

[index]: ../README.md
[02.Mouse]: ../02.Mouse/README.md

[run-red]: http://ogstudio.github.io/ogse/?base64code=bWFpbi5hcHBsaWNhdGlvbi5jYW1lcmEuY2xlYXJDb2xvciA9IHsxLCAwLCAwfQ==
[run-print]: https://ogstudio.github.io/ogse/?base64code=bG9jYWwgY29sb3IgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYS5jbGVhckNvbG9yCnByaW50KCJEZWZhdWx0IGJhY2tncm91bmQgY29sb3I6IiwgY29sb3JbMV0sIGNvbG9yWzJdLCBjb2xvclszXSk=
