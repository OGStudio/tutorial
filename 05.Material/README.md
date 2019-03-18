
**EN** | [RU][ru]

| < Back | Index | Next > |
|-|-|-|
| [04. Selection][04.Selection] | [Tutorials][index] | [06. ??][06.??] |

## 05. Material

In this tutorial we are going to dislay colored sphere.

Estimated completion time: 10 minutes.

## Table of contents

* [Sphere](#sphere)
* [Red color](#red)
* [Toggle sphere color](#toggle)
* [Summary](#summary)

<a name="sphere"/>

# Sphere

Let's display a sphere:

```lua
local nodes = main.application.nodes
local root = nodes:node("root")
local sphere = nodes:createSphere("sphere", 1)
root:addChild(sphere)
```
**[Run in `ogse`][run-sphere]**

<a name="red"/>

# Red color

Let's make this sphere red.

**Add** the following code:

```lua
local plainVertexShader = [[
void main()
{
    gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex;
}
]]
local colorFragmentShader = [[
void main()
{
    gl_FragColor = vec4(1, 0, 0, 1);
}
]]

local material = main.application.materials:createMaterial("red")
material:setShaders(plainVertexShader, colorFragmentShader)
sphere:setMaterial(material)
```
**[Run in `ogse`][run-red]**

We defined GLSL shaders to color everything in red and then used them to create
material for the sphere.

Let's see into API we introduced:

* `main.application.materials` instance hosts materials that define the look of nodes
* `main.application.materials:createMaterial()` method
    * **accepts** material name to create
    * **returns** a new instance of `render.Material`
        ```lua
        local material = main.application.materials:createMaterial("outfit")
        ```
* `render.Material:setShaders()` method
    * **accepts** vertex and fragment GLSL shaders
        ```lua
        local vertexShader = "void main() { gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex; }"
        local fragmentShader = "void main() { gl_FragColor = vec4(1, 0, 0, 1); }"
        material:setShaders(vertexShader, fragmentShader)
        ```
* `scene.Node:setMaterial()` method
    * **accepts** material instance to paint a node with
        ```lua
        node:setMaterial(material)
        ```

**Notes**:

* `[[` and `]]` allow to define multiline strings in Lua
* `plainVertexShader` converts each node's vertex from object/model space to
screen one to make the node visible on the screen
* `colorFragmentShader` paints each fragment (of the node) in red

<a name="toggle"/>

# Toggle sphere color

Let's toggle sphere color between red and green when pressing mouse button:

```lua
local nodes = main.application.nodes
local root = nodes:node("root")
local sphere = nodes:createSphere("sphere", 1)
root:addChild(sphere)

local plainVertexShader = [[
void main()
{
    gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex;
}
]]
local colorFragmentShader = [[
#ifdef GL_ES
    precision highp float;
#endif

uniform vec3 color;

void main()
{
    gl_FragColor = vec4(color, 1);
}
]]

local material = main.application.materials:createMaterial("many")
material:setShaders(plainVertexShader, colorFragmentShader)
sphere:setMaterial(material)

local COLOR_RED = {1, 0, 0}
local COLOR_GREEN = {0, 1, 0}
-- Default color.
material:setUniform("color", COLOR_RED)
-- Toggle color.
local mouse = main.application.mouse
mouse.pressedButtonsChanged:addCallback(
    function()
        if (#mouse.pressedButtons > 0)
        then
            material:setUniform("color", COLOR_GREEN)
        else
            material:setUniform("color", COLOR_RED)
        end
    end
)
```
**[Run in `ogse`][run-toggle]**

Now sphere is green when you hold the mouse.

Let's see into API we introduced:

* `render.Material:setUniform()` method
    * **accepts** uniform name and its value
        ```lua
        material:setUniform("color", {1, 0, 0})
        ```

**Notes**:

* uniform is a way to pass values from code to shaders
* `precision highp float` is necessary for GLES (used by WebGL) to treat
all floats with specific precision

<a name="summary"/>

# Summary

You have successfully displayed a colored sphere.

| < Back | Index | Next > |
|-|-|-|
| [04. Selection][04.Selection] | [Tutorials][index] | [06. ??][06.??] |

[ru]: README-ru.md

[index]: ../README.md
[04.Selection]: ../04.Selection/README.md
[06.??]: ../06.??/README.md

[run-sphere]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKbG9jYWwgc3BoZXJlID0gbm9kZXM6Y3JlYXRlU3BoZXJlKCJzcGhlcmUiLCAxKQpyb290OmFkZENoaWxkKHNwaGVyZSk=
[run-red]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKbG9jYWwgc3BoZXJlID0gbm9kZXM6Y3JlYXRlU3BoZXJlKCJzcGhlcmUiLCAxKQpyb290OmFkZENoaWxkKHNwaGVyZSkKCmxvY2FsIHBsYWluVmVydGV4U2hhZGVyID0gW1sKdm9pZCBtYWluKCkKewogICAgZ2xfUG9zaXRpb24gPSBnbF9Nb2RlbFZpZXdQcm9qZWN0aW9uTWF0cml4ICogZ2xfVmVydGV4Owp9Cl1dCmxvY2FsIGNvbG9yRnJhZ21lbnRTaGFkZXIgPSBbWwp2b2lkIG1haW4oKQp7CiAgICBnbF9GcmFnQ29sb3IgPSB2ZWM0KDEsIDAsIDAsIDEpOwp9Cl1dCgpsb2NhbCBtYXRlcmlhbCA9IG1haW4uYXBwbGljYXRpb24ubWF0ZXJpYWxzOmNyZWF0ZU1hdGVyaWFsKCJyZWQiKQptYXRlcmlhbDpzZXRTaGFkZXJzKHBsYWluVmVydGV4U2hhZGVyLCBjb2xvckZyYWdtZW50U2hhZGVyKQpzcGhlcmU6c2V0TWF0ZXJpYWwobWF0ZXJpYWwp
[run-toggle]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKbG9jYWwgc3BoZXJlID0gbm9kZXM6Y3JlYXRlU3BoZXJlKCJzcGhlcmUiLCAxKQpyb290OmFkZENoaWxkKHNwaGVyZSkKCmxvY2FsIHBsYWluVmVydGV4U2hhZGVyID0gW1sKdm9pZCBtYWluKCkKewogICAgZ2xfUG9zaXRpb24gPSBnbF9Nb2RlbFZpZXdQcm9qZWN0aW9uTWF0cml4ICogZ2xfVmVydGV4Owp9Cl1dCmxvY2FsIGNvbG9yRnJhZ21lbnRTaGFkZXIgPSBbWwojaWZkZWYgR0xfRVMKICAgIHByZWNpc2lvbiBoaWdocCBmbG9hdDsKI2VuZGlmCgp1bmlmb3JtIHZlYzMgY29sb3I7Cgp2b2lkIG1haW4oKQp7CiAgICBnbF9GcmFnQ29sb3IgPSB2ZWM0KGNvbG9yLCAxKTsKfQpdXQoKbG9jYWwgbWF0ZXJpYWwgPSBtYWluLmFwcGxpY2F0aW9uLm1hdGVyaWFsczpjcmVhdGVNYXRlcmlhbCgibWFueSIpCm1hdGVyaWFsOnNldFNoYWRlcnMocGxhaW5WZXJ0ZXhTaGFkZXIsIGNvbG9yRnJhZ21lbnRTaGFkZXIpCnNwaGVyZTpzZXRNYXRlcmlhbChtYXRlcmlhbCkKCmxvY2FsIENPTE9SX1JFRCA9IHsxLCAwLCAwfQpsb2NhbCBDT0xPUl9HUkVFTiA9IHswLCAxLCAwfQotLSBEZWZhdWx0IGNvbG9yLgptYXRlcmlhbDpzZXRVbmlmb3JtKCJjb2xvciIsIENPTE9SX1JFRCkKLS0gVG9nZ2xlIGNvbG9yLgpsb2NhbCBtb3VzZSA9IG1haW4uYXBwbGljYXRpb24ubW91c2UKbW91c2UucHJlc3NlZEJ1dHRvbnNDaGFuZ2VkOmFkZENhbGxiYWNrKAogICAgZnVuY3Rpb24oKQogICAgICAgIGlmICgjbW91c2UucHJlc3NlZEJ1dHRvbnMgPiAwKQogICAgICAgIHRoZW4KICAgICAgICAgICAgbWF0ZXJpYWw6c2V0VW5pZm9ybSgiY29sb3IiLCBDT0xPUl9HUkVFTikKICAgICAgICBlbHNlCiAgICAgICAgICAgIG1hdGVyaWFsOnNldFVuaWZvcm0oImNvbG9yIiwgQ09MT1JfUkVEKQogICAgICAgIGVuZAogICAgZW5kCik=
