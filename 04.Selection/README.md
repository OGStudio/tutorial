
**EN** | [RU][ru]

| < Back | Index | Next > |
|-|-|-|
| [03. Spheres][03.Spheres] | [Tutorials][index] | [05. ??][05.??] |

## 04. Node selection

In this tutorial we are going to select spheres with mouse (finger).

Estimated completion time: 10 minutes.

## Table of contents

* [Three spheres](#spheres)
* [Print selected sphere name](#print)
* [Summary](#summary)

<a name="spheres"/>

# Three spheres

Let's display three spheres:

```lua
-- Orient camera to have a better look at the scene.
local camera = main.application.camera
camera.position = {0, -30, 0}
camera.rotation = {90, 0, 0}

-- Get scene root.
local nodes = main.application.nodes
local root = nodes:node("root")

-- Create, position, and display spheres.
local spheres = { }
for id = 0, 2
do
    -- Create sphere.
    local name = "sphere-" .. id
    local sphere = nodes:createSphere(name, 1)
    table.insert(spheres, sphere)
    -- Display it.
    root:addChild(sphere)
    -- Have free space in between by Z axis.
    local pos = sphere.position
    pos[3] = pos[3] - id * 3
    sphere.position = pos
end
```
**[Run in `ogse`][run-spheres]**

**Notes**:

* `..` is a string concatenation operator
* we name spheres as `sphere-0`, `sphere-1`, and `sphere-2`
* we keep spheres in `spheres` array to mark them for selection in the next section
* Z axis goes just like you would expect Y to go

<a name="print"/>

# Print selected sphere name

Let's make spheres selectable and print their names upon selection.

**Add** the following code:

```lua
-- Make spheres selectable.
local SELECTION_MASK = 0x2
for _, sphere in pairs(spheres)
do
   sphere:setMask(SELECTION_MASK) 
end

-- Print selected sphere name.
local mouse = main.application.mouse
mouse.pressedButtonsChanged:addCallback(
    function()
        -- Detect release.
        if (#mouse.pressedButtons == 0)
        then
            -- Find node at mouse position.
            local node = camera:nodeAtPosition(mouse.position, SELECTION_MASK)
            if (node)
            then
                print("Selected node:", node.__name)
            end
        end
    end
)
```
**[Run in `ogse`][run-print]**

Select spheres with mouse (finger). You should see something like this
in the debug console:

```
Selected node:  sphere-0
Selected node:  sphere-1
Selected node:  sphere-2
```

Let's see into API we introduced:

* `scene.Node:setMask()` method
    * **accepts** bit mask to mark a scene node with 
        ```lua
        node:setMask(0x2)
        ```
* `main.application.camera:nodeAtPosition()` method
    * **accepts** mouse position (an array with two components: X, Y) and a bit mask
    * **returns**
        * either an instance of `scene.Node` that

            1. intersects a ray coming from mouse position
            2. has specified bit mask
            3. is closest to the camera if several scene nodes match the first two conditions

        * or `nil` otherwise
        ```lua
        local pos = main.application.mouse.position
        local node = main.application.camera:nodeAtPosition(pos, 0x2)
        if (node)
        then
            print("There is a node behind current mouse position")
        end
        ```
* `scene.Node.__name` read-only property contains the name of a node

**Notes**:

* `SELECTION_MASK` is used to tell apart selectable nodes from the rest
* `pairs()` function allows to loop an array
* `_` (in `for` loop) is a common way to denote unused variables
* hexidecimal notation is a common way to denote bit masks

<a name="summary"/>

# Summary

You have successfully displayed spheres, made them selectable, and then
printed their names upon selection.

| < Back | Index | Next > |
|-|-|-|
| [03. Spheres][03.Spheres] | [Tutorials][index] | [05. ??][05.??] |

[ru]: README-ru.md

[index]: ../README.md
[03.Spheres]: ../03.Spheres/README.md
[05.??]: ../05.??/README.md

[run-spheres]: https://ogstudio.github.io/ogse/?base64script=LS0gT3JpZW50IGNhbWVyYSB0byBoYXZlIGEgYmV0dGVyIGxvb2sgYXQgdGhlIHNjZW5lLgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQpjYW1lcmEucG9zaXRpb24gPSB7MCwgLTMwLCAwfQpjYW1lcmEucm90YXRpb24gPSB7OTAsIDAsIDB9CgotLSBHZXQgc2NlbmUgcm9vdC4KbG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKCi0tIENyZWF0ZSwgcG9zaXRpb24sIGFuZCBkaXNwbGF5IHNwaGVyZXMuCmxvY2FsIHNwaGVyZXMgPSB7IH0KZm9yIGlkID0gMCwgMgpkbwogICAgLS0gQ3JlYXRlIHNwaGVyZS4KICAgIGxvY2FsIG5hbWUgPSAic3BoZXJlLSIgLi4gaWQKICAgIGxvY2FsIHNwaGVyZSA9IG5vZGVzOmNyZWF0ZVNwaGVyZShuYW1lLCAxKQogICAgdGFibGUuaW5zZXJ0KHNwaGVyZXMsIHNwaGVyZSkKICAgIC0tIERpc3BsYXkgaXQuCiAgICByb290OmFkZENoaWxkKHNwaGVyZSkKICAgIC0tIEhhdmUgZnJlZSBzcGFjZSBpbiBiZXR3ZWVuIGJ5IFogYXhpcy4KICAgIGxvY2FsIHBvcyA9IHNwaGVyZS5wb3NpdGlvbgogICAgcG9zWzNdID0gcG9zWzNdIC0gaWQgKiAzCiAgICBzcGhlcmUucG9zaXRpb24gPSBwb3MKZW5k
[run-print]: https://ogstudio.github.io/ogse/?base64script=LS0gT3JpZW50IGNhbWVyYSB0byBoYXZlIGEgYmV0dGVyIGxvb2sgYXQgdGhlIHNjZW5lLgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQpjYW1lcmEucG9zaXRpb24gPSB7MCwgLTMwLCAwfQpjYW1lcmEucm90YXRpb24gPSB7OTAsIDAsIDB9CgotLSBHZXQgc2NlbmUgcm9vdC4KbG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKCi0tIENyZWF0ZSwgcG9zaXRpb24sIGFuZCBkaXNwbGF5IHNwaGVyZXMuCmxvY2FsIHNwaGVyZXMgPSB7IH0KZm9yIGlkID0gMCwgMgpkbwogICAgLS0gQ3JlYXRlIHNwaGVyZS4KICAgIGxvY2FsIG5hbWUgPSAic3BoZXJlLSIgLi4gaWQKICAgIGxvY2FsIHNwaGVyZSA9IG5vZGVzOmNyZWF0ZVNwaGVyZShuYW1lLCAxKQogICAgdGFibGUuaW5zZXJ0KHNwaGVyZXMsIHNwaGVyZSkKICAgIC0tIERpc3BsYXkgaXQuCiAgICByb290OmFkZENoaWxkKHNwaGVyZSkKICAgIC0tIEhhdmUgZnJlZSBzcGFjZSBpbiBiZXR3ZWVuIGJ5IFogYXhpcy4KICAgIGxvY2FsIHBvcyA9IHNwaGVyZS5wb3NpdGlvbgogICAgcG9zWzNdID0gcG9zWzNdIC0gaWQgKiAzCiAgICBzcGhlcmUucG9zaXRpb24gPSBwb3MKZW5kCgotLSBNYWtlIHNwaGVyZXMgc2VsZWN0YWJsZS4KbG9jYWwgU0VMRUNUSU9OX01BU0sgPSAweDIKZm9yIF8sIHNwaGVyZSBpbiBwYWlycyhzcGhlcmVzKQpkbwogICBzcGhlcmU6c2V0TWFzayhTRUxFQ1RJT05fTUFTSykgCmVuZAoKLS0gUHJpbnQgc2VsZWN0ZWQgc3BoZXJlIG5hbWUuCmxvY2FsIG1vdXNlID0gbWFpbi5hcHBsaWNhdGlvbi5tb3VzZQptb3VzZS5wcmVzc2VkQnV0dG9uc0NoYW5nZWQ6YWRkQ2FsbGJhY2soCiAgICBmdW5jdGlvbigpCiAgICAgICAgLS0gRGV0ZWN0IHJlbGVhc2UuCiAgICAgICAgaWYgKCNtb3VzZS5wcmVzc2VkQnV0dG9ucyA9PSAwKQogICAgICAgIHRoZW4KICAgICAgICAgICAgLS0gRmluZCBub2RlIGF0IG1vdXNlIHBvc2l0aW9uLgogICAgICAgICAgICBsb2NhbCBub2RlID0gY2FtZXJhOm5vZGVBdFBvc2l0aW9uKG1vdXNlLnBvc2l0aW9uLCBTRUxFQ1RJT05fTUFTSykKICAgICAgICAgICAgaWYgKG5vZGUpCiAgICAgICAgICAgIHRoZW4KICAgICAgICAgICAgICAgIHByaW50KCJTZWxlY3RlZCBub2RlOiIsIG5vZGUuX19uYW1lKQogICAgICAgICAgICBlbmQKICAgICAgICBlbmQKICAgIGVuZAop
