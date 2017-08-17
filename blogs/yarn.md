# Yarn Package Manager

## Installing packages globally
Yarn tries to put the launching script inside the directory where the node executable resides. While installing the `ember-cli` globally, yarn tried to copy the `ember.cmd` script to `C:\Program Files\nodejs\ember.cmd` and the following error was encountered:
```
Error: EPERM: operation not permitted, open 'C:\Program Files\nodejs\ember.cmd'
```

**NOTE**: To avoid the error and be able to install global packages as a normal user, set the `prefix` property in your `yarn` configuration:

```
yarn config set prefix %LOCALAPPDATA%\Yarn\bin
```

The other interesting thing is that yarn's MSI installer included the directory `%LOCALAPPDATA%\Yarn\bin` in the `PATH` environment variable. Not everything that you install globally do not end up in this directory, for example, `ember-cli`.

The location where yarn always put the scripts is `%LOCALAPPDATA%\Yarn\config\global\node_modules\.bin`

In Linux, it is
`$HOME/.config/yarn/global/node_modules/.bin`

Some versions of Yarn also tried to install the scripts in the `nodejs` installation directory; for example in Windows, `C:\Program Files\nodejs\`, like the one shown below:

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

## Using yarn with Angular

```
yarn global add @angular/cli

ng set --global packageManager=yarn

ng new my-app

cd my-app; yarn start
```

## Using yarn with Glimmer JS

NOTE: You need to pass the Git repository URL instead of the `@glimmerjs/blueprint` package name: `https://github.com/glimmerjs/glimmer-blueprint.git`.
```
%LOCALAPPDATA%\Yarn\config\global\node_modules\.bin\ember.cmd new first-app -b https://github.com/glimmerjs/glimmer-blueprint.git --yarn true

cd first-app

ember serve
```

## `yarn.lock` File

After you run `yarn` in a project directory, it creates a file called `yarn.lock`; this file contains a *resolved* list of the **project's dependencies**. If you update the project's dependencies with yarn, this file gets updated accordingly. You may check in this file into version control.

> Written with [StackEdit](https://stackedit.io/).