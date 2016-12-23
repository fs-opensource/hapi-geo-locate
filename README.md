# hapi-geo-locate
A hapi plugin to geo locate requests by IP and provide `request.location` in your route handlers. The plugin uses [ipinfo.io](http://ipinfo.io/) for the IP geo location.


## Usage
The most straight forward way to register the `hapi-geo-locate` plugin: 

```
server.register(require('hapi-geo-locate'), (err) => {
    if (err) {
        // handle plugin registration error
    }
    
    // went smooth like chocolate :)
})

// Within your route handler functions, you can access the location like this
server.route({
    method: 'GET',
    path: '/',
    handler: (request, reply) => {
        const location = request.location
        // use client location
        
        reply(request.location)
    }
})
```


## Plugin Registration Options
The following plugin options allow you to customize the default behavior of `hapi-geo-locate`:

- **disabledByDefault**: `(boolean)`, default: `false` — by default, the plugin geo locates the request by IP on every request

```
server.register({
    require('hapi-geo-locate'),
    options: {
        disabledByDefault: true
    }
}, (err) => {
    // …
})

// Within your route handler functions, you can access the location like this
server.route({
    method: 'GET',
    path: '/',
    handler: (request, reply) => {
        const location = request.location // will be undefined
        reply(location)
    }
})
```


# Plugin Route Handler Options
The following plugin options allow you to customize the behavior of `hapi-geo-locate` on individual route handlers:

- **enabled**: `(boolean)` — tells the plugin to enable (`true`) or disable (`false`) geo location for the request by IP

The plugin configuration can be customized using the `hapiGeoLocation` (plugin name in camelCase) key:

```
server.register({
    require('hapi-geo-locate'),
    options: {
        disabledByDefault: true
    }
}, (err) => {
    // …
})

// Within your route handler functions, you can access the location like this
server.route({
    method: 'GET',
    path: '/',
    handler: (request, reply) => {
        const location = request.location
        // use the location
        
        reply(location)
    },
    config: {
        plugins: {
            hapiGeoLocate: {
                enabled: true
            }
        }
    }
})
```


## Links

- [hapi tutorial series](https://futurestud.io/tutorials/hapi-get-your-server-up-and-running)


---

> [futurestud.io](https://futurestud.io) &nbsp;&middot;&nbsp;
> GitHub [@fs-opensource](https://github.com/fs-opensource/) &nbsp;&middot;&nbsp;
> Twitter [@futurestud_io](https://twitter.com/futurestud_io)