
## Production Ready Flask App - Part I

Notes from Miguel Grinberg's talk on making a production flask app.

PyCon 2016 - 20160528 0900 PST

Presentation URL: Miguel will put a URL in the github readme and tweet the link.


### 1. Move utility functions to utils.py (tag: v0.2)

url_for, timestamp functions.


### 2. Refactor database models. (tag: v0.3)

Avoid cyclic dependency of importing db from controller then importing model from models.py

Add a check for __main__ in models.py, if there isn't a main then fallback to ugly hardcoded "from flack import db".


### 3. Create an Application Package (tag: v0.4) - Use Flask-Script

A newer option exists over Flask-Script but is not yet production ready.

Flask-Script is available now: 
https://flask-script.readthedocs.io/en/latest/

See `git diff v0.3 v0.4` between these two tags to understand necessary changes.


### 4. Refactoring API Authentication (tag: v0.5) - 

Moved auth stuff to auth.py.  There were three auth functions finally imported.

Again see `git diff v0.4 v0.5` for details.


### 5. Refactoring Tests (tag: v0.6) - Change to a package style folder structure.

To get the overview, checkout this tag and manage.py. Look at file structure.

Now we are in a django style construction. `tests` folder exists alongside `flack` folder.


### 6. Refactoring Configuration (tag: v0.7) - Add a config.py next to manage.py.

Add a config.py. This is pretty hairy even in django.

People solve configuration in different ways. 

I have a pretty good django dev.cfg/prod.cfg pattern that I would use here.


### 7. Create an `API Blueprint` - separate the api.

Create: `flack/api.py`.  Use a Blueprint.  Blueprint is initialized where app creation is done, currently flack.py.


### 8. Create Stats package.

See `git diff v0.8 v0.9`


### 9. Using an application Factory Function (tag: v0.10) - use a Blueprint for app.

>>> Sometimes it is desirable to work with more than one application
>>> Best Example: Unit tests that need applications with different configurations.

#### SPECIAL NOTE:

Having app blueprints allows you to have a really elegant test setup and teardown.

#### Howto get the Blueprint working (see `git diff v0.9 v.10` for exact code)

We need to get rid of app because it will exist outside the context of the controller.

Now we can no longer reference app.  
We must refactor app.config and other references to app.
That means no app.debug.

To achieve this we can use a Blueprint.
Use the current_app context variable to access application.

Put application factory function in __init__.py, see create_app function here.

To create an app you now call create_app, pass an application name, and get the app.

SQLAlchemy needs the models in __init__.py because it introspects on the app.
You can miss this and maybe the models get imported elsewhere but that is sloppy.


### 10. Creating an API Package (tag: v0.11) - Turn api.py into a package.

This is a simple step, make an api folder and break the components of api.py down into the 3 files/modules: tokens, messages, users.

tokens, messages, users become modules inside of the api package.



## Part 2 - Scaling Flask for Production.

Notes from Miguel Grinberg's talk on making a production flask app.

PyCon 2016 - 20160528 0900 PST

Presentation URL: Miguel will put a URL in the github readme and tweet the link.


### Scaling Web Servers

Problem - one request at a time.  Not great.

#### Multiple Threads

Limited use of multiple threads because of GIL.  Not really great.


#### Multiple processes

Obviously multiple apps sounds nice. Each process has its own set of things.

What about SQLAlchemy?


#### Green threads / coroutines - asyncio, gevent, eventlet.

Flask doesn't support asyncio.

Flask does support gevent, eventlet.

IO and standard library `threading` functions are incompatible.

How about manually triggering a switch? - `sleep` function to take a break and let other threads have a turn.

Note on gevent and eventlet -- A lot of people get this wrong on stack overflow. This stuff isn't for cpu intensive work. All green threads need a chance to run and CPU must be available or sleeps must run very often to let the scheduler switch.

Miguel's IO library is for this. Read more about this.  I have it in other notes but a google search will suffice.

Both eventlet and gevent allow monkeypatching to coroutine friendly functions (overwrite standard library function with the coroutine friendly function).


#### Using Production Web Servers (tag: v0.12) 

##### gunicorn

Limited load balancing - Why limited? I will have to look this up.

Written in Python - robust but not lightning fast

Supports multiple processes, and eventlet or gevent green threads.


##### uwsgi




##### nginx

Written in C.  

