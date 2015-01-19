---
layout: post
category : computing
title: "A simple python webserver"
tagline: ""
tags : [python]
last_modified: 2015-1-19
---

{: .alert .alert-warning}
The command has been changed in Python 3: `python -m http.server`.

Python has a very simple web server which allows you to share a particular directory with a one line command.
    
    python -m SimpleHTTPServer 8000
    
Index directory can be then accessed by http://\<ip address\>:8000.
<!--more-->
More complicated usages: [Only serve on localhost](http://www.linuxjournal.com/content/tech-tip-really-simple-http-server-python)

```python
import sys
import BaseHTTPServer
from SimpleHTTPServer import SimpleHTTPRequestHandler

HandlerClass = SimpleHTTPRequestHandler
ServerClass = BaseHTTPServer.HTTPServer
Protocol = "HTTP/1.0"

if sys.argv[1:]:
port = int(sys.argv[1])
else:
port = 8000
server_address = ('127.0.0.1', port)

HandlerClass.protocol_version = Protocol
httpd = ServerClass(server_address, HandlerClass)

sa = httpd.socket.getsockname()
print "Serving HTTP on", sa[0], "port", sa[1], "..."
httpd.serve_forever()
```


and [Simple Python Webserver to save file](http://stackoverflow.com/questions/13146064/simple-python-webserver-to-save-file)

```python
from os import curdir
from os.path import join as pjoin

from http.server import BaseHTTPRequestHandler, HTTPServer

class StoreHandler(BaseHTTPReque stHandler):
store_path = pjoin(curdir, 'store.json')

def do_GET(self):
if self.path == '/store.json':
with open(self.store_path) as fh:
self.send_response(200)
self.send_header('Content-type', 'text/json')
self.end_headers()
self.wfile.write(fh.read().encode())

def do_POST(self):
if self.path == '/store.json':
length = self.headers['content-length']
data = self.rfile.read(int(length))

with open(self.store_path, 'w') as fh:
fh.write(data.decode())

self.send_response(200)

server = HTTPServer(('', 8080), StoreHandler)
server.serve_forever()
```
