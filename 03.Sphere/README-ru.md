
[EN][en] | **RU**

| < Назад | Начало | Далее > |
|-|-|-|
| [02. Мышь][02.Mouse] | [Самоучители][index] | [04. ??][04.??] |

## 03. Сфера

В этом самоучителе мы отобразим сферу.

Ориентировочное время выполнения: 5 минут.

## Содержание

* [Сфера](#sphere)
* [Итог](#summary)

<a name="sphere"/>

# Сфера

Давайте отобразим сферу:

```lua
local sphere = main.application.nodes:createSphere("sphere", 1)
local root = main.application.nodes:node("root")
root:addChild(sphere)
```
**[Запустить в `ogse`][run-sphere]**

Взглянем на использованный нами API:

* `main.application.nodes` (экземпляр) содержит узлы сцены (необязательно видимые)
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

<a name="summary"/>

# Итог

Вы успешно отобразили сферу.

| < Назад | Начало | Далее > |
|-|-|-|
| [02. Мышь][02.Mouse] | [Самоучители][index] | [04. ??][04.??] |

[en]: README.md

[index]: ../README-ru.md
[02.Mouse]: ../02.Mouse/README-ru.md
[03.Sphere]: ../03.Sphere/README-ru.md

[run-sphere]: https://ogstudio.github.io/ogse/?base64script=bG9jYWwgc3BoZXJlID0gbWFpbi5hcHBsaWNhdGlvbi5ub2RlczpjcmVhdGVTcGhlcmUoInNwaGVyZSIsIDEpCmxvY2FsIHJvb3QgPSBtYWluLmFwcGxpY2F0aW9uLm5vZGVzOm5vZGUoInJvb3QiKQpyb290OmFkZENoaWxkKHNwaGVyZSk=
