
[EN][en] | **RU**

| < Назад | Начало | Далее > |
|-|-|-|
| [03. Сферы][03.Spheres] | [Самоучители][index] | [05. Материал][05.Material] |

## 04. Выбор узла

В этом самоучителе мы научимся выбирать сферы мышью (пальцем).

Ориентировочное время выполнения: 10 минут.

## Содержание

* [Три сферы](#spheres)
* [Вывод имени выбранной сферы](#print)
* [Итог](#summary)

<a name="spheres"/>

# Три сферы

Давайте отобразим три сферы:

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
**[Запустить в `ogse`][run-spheres]**

**Замечания**:

* `..` является оператором сцепления (конкатенации) строк
* мы называем сферы как `sphere-0`, `sphere-1` и `sphere-2`
* мы храним сферы в массиве `spheres`, чтобы отметить их для выбора в следующей секции
* ось Z идёт так, как обычно идёт ось Y

<a name="print"/>

# Вывод имени выбранной сферы

Давайте отметим сферы как выбираемые и сделаем вывод их имён при выборе.

**Добавьте** следующий код:

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
**[Запустить в `ogse`][run-print]**

Выбирайте сферы с помощью мыши (пальца). Вы должны увидеть что-то подобное
в консоли отладки:

```
Selected node:  sphere-0
Selected node:  sphere-1
Selected node:  sphere-2
```

Взглянем на новый использованный нами API:

* `scene.Node:setMask()` (метод)
    * **принимает** битовую маску для отметки узла
        ```lua
        node:setMask(0x2)
        ```
* `main.application.camera:nodeAtPosition()` (метод)
    * **принимает** позицию мыши (массив с двумя компонентами: X, Y) и битовую маску
    * **возвращает**
        * либо экземпляр `scene.Node`, который

            1. пересекает луч, исходящий из позиции мыши
            2. отмечен указанной битовой маской
            3. ближайший к камере, если несколько узлов удовлетворяют предыдущим двум условиям

        * либо `nil` в противном случае
        ```lua
        local pos = main.application.mouse.position
        local node = main.application.camera:nodeAtPosition(pos, 0x2)
        if (node)
        then
            print("There is a node behind current mouse position")
        end
        ```
* `scene.Node.__name` (свойство лишь для чтения) содержит имя узла

**Замечания**:

* `SELECTION_MASK` используется для различения выбираемых узлов от остальных
* `pairs()` (функция) используется для прохода массива
* `_` (в цикле `for`) является распространённым способом обозначения
неиспользуемых переменных
* шестнадцатиричное представление является распространённым способом
обозначения битовых масок

<a name="summary"/>

# Итог

Вы успешно отобразили сферы, отметили их как выбираемые, после чего отобразили
их имена при выборе.

| < Назад | Начало | Далее > |
|-|-|-|
| [03. Сферы][03.Spheres] | [Самоучители][index] | [05. Материал][05.Material] |

[en]: README.md

[index]: ../README-ru.md
[03.Spheres]: ../03.Spheres/README-ru.md
[05.Material]: ../05.Material/README-ru.md

[run-spheres]: https://ogstudio.github.io/ogse/?base64script=LS0gT3JpZW50IGNhbWVyYSB0byBoYXZlIGEgYmV0dGVyIGxvb2sgYXQgdGhlIHNjZW5lLgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQpjYW1lcmEucG9zaXRpb24gPSB7MCwgLTMwLCAwfQpjYW1lcmEucm90YXRpb24gPSB7OTAsIDAsIDB9CgotLSBHZXQgc2NlbmUgcm9vdC4KbG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKCi0tIENyZWF0ZSwgcG9zaXRpb24sIGFuZCBkaXNwbGF5IHNwaGVyZXMuCmxvY2FsIHNwaGVyZXMgPSB7IH0KZm9yIGlkID0gMCwgMgpkbwogICAgLS0gQ3JlYXRlIHNwaGVyZS4KICAgIGxvY2FsIG5hbWUgPSAic3BoZXJlLSIgLi4gaWQKICAgIGxvY2FsIHNwaGVyZSA9IG5vZGVzOmNyZWF0ZVNwaGVyZShuYW1lLCAxKQogICAgdGFibGUuaW5zZXJ0KHNwaGVyZXMsIHNwaGVyZSkKICAgIC0tIERpc3BsYXkgaXQuCiAgICByb290OmFkZENoaWxkKHNwaGVyZSkKICAgIC0tIEhhdmUgZnJlZSBzcGFjZSBpbiBiZXR3ZWVuIGJ5IFogYXhpcy4KICAgIGxvY2FsIHBvcyA9IHNwaGVyZS5wb3NpdGlvbgogICAgcG9zWzNdID0gcG9zWzNdIC0gaWQgKiAzCiAgICBzcGhlcmUucG9zaXRpb24gPSBwb3MKZW5k
[run-print]: https://ogstudio.github.io/ogse/?base64script=LS0gT3JpZW50IGNhbWVyYSB0byBoYXZlIGEgYmV0dGVyIGxvb2sgYXQgdGhlIHNjZW5lLgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQpjYW1lcmEucG9zaXRpb24gPSB7MCwgLTMwLCAwfQpjYW1lcmEucm90YXRpb24gPSB7OTAsIDAsIDB9CgotLSBHZXQgc2NlbmUgcm9vdC4KbG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKCi0tIENyZWF0ZSwgcG9zaXRpb24sIGFuZCBkaXNwbGF5IHNwaGVyZXMuCmxvY2FsIHNwaGVyZXMgPSB7IH0KZm9yIGlkID0gMCwgMgpkbwogICAgLS0gQ3JlYXRlIHNwaGVyZS4KICAgIGxvY2FsIG5hbWUgPSAic3BoZXJlLSIgLi4gaWQKICAgIGxvY2FsIHNwaGVyZSA9IG5vZGVzOmNyZWF0ZVNwaGVyZShuYW1lLCAxKQogICAgdGFibGUuaW5zZXJ0KHNwaGVyZXMsIHNwaGVyZSkKICAgIC0tIERpc3BsYXkgaXQuCiAgICByb290OmFkZENoaWxkKHNwaGVyZSkKICAgIC0tIEhhdmUgZnJlZSBzcGFjZSBpbiBiZXR3ZWVuIGJ5IFogYXhpcy4KICAgIGxvY2FsIHBvcyA9IHNwaGVyZS5wb3NpdGlvbgogICAgcG9zWzNdID0gcG9zWzNdIC0gaWQgKiAzCiAgICBzcGhlcmUucG9zaXRpb24gPSBwb3MKZW5kCgotLSBNYWtlIHNwaGVyZXMgc2VsZWN0YWJsZS4KbG9jYWwgU0VMRUNUSU9OX01BU0sgPSAweDIKZm9yIF8sIHNwaGVyZSBpbiBwYWlycyhzcGhlcmVzKQpkbwogICBzcGhlcmU6c2V0TWFzayhTRUxFQ1RJT05fTUFTSykgCmVuZAoKLS0gUHJpbnQgc2VsZWN0ZWQgc3BoZXJlIG5hbWUuCmxvY2FsIG1vdXNlID0gbWFpbi5hcHBsaWNhdGlvbi5tb3VzZQptb3VzZS5wcmVzc2VkQnV0dG9uc0NoYW5nZWQ6YWRkQ2FsbGJhY2soCiAgICBmdW5jdGlvbigpCiAgICAgICAgLS0gRGV0ZWN0IHJlbGVhc2UuCiAgICAgICAgaWYgKCNtb3VzZS5wcmVzc2VkQnV0dG9ucyA9PSAwKQogICAgICAgIHRoZW4KICAgICAgICAgICAgLS0gRmluZCBub2RlIGF0IG1vdXNlIHBvc2l0aW9uLgogICAgICAgICAgICBsb2NhbCBub2RlID0gY2FtZXJhOm5vZGVBdFBvc2l0aW9uKG1vdXNlLnBvc2l0aW9uLCBTRUxFQ1RJT05fTUFTSykKICAgICAgICAgICAgaWYgKG5vZGUpCiAgICAgICAgICAgIHRoZW4KICAgICAgICAgICAgICAgIHByaW50KCJTZWxlY3RlZCBub2RlOiIsIG5vZGUuX19uYW1lKQogICAgICAgICAgICBlbmQKICAgICAgICBlbmQKICAgIGVuZAop
