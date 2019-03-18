
[EN][en] | **RU**

| < Назад | Начало | Далее > |
|-|-|-|
| [04. Выбор узла][04.Selection] | [Самоучители][index] | [06. ??][06.??] |

## 05. Материал

В этом самоучителе мы научимся отображать сферу в цвете.

Ориентировочное время выполнения: 10 минут.

## Содержание

* [Сфера](#sphere)
* [Красный цвет](#red)
* [Переключение цвета сферы](#toggle)
* [Итог](#summary)

<a name="sphere"/>

# Сфера

Давайте отобразим сферу:

```lua
local nodes = main.application.nodes
local root = nodes:node("root")
local sphere = nodes:createSphere("sphere", 1)
root:addChild(sphere)
```
**[Run in `ogse`][run-sphere]**

<a name="red"/>

# Красный цвет

Давайте сделаем сферу красной.

**Добавьте** следующий код:

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

Мы определили шейдеры GLSL, которые отображают всё в красном, после чего
использовали их для создания материала сферы.

Взглянем на новый использованный нами API:

* `main.application.materials` (экземпляр) содержит материалы, определяющие внешний вид узлов
* `main.application.materials:createMaterial()` (метод)
    * **принимает** название материала для создания
    * **возвращает** новый экземпляр `render.Material`
        ```lua
        local material = main.application.materials:createMaterial("outfit")
        ```
* `render.Material:setShaders()` (метод)
    * **принимает** вершинный и фрагментный шейдеры GLSL
        ```lua
        local vertexShader = "void main() { gl_Position = gl_ModelViewProjectionMatrix * gl_Vertex; }"
        local fragmentShader = "void main() { gl_FragColor = vec4(1, 0, 0, 1); }"
        material:setShaders(vertexShader, fragmentShader)
        ```
* `scene.Node:setMaterial()` (метод)
    * **принимает** экземпляр материала, чтобы определить внешний вид узла
        ```lua
        node:setMaterial(material)
        ```

**Замечания**:

* `[[` и `]]` позволяют расположить строку на нескольких строках
* `plainVertexShader` переводит каждую вершину узла из объектного/модельного
пространства в экранное, чтобы сделать этот узел видимым на экране
* `colorFragmentShader` отображает все фрагменты (узла) в красном цвете

<a name="toggle"/>

# Переключение цвета сферы

Давайте переключать цвет сферы между красным и зелёным на нажатие мыши:

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

Теперь сфера зелёная во время удержания кнопки мыши.

Взглянем на новый использованный нами API:

* `render.Material:setUniform()` (метод)
    * **принимает** названием и значение uniform
        ```lua
        material:setUniform("color", {1, 0, 0})
        ```

**Замечания**:

* uniform позволяет передавать значение из кода в шейдер
* `precision highp float` (строка) необходима для GLES (WebGL), чтобы задать
точность всех чисел с плавающей точкой

<a name="summary"/>

# Итог

Вы успешно отобразили сферу в цвете.

| < Назад | Начало | Далее > |
|-|-|-|
| [04. Выбор узла][04.Selection] | [Самоучители][index] | [06. ??][06.??] |

[en]: README.md

[index]: ../README-ru.md
[04.Selection]: ../04.Selection/README-ru.md
[06.??]: ../06.??/README-ru.md

[run-sphere]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKbG9jYWwgc3BoZXJlID0gbm9kZXM6Y3JlYXRlU3BoZXJlKCJzcGhlcmUiLCAxKQpyb290OmFkZENoaWxkKHNwaGVyZSk=
[run-red]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKbG9jYWwgc3BoZXJlID0gbm9kZXM6Y3JlYXRlU3BoZXJlKCJzcGhlcmUiLCAxKQpyb290OmFkZENoaWxkKHNwaGVyZSkKCmxvY2FsIHBsYWluVmVydGV4U2hhZGVyID0gW1sKdm9pZCBtYWluKCkKewogICAgZ2xfUG9zaXRpb24gPSBnbF9Nb2RlbFZpZXdQcm9qZWN0aW9uTWF0cml4ICogZ2xfVmVydGV4Owp9Cl1dCmxvY2FsIGNvbG9yRnJhZ21lbnRTaGFkZXIgPSBbWwp2b2lkIG1haW4oKQp7CiAgICBnbF9GcmFnQ29sb3IgPSB2ZWM0KDEsIDAsIDAsIDEpOwp9Cl1dCgpsb2NhbCBtYXRlcmlhbCA9IG1haW4uYXBwbGljYXRpb24ubWF0ZXJpYWxzOmNyZWF0ZU1hdGVyaWFsKCJyZWQiKQptYXRlcmlhbDpzZXRTaGFkZXJzKHBsYWluVmVydGV4U2hhZGVyLCBjb2xvckZyYWdtZW50U2hhZGVyKQpzcGhlcmU6c2V0TWF0ZXJpYWwobWF0ZXJpYWwp
[run-toggle]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgbm9kZXMgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzCmxvY2FsIHJvb3QgPSBub2Rlczpub2RlKCJyb290IikKbG9jYWwgc3BoZXJlID0gbm9kZXM6Y3JlYXRlU3BoZXJlKCJzcGhlcmUiLCAxKQpyb290OmFkZENoaWxkKHNwaGVyZSkKCmxvY2FsIHBsYWluVmVydGV4U2hhZGVyID0gW1sKdm9pZCBtYWluKCkKewogICAgZ2xfUG9zaXRpb24gPSBnbF9Nb2RlbFZpZXdQcm9qZWN0aW9uTWF0cml4ICogZ2xfVmVydGV4Owp9Cl1dCmxvY2FsIGNvbG9yRnJhZ21lbnRTaGFkZXIgPSBbWwojaWZkZWYgR0xfRVMKICAgIHByZWNpc2lvbiBoaWdocCBmbG9hdDsKI2VuZGlmCgp1bmlmb3JtIHZlYzMgY29sb3I7Cgp2b2lkIG1haW4oKQp7CiAgICBnbF9GcmFnQ29sb3IgPSB2ZWM0KGNvbG9yLCAxKTsKfQpdXQoKbG9jYWwgbWF0ZXJpYWwgPSBtYWluLmFwcGxpY2F0aW9uLm1hdGVyaWFsczpjcmVhdGVNYXRlcmlhbCgibWFueSIpCm1hdGVyaWFsOnNldFNoYWRlcnMocGxhaW5WZXJ0ZXhTaGFkZXIsIGNvbG9yRnJhZ21lbnRTaGFkZXIpCnNwaGVyZTpzZXRNYXRlcmlhbChtYXRlcmlhbCkKCmxvY2FsIENPTE9SX1JFRCA9IHsxLCAwLCAwfQpsb2NhbCBDT0xPUl9HUkVFTiA9IHswLCAxLCAwfQotLSBEZWZhdWx0IGNvbG9yLgptYXRlcmlhbDpzZXRVbmlmb3JtKCJjb2xvciIsIENPTE9SX1JFRCkKLS0gVG9nZ2xlIGNvbG9yLgpsb2NhbCBtb3VzZSA9IG1haW4uYXBwbGljYXRpb24ubW91c2UKbW91c2UucHJlc3NlZEJ1dHRvbnNDaGFuZ2VkOmFkZENhbGxiYWNrKAogICAgZnVuY3Rpb24oKQogICAgICAgIGlmICgjbW91c2UucHJlc3NlZEJ1dHRvbnMgPiAwKQogICAgICAgIHRoZW4KICAgICAgICAgICAgbWF0ZXJpYWw6c2V0VW5pZm9ybSgiY29sb3IiLCBDT0xPUl9HUkVFTikKICAgICAgICBlbHNlCiAgICAgICAgICAgIG1hdGVyaWFsOnNldFVuaWZvcm0oImNvbG9yIiwgQ09MT1JfUkVEKQogICAgICAgIGVuZAogICAgZW5kCik=