Ideal for serving static files in production. You expose the static file in the nginx config.


#### Bottlenecks: I/O Bound and CPU Bound

##### I/O Bottlenecks

Flack example: scraping links included in posts

Solution: concurrent request handlers through multiple threads, processes, or green threads.

Make I/O heavy requests asynchronous.

##### CPU Bottlenecks

Flack example: rendering posts from markdown to HTML

Solution: Offload CPU intensive requests to auxiliary threads or processes to keep the server unblocked.  Rephrased: make CPU intensive requests asynchronous.


#### Asynchronous HTTP Requests (tag: v0.13)

1. Request starts background work, gives a status 202.
2. Goes back to listening requests.
3. Location header has a status URL where the client can ask for status for the asynchronous task.
4. Request to status URL returns 202 while the request is still in progress.
5. When complete, (see presentation for details)

There is a decorator for this in `flack`, migue's app.... @async decorator.

That's all that is necessary!!!  This is almost too easy.

If you `git diff v0.12 v0.13` and view the tasks module, you can see async implemenation. 

note that `request.environ` has environmental information to build a request object.

This way miguel can build his own request object.

Miguel uses threading here, I think this won't matter because the threads are being used inside of a single request.

We went into great detail about the `@async` decorator code.  Miguel mentioned maybe he should test it more and build a flask extension out of it. Probably production ready but definitely not widely tested.

Async really gets into the guts of flask and does a lot of stuff flask does manually building the response etc. it looks good but it just isn't vetted and I don't know enough flask futs to vet it.


#### Celery Workers (tag: v0.14)

There's a wrapper in `manage.py`. Celery is integrated into the previous async section.

For quick setup `redis` works with Celery.

Celery needs to be available in __init__.py for the same reason as the model. Flask uses the context apparently.  There must be something else since flask doesn't really 'expect' celery.  Maybe celery is loaded up in the app then refers to stuff.. Still seems a little circular.


#### Websocket (tag: v0.15) - clients must 'poll' to stay up to date... we need to use 'server-push' to reduce load when new stuff happens.

This "server-push" websocket model will reduce load, removing all redundant quests.

The previous version used 2 requests per second per client just to stay up to date.

Options:
1. Streaming
2. Long-polling
3. WebSocket
4. Socket.IO (long-polling + WebSocket)

##### Streaming
One of Miguel Grinberg's Posts using Streaming (1): http://blog.miguelgrinberg.com/post/video-streaming-with-flask

##### Long polling 
client asks 'is there anything new?' but the server doesn't respond right away.  it waits maybe 10 seconds because nothing happened. it does block the thread but it doesn't respond until something changes or until the long poll times out. A new one can then be generated.

##### WebSocket 
HTML5 Standard. Not HTTP anymore. Both connections can write to the other side at any time. Any side can write/read at any time.

##### SocketIO
written in JS. Node.js service. SocketIO Protocol supports WebSocket and falls aback to long-polling if WebSocket isn't supported by the client.

`Type 1:`

Python client: use socketio.emit class in a push_model method.  See slides.
Javascript server: socketio node.js service

`Type 2:`

Python Server: @socketio.on() decorator
Javascript client: socket.emit(). See slides.


#### Even more Socket.IO.  We can now only use gevent or eventlet.

See the events.py module `git diff v0.14 v0.15`, added to manage events.

I'm pretty far afield of things I have actually done at this point so my thoughts aren't very helpful.

This code is starting to look a ton like django. However, I don't think Django has async built in either, so maybe this is a limit for out-of-the-box django as well. More research needed.

Need an auxiliary wsgi process for socketio. There is a second wsgi_aux.py or something in the source.

Miguel used eventlet.monkey_patch() to replace a bunch of stuff with eventlet counterparts. This seems pretty specific, better know what you are doing and read the monkey patch code.

`manage.py runserver` needs socketio stuff.  Socketio needs socketio.run, rather than app.run, so this gets added in. 

Also see tests. socketio has its own test client.

Finally nginx has requirements for load balancing. Nginx option "sticky sessions"

Grep the flack.conf in the nginx folder for `ip_hash` and read about this nginx option. Socketio is stateful and rest APIs are stateless so this option is necessary.


#### Flask-SocketIO

- Miguel's project
- Pure python, translation of the Socket.IO node project for flask.



##### Questions / Notes

- Flask has a Python profiler.

