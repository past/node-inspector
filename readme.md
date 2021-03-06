Node Inspector is a debugger interface for nodeJS using the WebKit Web Inspector.

## Getting Started

### Requirements

* [nodeJS](http://github.com/ry/node)
  - versions: 0.1.101 or later
* A WebKit based browser: Chrome, Safari, OmniWeb, etc.

### Setup

1. make a debug build of node
		./configure --debug
		make
		make install

If you get an error like: `Build failed: Missing node signature for...` try `make distclean` then try again.

### Debugging

There are two ways to use node-inspector. First I'll describe the easy way. 
As an example lets debug test/hello.js, from the root project directory (node-inspector)

1. start the inspector like this:
		node bin/inspector.js --start=test/hello.js

    > Note: --start path must be relative to the current working directory or absolute

2. open http://127.0.0.1:8080 in your favorite WebKit based browser

    > Chrome 5 users **MUST** use 127.0.0.1 **NOT** localhost or the browser will not connect to the debugger

3. you should now see the javascript source from nodeJS

4. set some breakpoints, see what happens


This will start a child process `node_g --debug test/hello.js` and host the inspector 
interface at http://localhost:8080. The other way is to connect the inspector to an 
external node process.

1. start a node process:
		node_g --debug=7878 test/hello.js
		
2. start the inspector:
		node bin/inspector.js --debug-port=7878 --web-port=8000

3. open http://127.0.0.1:8000

For more information on getting started see the [wiki](http://github.com/dannycoates/node-inspector/wiki/Getting-Started---from-scratch)

## Options

		--start=[file]        starts [file] in a child process with node_g --debug
		                      [file] path can be absolute or relative to $PWD
		--start-brk=[file]    same as start with --debug-brk
		--web-port=[port]     port to host the inspector (default 8080)
		--debug-port=[port]   v8 debug port to connect to (default 5858)
		--fwd-io              forward stdout and stderr from the child process to inspector console

## Extensions

This project started as a Chrome extension. For more info see the [wiki](http://github.com/dannycoates/node-inspector/wiki/Google-Chrome-Extension).

## Cool stuff

* the WebKit Web Inspector debugger is a great js debugger interface, it works just as well for node
* uses a WebSocket to connect to debug-agent, so no polling for breaks
* remote debugging
* javascript top to bottom :)

## Known Issues

This is alpha quality code, so use at your own risk:

* be careful about viewing the contents of Buffer objects, each byte is displayed as an individual array element, for anything but tiny Buffers this will take too long to render
* while not stopped at a breakpoint the console doesn't always behave as you might expect
* pause on exceptions doesn't play nice with the node event loop
* closing the inspector does not stop debugging, you must stop inspector.js manually

## TODOS

* save application settings
* profiler panel

## Thanks

This project respectfully uses code from and thanks the authors of:

* [WebKit](http://webkit.org/building/checkout.html)
* [node](http://github.com/ry/node)
* [node-websocket-server](http://github.com/miksago/node-websocket-server)
* [node-paperboy](http://github.com/felixge/node-paperboy)


