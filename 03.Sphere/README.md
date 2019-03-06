
**EN** | [RU][ru]

| < Back | Index | Next > |
|-|-|-|
| [02. Mouse][02.Mouse] | [Tutorials][index] | [04. ??][04.??] |

## 03. Sphere

In this tutorial we are going to display a sphere.

Estimated completion time: 5 minutes.

## Table of contents

* [Sphere](#sphere)
* [Summary](#summary)

<a name="sphere"/>

# Sphere

Let's display a sphere:

```lua
local sphere = main.application.nodes:createSphere("sphere", 1)
local root = main.application.nodes:node("root")
root:addChild(sphere)
```
**[Run in `ogse`][run-sphere]**

Let's see into API we used:

* `main.application.nodes` instance hosts scene nodes (not necessarily visible)
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

<a name="summary"/>

# Summary

You have successfully created spherical scene node.

| < Back | Index | Next > |
|-|-|-|
| [02. Mouse][02.Mouse] | [Tutorials][index] | [04. ??][04.??] |

[ru]: README-ru.md

[index]: ../README.md
[02.Mouse]: ../02.Mouse/README.md

[run-sphere]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgc3BoZXJlID0gbWFpbi5hcHBsaWNhdGlvbi5ub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzOm5vZGUoInJvb3QiKQpyb290OmFkZENoaWxkKHNwaGVyZSk=
