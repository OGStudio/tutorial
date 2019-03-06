
[EN][en] | **RU**

| < Назад | Начало | Далее > |
|-|-|-|
| Не доступно | [Самоучители][index] | [02. Мышь][02.Mouse] |

## 01. Цвет фона

В этом самоучителе мы начинаем обучениe с установки цвета фона.

Ориентировочное время выполнения: 5 минут.

## Содержание

* [Красный фон](#red)
* [Вывод цвета фона по умолчанию](#print)
* [Итог](#summary)

<a name="red"/>

# Красный фон

Такова строка кода для установки красного фона:

```lua
main.application.camera.clearColor = {1, 0, 0}
```
**[Запустить в `ogse`][run-red]**

**Внимание**: либо скопируйте код в `ogse` самостоятельно, либо нажмите **Запустить в `ogse`**.

Давайте взглянем на использованный нами API:

* `main` (пространство имён) содержит экземпляр приложения `application`
* `main.application` (экземпляр) содержит подсистемы вроде `camera` (камера), `mouse` (мышь) и т.д.
* `main.application.camera` (экземпляр) является "окном" в сцену приложения
* `main.application.camera.clearColor` (свойство) является очищающим цветом (фактически цветом фона) камеры
    * **принимает** массив компонент цвета в формате RGB
        ```lua
        main.application.camera.clearColor = {1, 0, 0}
        ```
    * **возвращает** массив компонент цвета в формате RGB
        ```lua
        local color = main.application.camera.clearColor
        print("background color:", color[1], color[2], color[3])
        ```

<a name="print"/>

# Вывод цвета фона по умолчанию

Установить цвет фона оказалось довольно легко, правда? Теперь узнаем
цвет фона по умолчанию:

```lua
local color = main.application.camera.clearColor
print("Default background color:", color[1], color[2], color[3])
```
**[Запустить в `ogse`][run-print]**

**Замечания**:

* ключевое слово `local` означает, что объявленная переменная локальна лишь
для текущей области видимости и будет собрана сборщиком мусора при выходе
из этой области
* `Lua` индексирует массив с `1`, а не с `0` как `C`

Взгляните на консоль отладки. Вы должны увидеть следующую строку:

```
Default background color:  0.200000    0.200000    0.400000
```

Таким образом, цветом фона по умолчанию является `0.2, 0.2, 0.4`. Почему?
Потому что `0.2, 0.2, 0.4` является цветом фона по умолчанию для
библиотеки `OpenSceneGraph`, используемой `ogs`.

<a name="summary"/>

# Итог

Вы успешно установили цвет фона и вывели цвет фона по умолчанию.

| < Назад | Начало | Далее > |
|-|-|-|
| Не доступно | [Самоучители][index] | [02. Мышь][02.Mouse] |

[en]: README.md

[index]: ../README-ru.md
[02.Mouse]: ../02.Mouse/README-ru.md

[run-red]: http://ogstudio.github.io/ogse/?base64code=bWFpbi5hcHBsaWNhdGlvbi5jYW1lcmEuY2xlYXJDb2xvciA9IHsxLCAwLCAwfQ==
[run-print]: https://ogstudio.github.io/ogse/?base64code=bG9jYWwgY29sb3IgPSBtYWluLmFwcGxpY2F0aW9uLmNhbWVyYS5jbGVhckNvbG9yCnByaW50KCJEZWZhdWx0IGJhY2tncm91bmQgY29sb3I6IiwgY29sb3JbMV0sIGNvbG9yWzJdLCBjb2xvclszXSk=
