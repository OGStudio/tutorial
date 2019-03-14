
[EN][en] | **RU**

Этот документ является частью [программы обучения OGStudio][education].

Самоучители описывают создание (и распространение) простой игры с
помощью `ogs` за считанные часы.

# Инструменты

Нашим основным инструментом является `ogse`
([http://ogstudio.github.io/ogse](https://ogstudio.github.io/ogse)),
минималистичный редактор:

![screen-editor]

Слева:

* кнопка для выполнения кода
* редактор кода

Справа:

* окно отображения результата выполнения кода
* отладочная консоль для вывода ценной информации

`ogse` использует `ogs`, инструмент для создания кросс-платформенных игр 3D.
`ogs` использует язык `Lua` для скриптов.

**Внимание**: ваш [веб-браузер должен иметь поддержку `WebGL`][webgl], чтобы
суметь выполнить примеры кода.

# Самоучители

**Внимание**: курс находится в разработке, поэтому список самоучителей ещё не окончательный.

| Самоучитель | Описание | Ориентировочное время выполнения | Новый API |
|-|-|-|-|
| [01. Цвет фона][01.BackgroundColor] | Установка цвета фона | 5 минут | <ol><li>`main`</li><li>`main.application`</li><li>`main.application.camera`</li><li>`main.application.camera.clearColor`</li><ol> |
| [02. Мышь][02.Mouse] | Установка цвета фона на нажатие кнопок мыши | 5 минут | <ol><li>`main.application.mouse`</li><li>`main.application.mouse.pressedButtons`</li><li>`main.application.mouse.pressedButtonsChanged`</li><li>`core`</li><li>`core.Reporter`</li><li>`core.Reporter:addCallback()`</li></ol> |
| [03. Сферы][03.Spheres] | Отображение сфер | 10 минут | <ol> <li>`main.application.nodes`</li> <li>`main.application.nodes:createSphere()`</li> <li>`main.application.nodes:node()`</li> <li>`scene`</li> <li>`scene.Node:addChild()`</li> <li>`scene.Node.position`</li> <li>`main.application.camera.position`</li> <li>`main.application.camera.rotation`</li> </ol> |
| [04. Выбор узла][04.Selection] | Выбор сфер | 10 минут | <ol> <li>`scene.Node:setMask()`</li> <li>`main.application.camera:nodeAtPosition()`</li> <li>`scene.Node.__name`</li> </ol> |

[en]: README.md

[education]: http://opengamestudio.org/pages/education.html
[01.BackgroundColor]: 01.BackgroundColor/README-ru.md
[02.Mouse]: 02.Mouse/README-ru.md
[03.Spheres]: 03.Spheres/README-ru.md
[04.Selection]: 04.Selection/README-ru.md

[screen-editor]: ogse.png
[webgl]: https://get.webgl.org
