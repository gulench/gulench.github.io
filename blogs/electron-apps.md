# Electron Apps

## Cache related issues

When you *upgrade* the version of an application, the app fails to render itself and just shows an *empty window*. This happens with the [CodeceptUI](https://codecept.io/ui/) application.

One way to clear the cache is to do the following:

1. Press `CTRL+SHIFT+I`, to open the browser **developer console**
2. Go to the **Network** tab and press `CTRL+R` to refresh the page
3. Inside the **network requests** list, right-click and select *Clear browser cache*

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2Njc2NDgyMywyMDEwMzMxODQ2XX0=
-->