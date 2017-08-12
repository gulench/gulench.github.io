# Yarn Package Manager

## Installing packages globally
Yarn tries to put the launching script inside the directory where the node executable resides. While installing the `ember-cli` globally, yarn tried to copy the `ember.cmd` script to `C:\Program Files\nodejs\ember.cmd` and the following error was encountered:
```
Error: EPERM: operation not permitted, open 'C:\Program Files\nodejs\ember.cmd'
```

The other interesting thing is that yarn's MSI installer included the directory `%LOCALAPPDATA%\Yarn\.bin` in the `PATH` environment variable.

The location where yarn actually put the scripts is `%LOCALAPPDATA%\Yarn\config\global\node_modules\.bin`

In Linux, it is
`$HOME/.config/yarn/global/node_modules/.bin`

**`C:\Program Files\nodejs\yo.cmd`**
```
@"%~dp0\..\..\Users\gulen\AppData\Local\Yarn\config\global\node_modules\.bin\yo.cmd"   %*
```

**`C:\Users\gulen\AppData\Local\Yarn\config\global\node_modules\.bin\yo.cmd`**
```
@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\..\yo\lib\cli.js" %*
) ELSE (
  @SETLOCAL
  @SET PATHEXT=%PATHEXT:;.JS;=;%
  node  "%~dp0\..\yo\lib\cli.js" %*
)
```

> Written with [StackEdit](https://stackedit.io/).