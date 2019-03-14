
[EN][en] | **RU**

| < Назад | Начало | Далее > |
|-|-|-|
| [02. Мышь][02.Mouse] | [Самоучители][index] | [04. Выбор узла][04.Selection] |

## 03. Сферы

В этом самоучителе мы отобразим сферы.

Ориентировочное время выполнения: 10 минут.

## Содержание

* [Одна сфера](#sphere)
* [Другая сфера](#spheres)
* [Ориентация камеры](#camera)
* [Обе сферы](#two)
* [Итог](#summary)

<a name="sphere"/>

# Одна сфера

Давайте отобразим одну сферу:

```lua
local nodes = main.application.nodes

local sphere = nodes:createSphere("sphere", 1)
local root = nodes:node("root")
root:addChild(sphere)
```
**[Запустить в `ogse`][run-sphere]**

Взглянем на новый использованный нами API:

* `main.application.nodes` (экземпляр) содержит узлы сцены (необязательно видимые) класса `scene.Node`
* `main.application.nodes:createSphere()` (метод)
    * **принимает** название сферы (узла) и её радиус
    * **возвращает** новый экземпляр `scene.Node`, представляющий сферу
        ```lua
        local sphere = main.application.nodes:createSphere("sphere", 1)
        ```
* `main.application.nodes:node()` (метод)
    * **принимает** название искомого узла среди узлов сцены, содержащися экземпляром `main.application.nodes`
    * **возвращает** либо уже существующий экземпляр `scene.Node`, либо `nil` в противном случае
        ```lua
        local node = main.application.nodes:node("sphere")
        if (node)
        then
            print("Node exists")
        else
            print("Node does not exist")
        end
        ```
* `scene` (пространство имён) содержит функциональность управления графом сцены
* `scene.Node:addChild()` (метод)
    * **принимает** экземпляр `scene.Node` для присоединения его в качестве дочернего узла
        ```lua
        local parent = main.application.nodes:node("parent")
        local child = main.application.nodes:node("child")
        parent:addChild(child)
        ```

**Замечания**:

* названия узлов сцены должны быть уникальны
* узел `root` создаётся `ogs` и служит корнем для видимых узлов сцены
* лишь те узлы видимы, которые в начале своей иерархии графа сцены имеют `root`

<a name="spheres"/>

# Другая сфера

Давайте отобразим другую сферу справа от текущей.

**Добавьте** следующий код:

```lua
local sphereRight = nodes:createSphere("another", 1)
root:addChild(sphereRight)
sphereRight.position = {2, 0, 0}
```
**[Запустить в `ogse`][run-spheres]**

Взглянем на новый использованный нами API:

* `scene.Node.position` (свойство)
    * **принимает** массив компонент позиции в формате XYZ
        ```lua
        node.position = {2, 0, 0}
        ```
    * **возвращает** массив компонент позиции в формате XYZ
        ```lua
        local pos = node.position
        print("Node position:", pos[1], pos[2], pos[3])
        ```

Возможно, вы уже заметили пару странных вещей:

* `sphereRight` находится **слева**
* видна лишь часть сферы

<a name="camera"/>

# Ориентация камеры

Эти проблемы возникли из-за того, что камера сама выбрала себе позицию.
Давайте посмотрим, каковы текущие позиция и вращение камеры.

**Добавьте** следующий код:

```lua
local camera = main.application.camera

local pos = camera.position
print("Camera position:", pos[1], pos[2], pos[3])
local rot = camera.rotation
print("Camera rotation:", rot[1], rot[2], rot[3])
```
**[Запустить в `ogse`][run-camera]**

Взглянем на новый использованный нами API:

* `main.application.camera.position` (свойство)
    * **принимает** массив компонент позиции в формате XYZ
        ```lua
        main.application.camera.position = {0, -30, 0}
        ```
    * **возвращает** массив компонент позиции в формате XYZ
        ```lua
        local pos = main.application.camera.position
        print("Camera position:", pos[1], pos[2], pos[3])
        ```
* `main.application.camera.rotation` (свойство)
    * **принимает** массив компонент вращения в градусах XYZ
        ```lua
        main.application.camera.rotation = {90, 0, 0}
        ```
    * **возвращает** массив компонент вращения в градусах XYZ
        ```lua
        local rot = main.application.camera.rotation
        print("Camera rotation:", rot[1], rot[2], rot[3])
        ```

Консоль отладки должна содержать теперь что-то вроде:
```
Camera position:    0.000000    3.974028    0.000000
Camera rotation:    90.000000   0.000000    180.000000
```

Довольно интересная ориентация камеры, не так ли?

<a name="two"/>

# Обе сферы

Возможно, вы решили, что установка вращения камеры в `0, 0, 0` поместит
`sphereRight` справа. Тем не менее, одного вращения не хватит, чтобы улучшить
вид сцены. На самом деле, нам нужна следующая ориентация камеры:

* позиция: `0, -30, 0`
* вращение: `90, 0, 0`

Честно говоря, мы пришли к этим значениям благодаря экспериментам, у нас нет
логического объяснения этих значений. Извиняйте.

Давайте теперь отобразим обе сферы таким образом, чтобы они были отчётливо
видны. Вот полный код:

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
**[Запустить в `ogse`][run-two]**

Теперь `sphereRight` находится справа от первоначальной сферы.

<a name="summary"/>

# Итог

Вы успешно отобразили сферы, позиционировали одну из них, а затем улучшили
угол обзора с помощью ориентации камеры.

| < Назад | Начало | Далее > |
|-|-|-|
| [02. Мышь][02.Mouse] | [Самоучители][index] | [04. Выбор узла][04.Selection] |

[en]: README.md

[index]: ../README-ru.md
[02.Mouse]: ../02.Mouse/README-ru.md
[04.Selection]: ../04.Selection/README-ru.md

[run-sphere]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUp
[run-spheres]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUpCgpsb2NhbCBzcGhlcmVSaWdodCA9IG5vZGVzOmNyZWF0ZVNwaGVyZSgiYW5vdGhlciIsIDEpCnJvb3Q6YWRkQ2hpbGQoc3BoZXJlUmlnaHQpCnNwaGVyZVJpZ2h0LnBvc2l0aW9uID0gezIsIDAsIDB9
[run-camera]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUpCgpsb2NhbCBzcGhlcmVSaWdodCA9IG5vZGVzOmNyZWF0ZVNwaGVyZSgiYW5vdGhlciIsIDEpCnJvb3Q6YWRkQ2hpbGQoc3BoZXJlUmlnaHQpCnNwaGVyZVJpZ2h0LnBvc2l0aW9uID0gezIsIDAsIDB9Cgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQoKbG9jYWwgcG9zID0gY2FtZXJhLnBvc2l0aW9uCnByaW50KCJDYW1lcmEgcG9zaXRpb246IiwgcG9zWzFdLCBwb3NbMl0sIHBvc1szXSkKbG9jYWwgcm90ID0gY2FtZXJhLnJvdGF0aW9uCnByaW50KCJDYW1lcmEgcm90YXRpb246Iiwgcm90WzFdLCByb3RbMl0sIHJvdFszXSk=
[run-two]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCgpsb2NhbCBzcGhlcmUgPSBub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKcm9vdDphZGRDaGlsZChzcGhlcmUpCgpsb2NhbCBzcGhlcmVSaWdodCA9IG5vZGVzOmNyZWF0ZVNwaGVyZSgiYW5vdGhlciIsIDEpCnJvb3Q6YWRkQ2hpbGQoc3BoZXJlUmlnaHQpCnNwaGVyZVJpZ2h0LnBvc2l0aW9uID0gezIsIDAsIDB9Cgpsb2NhbCBjYW1lcmEgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYQoKY2FtZXJhLnBvc2l0aW9uID0gezAsIC0zMCwgMH0KY2FtZXJhLnJvdGF0aW9uID0gezkwLCAwLCAwfQ==
