# Asynchronous Programming

Ok, lets try to creat somethign here. Lets start with Promises.

Lets assume you need to get information about several widgets.

## Promises
We can use promises to get the widgets.

``` javascript
Promise.all(widgetIds.map((id) => new Promise(...)))
.then(widgets => {
    // this will only happen if everything comes back without an error.
})
.catch(() => {
    // this will happen if any of the calls come back with an error
})
.finally(() => {
    // this will always happen.
})
```

Now the problem with this is that if any of them error the whole thing is caught and handled as an error. Perhaps a better way to handl this is this.

``` javascript
Promise.allSettled(widgetIds.map((id) => new Promise(...)))
.then(results => {
    const widgets = results.filter(({status}) => status === 'fulfilled')
    const brokenWidgets = results.filter(({status}) => status === 'rejected')
})
```

With Promise.allSettled we can get the calls that worked and handle the ones that didn't more easaly.

## Async/Await
Lets try using async and await.

Now to do this we need to use a async fucntion.

``` javascript
async function getWidgets(widgetIds = []) {
    async function getWidgetById(id) {
        // get widget
    }

    const widgets = await widgetIds.map(getWidgetById)
    //handle widgets here.
}
```

## mixed

Remember you can mix and match.

``` javascript
async function getWidgets(widgetIds = []) {
    async function getWidgetById(id) {
        // get widget
    }

    const response = await widgetIds.map(getWidgetById)
    //handle widgets here.
    return widgets
}

getWidgets(ids).then(() => {})
```
