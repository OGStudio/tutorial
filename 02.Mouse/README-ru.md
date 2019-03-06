
[EN][en] | **RU**

| < Назад | Начало | Далее > |
|-|-|-|
| [01. Цвет фона][01.BackgroundColor] | [Самоучители][index] | [03. Сфера][03.Sphere] |

## 02. Мышь

В этом самоучителе мы задаём цвет фона на нажатие кнопок мыши.

Ориентировочное время выполнения: 5 минут.

## Содержание

* [Кнопки мыши](#buttons)
* [Переключение цвета фона](#toggle)
* [Итог](#summary)

<a name="buttons"/>

# Кнопки мыши

Давайте отследим нажатия и отпускания кнопок мыши:

```lua
local mouse = main.application.mouse
mouse.pressedButtonsChanged:addCallback(
    function()
        print("Mouse buttons have been pressed or released")
        print("Pressed buttons:", #mouse.pressedButtons)
    end
)
```
**[Запустить в `ogse`][run-buttons]**

Давайте взглянем на использованный нами API:

* `main.application.mouse` (экземпляр) позволяет получить текущие свойства
мыши (пальца) вроде позиции, нажатых кнопок мыши и подписаться на их
изменения
* `main.application.mouse.pressedButtons` (массив) содержит список нажатых
кнопок мыши
* `main.application.mouse.pressedButtonsChanged` (экземпляр `core::Reporter`)
уведомляет о нажатии и отпускании кнопок мыши
    * **для подписки** на все уведомления мы используем метод `addCallback()` экземпляра `core.Reporter`:
        ```lua
        main.application.mouse.pressedButtonsChanged:addCallback(
            function()
                print("Mouse buttons have been pressed or released")
            end
        )
        ```

**Замечания**:

* `pressedButtonsChanged` является экземпляром, который мы слушаем
* `addCallback()` является методом экземпляра `pressedButtonsChanged`
* `pressedButtonsChanged` и `addCallback` разделены `:`, т.к. это вызов метода
* `function() ... end` является функцией обратного вызова (замыканием),
исполняемым при получении каждого уведомления
* `#` является оператором, возвращающим количество элементов массива

Взгляните на консоль отладки. Вы должны увидеть примерно такой вывод при
нажатии кнопок мыши:

```
Mouse buttons have been pressed or released
Pressed buttons:    1
Mouse buttons have been pressed or released
Pressed buttons:    0
Mouse buttons have been pressed or released
Pressed buttons:    1
Mouse buttons have been pressed or released
Pressed buttons:    2
Mouse buttons have been pressed or released
Pressed buttons:    1
Mouse buttons have been pressed or released
Pressed buttons:    0
```

<a name="toggle"/>

# Переключение цвета фона

Давайте устанавливать красный цвет фона, когда нажата хотя бы одна кнопка мыши,
и возвращать цвет фона к значению `0.2, 0.2, 0.4`, если ни одна из кнопок мыши
не нажата:

```lua
local DEFAULT_COLOR = {0.2, 0.2, 0.4}
local PRESSED_COLOR = {1.0, 0.0, 0.0}

local mouse = main.application.mouse
local camera = main.application.camera

mouse.pressedButtonsChanged:addCallback(
    function()
        if (#mouse.pressedButtons > 0)
        then
            camera.clearColor = PRESSED_COLOR
        else
            camera.clearColor = DEFAULT_COLOR
        end
    end
)
```
**[Запустить в `ogse`][run-toggle]**

Теперь цвет фона красный при удеражинии кнопки (кнопок) мыши.

<a name="summary"/>

# Итог

Вы успешно отследили нажатия кнопок мыши и переключили цвет фона.

| < Назад | Начало | Далее > |
|-|-|-|
| [01. Цвет фона][01.BackgroundColor] | [Самоучители][index] | [03. Сфера][03.Sphere] |

[en]: README.md

[index]: ../README-ru.md
[01.BackgroundColor]: ../01.BackgroundColor/README-ru.md
[03.Sphere]: ../03.Sphere/README-ru.md

[run-buttons]: https://ogstudio.github.io/ogse/?base64code=bG9jYWwgbW91c2UgPSBtYWluLmFwcGxpY2F0aW9uLm1vdXNlCm1vdXNlLnByZXNzZWRCdXR0b25zQ2hhbmdlZDphZGRDYWxsYmFjaygKICAgIGZ1bmN0aW9uKCkKICAgICAgICBwcmludCgiTW91c2UgYnV0dG9ucyBoYXZlIGJlZW4gcHJlc3NlZCBvciByZWxlYXNlZCIpCiAgICAgICAgcHJpbnQoIlByZXNzZWQgYnV0dG9uczoiLCAjbW91c2UucHJlc3NlZEJ1dHRvbnMpCiAgICBlbmQKKQ==
[run-toggle]: https://ogstudio.github.io/ogse/?base64code=bG9jYWwgREVGQVVMVF9DT0xPUiA9IHswLjIsIDAuMiwgMC40fQpsb2NhbCBQUkVTU0VEX0NPTE9SID0gezEuMCwgMC4wLCAwLjB9Cgpsb2NhbCBtb3VzZSA9IG1haW4uYXBwbGljYXRpb24ubW91c2UKbG9jYWwgY2FtZXJhID0gbWFpbi5hcHBsaWNhdGlvbi5jYW1lcmEKCm1vdXNlLnByZXNzZWRCdXR0b25zQ2hhbmdlZDphZGRDYWxsYmFjaygKICAgIGZ1bmN0aW9uKCkKICAgICAgICBpZiAoI21vdXNlLnByZXNzZWRCdXR0b25zID4gMCkKICAgICAgICB0aGVuCiAgICAgICAgICAgIGNhbWVyYS5jbGVhckNvbG9yID0gUFJFU1NFRF9DT0xPUgogICAgICAgIGVsc2UKICAgICAgICAgICAgY2FtZXJhLmNsZWFyQ29sb3IgPSBERUZBVUxUX0NPTE9SCiAgICAgICAgZW5kCiAgICBlbmQKKQ==
