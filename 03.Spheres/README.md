
**EN** | [RU][ru]

| < Back | Index | Next > |
|-|-|-|
| [02. Mouse][02.Mouse] | [Tutorials][index] | [04. Node selection][04.Selection] |

## 03. Spheres

In this tutorial we are going to display spheres.

Estimated completion time: 10 minutes.

## Table of contents

* [Single sphere](#sphere)
* [Another sphere](#spheres)
* [Camera orientation](#camera)
* [Two spheres](#two)
* [Summary](#summary)

<a name="sphere"/>

# Single sphere

Let's display single sphere:

```lua
local nodes = main.application.nodes

local sphere = nodes:createSphere("sphere", 1)
local root = nodes:node("root")
root:addChild(sphere)
```
**[Run in `ogse`][run-sphere]**

Let's see into API we introduced:

* `main.application.nodes` instance hosts scene nodes (not necessarily visible) of `scene.Node` class
* `main.application.nodes:createSphere()` method
    * **accepts** name of the sphere and its radius
    * **returns** a new instance of `scene.Node` represented as a sphere
        ```lua
        local sphere = main.application.nodes:createSphere("sphere", 1)
        ```
* `main.application.nodes:node()` method
    * **accepts** name of the node to find among nodes hosted by `main.application.nodes` instance
    * **returns** either an instance of `scene.Node` that already exists, or `nil` otherwise
        ```lua
        local node = main.application.nodes:node("sphere")
        if (node)
        then
            print("Node exists")
        else
            print("Node does not exist")
        end
        ```
* `scene` namespace hosts scene graph management functionality
* `scene.Node:addChild()` method
    * **accepts** an instance of `scene.Node` to attach it as a child node
        ```lua
        local parent = main.application.nodes:node("parent")
        local child = main.application.nodes:node("child")
        parent:addChild(child)
        ```

**Notes**:

* scene node names should be unique
* `root` node is created by `ogs` and serves as the root for visible scene nodes
* only nodes that have `root` at the beginning of their scene graph hierarchy are visible

<a name="spheres"/>

# Another sphere

Let's display another sphere to the right of currently displayed sphere.

**Add** the following code:

```lua
local sphereRight = nodes:createSphere("another", 1)
root:addChild(sphereRight)
sphereRight.position = {2, 0, 0}
```
**[Run in `ogse`][run-spheres]**

Let's see into API we introduced:

* `scene.Node.position` property
    * **accepts** array of position components in XYZ format
        ```lua
        node.position = {2, 0, 0}
        ```
    * **returns** array of position components in XYZ format
        ```lua
        local pos = node.position
        print("Node position:", pos[1], pos[2], pos[3])
        ```

You probably noticed two strange things by now:

* `sphereRight` is actually at the **left**
* you only see part of the sphere

<a name="camera"/>

# Camera orientation

These issues arise because we let camera decide its position for itself.
Let's see current camera position and rotation.

**Add** the following code:

```lua
local camera = main.application.camera

local pos = camera.position
print("Camera position:", pos[1], pos[2], pos[3])
local rot = camera.rotation
print("Camera rotation:", rot[1], rot[2], rot[3])
```
**[Run in `ogse`][run-camera]**

Let's see into API we introduced:

* `main.application.camera.position` property
    * **accepts** array of position components in XYZ format
        ```lua
        main.application.camera.position = {0, -30, 0}
        ```
    * **returns** array of position components in XYZ format
        ```lua
        local pos = main.application.camera.position
        print("Camera position:", pos[1], pos[2], pos[3])
        ```
* `main.application.camera.rotation` property
    * **accepts** array of rotation components in XYZ degrees
        ```lua
        main.application.camera.rotation = {90, 0, 0}
        ```
    * **returns** array of rotation components in XYZ degrees
        ```lua
        local rot = main.application.camera.rotation
        print("Camera rotation:", rot[1], rot[2], rot[3])
        ```

You should see something like this in the debug console:
```
Camera position:    0.000000    3.974028    0.000000
Camera rotation:    90.000000   0.000000    180.000000
```

Quite an interesting camera orientation, right?

<a name="two"/>

# Two spheres

You might be thinking that setting camera rotation to `0, 0, 0` would place
`sphereRight` to the right. However, rotation alone is not enough to make
scene look good. Instead, we need the following camera orientation:

* position: `0, -30, 0`
* rotation: `90, 0, 0`

To be honest, we came up with these values by experimenting, we don't have
any logical explanation here for you. Sorry.

Now, let's display both spheres so that we can see them clearly. Here's
complete code:

```lua
local nodes = main.application.nodes

local sphere = nodes:createSphere("sphere", 1)
local root = nodes:node("root")
root:addChild(sphere)

local sphereRight = nodes:createSphere("another", 1)
root:addChild(sphereRight)
sphereRight.position = {2, 0, 0}

local camera = main.application.camera

camera.position = {0, -30, 0}
camera.rotation = {90, 0, 0}
```
**[Run in `ogse`][run-two]**

Now `sphereRight` is finally to the right of the original sphere.

<a name="summary"/>

# Summary

You have successfully created spherical scene nodes, positioned one of them and
then oriented the camera to have a better look at the scene.

| < Back | Index | Next > |
|-|-|-|
| [02. Mouse][02.Mouse] | [Tutorials][index] | [04. Node selection][04.Selection] |

[ru]: README-ru.md

[index]: ../README.md
[02.Mouse]: ../02.Mouse/README.md
[04.Selection]: ../04.Selection/README.md

[run-sphere]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUp
[run-spheres]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUpCgpsb2NhbCBzcGhlcmVSaWdodCA9IG5vZGVzOmNyZWF0ZVNwaGVyZSgiYW5vdGhlciIsIDEpCnJvb3Q6YWRkQ2hpbGQoc3BoZXJlUmlnaHQpCnNwaGVyZVJpZ2h0LnBvc2l0aW9uID0gezIsIDAsIDB9
[run-camera]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUpCgpsb2NhbCBzcGhlcmVSaWdodCA9IG5vZGVzOmNyZWF0ZVNwaGVyZSgiYW5vdGhlciIsIDEpCnJvb3Q6YWRkQ2hpbGQoc3BoZXJlUmlnaHQpCnNwaGVyZVJpZ2h0LnBvc2l0aW9uID0gezIsIDAsIDB9Cgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQoKbG9jYWwgcG9zID0gY2FtZXJhLnBvc2l0aW9uCnByaW50KCJDYW1lcmEgcG9zaXRpb246IiwgcG9zWzFdLCBwb3NbMl0sIHBvc1szXSkKbG9jYWwgcm90ID0gY2FtZXJhLnJvdGF0aW9uCnByaW50KCJDYW1lcmEgcm90YXRpb246Iiwgcm90WzFdLCByb3RbMl0sIHJvdFszXSk=
[run-two]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUpCgpsb2NhbCBzcGhlcmVSaWdodCA9IG5vZGVzOmNyZWF0ZVNwaGVyZSgiYW5vdGhlciIsIDEpCnJvb3Q6YWRkQ2hpbGQoc3BoZXJlUmlnaHQpCnNwaGVyZVJpZ2h0LnBvc2l0aW9uID0gezIsIDAsIDB9Cgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQoKY2FtZXJhLnBvc2l0aW9uID0gezAsIC0zMCwgMH0KY2FtZXJhLnJvdGF0aW9uID0gezkwLCAwLCAwfQ==
