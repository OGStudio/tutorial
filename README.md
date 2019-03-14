
**EN** | [RU][ru]

This document is part of [OGStudio education program][education].

The tutorials describe how to create (and share) simple game with `ogs`
in a matter of few hours.

# Tools

Our main tool is `ogse`
([http://ogstudio.github.io/ogse](https://ogstudio.github.io/ogse)),
a minimalistic on-line editor:

![screen-editor]

On the left side:

* button to execute the code
* code editor

On the right side:

* render window to depict code execution result
* debug console to output valuable information

`ogse` is powered by `ogs`, a tool to create cross-platform 3D games.
`ogs` uses `Lua` language for scripting.

**Note**: your [web browser should have `WebGL` support][webgl] to be able to
run code samples.

# Tutorials

**Note**: the course is in development, so the list of tutorials is not yet final.

| Tutorial | Description | Estimated completion time | Introduced API |
|-|-|-|-|
| [01. Background color][01.BackgroundColor] | Set background color | 5 minutes | <ol><li>`main`</li><li>`main.application`</li><li>`main.application.camera`</li><li>`main.application.camera.clearColor`</li><ol> |
| [02. Mouse][02.Mouse] | Set background color on mouse button press | 5 minutes | <ol><li>`main.application.mouse`</li><li>`main.application.mouse.pressedButtons`</li><li>`main.application.mouse.pressedButtonsChanged`</li><li>`core`</li><li>`core.Reporter`</li><li>`core.Reporter:addCallback()`</li></ol> |
| [03. Spheres][03.Spheres] | Display spheres | 10 minutes | <ol> <li>`main.application.nodes`</li> <li>`main.application.nodes:createSphere()`</li> <li>`main.application.nodes:node()`</li> <li>`scene`</li> <li>`scene.Node:addChild()`</li> <li>`scene.Node.position`</li> <li>`main.application.camera.position`</li> <li>`main.application.camera.rotation`</li> </ol> |
| [04. Node selection][04.Selection] | Select spheres | 10 minutes | <ol> <li>`scene.Node:setMask()`</li> <li>`main.application.camera:nodeAtPosition()`</li> <li>`scene.Node.__name`</li> </ol> |

[ru]: README-ru.md

[education]: http://opengamestudio.org/pages/education.html
[01.BackgroundColor]: 01.BackgroundColor/README.md
[02.Mouse]: 02.Mouse/README.md
[03.Spheres]: 03.Spheres/README.md
[04.Selection]: 04.Selection/README.md

[screen-editor]: ogse.png
[webgl]: https://get.webgl.org
