
**EN** | [RU][ru]

| < Back | Tutorials | Next > |
|-|-|-|
| Not available | [Tutorials][index] | [1.2. Mouse][1.2.Mouse] |

# 1.1. Background color

In this tutorial we start education by learning to set background screen color.

Estimated completion time: ?? minutes.

# Table of contents

* [Editor](#editor)
* [Summary](#summary)

<a name="editor"/>

# Editor

`ogs` itself is a cross-platform tool, a library. However, to be able to
quickly check ideas or test code snippers, we provide an on-line editor
called `ogse`:

[https://ogstudio.github.io/ogse](https://ogstudio.github.io/ogse)

Open the link in your browser. You should see the following:

![screen-editor]




<a name="distribute"/>

# Distribute with GitHub Pages

In our case, the simplest game is just an empty render window.

Let's distribute the game with [GitHub Pages][github-pages].

| № | Action | Notes | Screenshot |
|-|-|-|-|
| 1. | Go to `Settings` | | ![screen-settings] |
| 2. | Select `master branch` as the source | Under `GitHub Pages` section | ![screen-source] |
| 3. | Hit `Save` | | ![screen-save] |
| 4. | Verify activation | | ![screen-activation] |
| 5. | Wait for publishing | | ![screen-published] |

<a name="index"/>

# Run the game

**Note**: your web browser **must** have [`WebGL` enabled and working][webgl].

![screen-index]

Click on the link `GitHub Pages` gave you. You should see an empty render window.

<a name="debug"/>

# Access debug console

![screen-debug]

Append `/debug.html` to the end of URL and hit `Enter` to access the same game with
debug console enabled.

Debug console is an important tool to debug your `ogstudio` games.

<a name="summary"/>

# Summary

You have successfully distributed web version of the simplest `ogstudio` game.
Now you can share the game with anyone who has more or less modern [web browser
with `WebGL` support][webgl].

| < Back | Tutorials | Next > |
|-|-|-|
| Not available | [Tutorials][index] | [1.2. Mouse][1.2.Mouse] |

[ru]: README-ru.md

[course]: ../README.md
[1.2.Mouse]: ../1.2.Mouse/README.md

[github-pages]: https://pages.github.com
[emscripten]: http://emscripten.org
[webgl]: https://get.webgl.org

[screen-settings]: readme/settings.png
[screen-source]: readme/source.png
[screen-save]: readme/save.png
[screen-activation]: readme/activation.png
[screen-published]: readme/published.png
[screen-index]: readme/screen-index.png
[screen-debug]: readme/screen-debug.png
