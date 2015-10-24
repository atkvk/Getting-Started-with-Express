# Getting-Started-with-Express
   There is a earlier version of tutorial for Express 3. Ignore that one.

## Section 1

### First express app
- Hello world


### The verbs

> Core feature of Express: **routing**


- [app].**all()**
- [app].get()
- [app].post()
- [app].put()
- [app].delete()


### Views and templates (Jade /EJS)

- Everything (passed to jade) is threated as JavaScript
- `` app.set('view engine', 'jade'); `` This seems not necessary any more


### Application settings

- Write settings  
  - app.set()
  - app.enable()
  - app.disable()
- Read settings
  - app.get() ** not the same as get routings**
  - app.enabled()
  - app.disabled()


- `` app.set('env', 'development');  // default: process.env.NODE_ENV``
- `` app.enable ('trust proxy') ``
- `` app.set('jsonp callback name', 'cb')``
-
	app.set('json replace', function(attr, val){
		if(attr === 'passwordHash'){
          return undefined;
        }
          return val;
      });  

- `` app.enable('case sensitive routing'); ``
- `` app.enable('strict routing');   // /hello !== /hello/ ``
- `` app.set('views', '[My_view_folder]'); ``
- `` app.set('view engine', 'jade'); ``
- `` app.enable('x-power-by');  // advertising for EXPRESS, will be sent in response header ``

## Section 2

### Middleware and request flow

- Category
  - Third-party middleware (bodyParser e.g.)
  - Custom middle ware;
  - Route function
  - Built-in middle  (express.static())

### Custom middleware based on route parameters

The middileware below get a user form database by name and attacht the user object to the request

    app.param('name', function(req, res, next, name){
      req.name = name[0].toUpperCase() + name.subString(1);

      Users.findOne({userName: name}, function(err, user){
        req.user = user;
        next();
        });
    }


### Grouping routes with **app.route()**

    app.route(workflows/:id)
        .get([callback])
        .put([callback])
        .delete([callback]);

### Router object (new in Express 4)

Why?
Allow modulize the code

Methods
  - use()
  - param()
  - verbs /all [get, post, put, delete, all]
  - route()

Examples: API versions routers.

## Section 3

### Request object

[Express API doc - Request](http://expressjs.com/4x/api.html#req.protocol)

- req.params.[myParameter]
- req.query.[myQueryString] // ../route?foo="xxx"
- req.body.[myFormValue]  // form value
- req.param('ATTR')  // This will check all the options above.


- req.route
- req.originalUrl
- req.cookies.ATTR
- req.get()
- req.accepts('text/html')

### Response object

[Express API doc - Response](http://expressjs.com/4x/api.html#res)

- res.status(200);
- res.set(header, value);
- res.get(header);

- res.cookie(name, value);
- res.clearCookie(name);

- res.redirect(status, path);
- res.send(status, text);
- res.json(status, object);
- res.jsonp(status, object);
- res.downloadFile(file);

### Formatting Response

    res.format({
      'text/plain': function(){ },
      'text/html': function(){ },
      'application/json': function(){ }
      });
