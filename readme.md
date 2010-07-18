Node Inspector is an debugger interface for nodeJS using the WebKit Web Inspector as a Google Chrome extension.

## Getting Started

### Requirements

* Google Chrome (or Chromium)
  - version 6.0.466.0 or later for context menu support
    - http://www.chromium.org/getting-involved/dev-channel
* nodeJS - http://github.com/ry/node
  - versions: 0.1.100 - 0.1.101

### Setup

1. make a debug build of node
    > ./configure --debug
    > make
    > make install

2. start Chrome

  To use context menus (for conditional breakpoints, etc.) start Chrome with:
    > --enable-experimental-extension-apis
    
  OR to disable context menus
    > remove "experimental" from /front-end/mainfest.json

3. enable Developer mode from the Chrome extensions page

4. load unpacked extension
    > open node-inspector/front-end
    
    You should now see a yellow triangle next to your address bar

### Debugging

1. start a node project with debugging, for example:
    > node_g --debug test/hello.js

2. start the debug-agent
    > node bin/debug-agent.js

3. open nodeJS Inspector

4. you should now see the javascript source from nodeJS

5. set some breakpoints, see what happens


## Cool stuff

* the WebKit Web Inspector debugger is a great js debugger interface, most it works just as well for node
* uses a WebSocket to connect to debug-agent, so no polling for breaks
* javascript top to bottom :)

## Known Issues

This pre-alpha quality code, so use at your own risk:

* while not stopped at a breakpoint the console doesn't always behave as you might expect
* hovering the mouse over the arguments of the wrapper function will crash node
* pause on exceptions doesn't play nice with the node event loop
* closing the inspector does not stop debugging, you must stop debug-agent.js manually
* opening the inspector more than once causes trouble
* connection info to debug-agent is hard coded to 127.0.0.1:8080

## Other Ideas

* most, if not all of the extension features could be served as a static site,
  which could allow you to host the debugger from a website.
* the debug-agent could be extended to provide collaborative debugging with
  multiple inspectors connected to the same debug session.
* use a native node extension instead of the debug-agent.js as a separate process

## TODOS

* save application settings
* single instance only
* debug-agent needs a lot of work
* try out live edit
* separate source into WebKit and custom code sections