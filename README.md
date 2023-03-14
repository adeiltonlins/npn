# npn
webserver
  └── static
      ├── css
      ├── image
      └── script
      webserver
  ├── config.json
  ├── filehandler.js
  ├── index.js
  ├── package.json
  ├── server.js
  └── static
      ├── css
      ├── image
      └── script
      process.title = 'MyWebServer';
  1. var args = process.argv,
  2.   port = args[2] || 7070,
  3.   webServer = require('./server');
  4.
  5. webServer.listen(port, function() {
  6.   console.log('Server started at port ' + port);
  7
  8. 1. var http = require('http'),
2.   config = require('./config'),
3.   fileHandler = require('./filehandler'),
4.   parse = require('url').parse,
5.   types = config.types,
6.   rootFolder = config.rootFolder,
7.   defaultIndex = config.defaultIndex,
8.   server;
9.
10. module.exports = server = http.createServer();
11.
12. server.on('request', onRequest);
13.
14. function onRequest(req, res) {
15.  var filename = parse(req.url).pathname,
16.      fullPath,
17.      extension;
18.
19.  if(filename === '/') {
20.      filename = defaultIndex;
21.  }
22.
23.  fullPath = rootFolder + filename;
24.  extension = filename.substr(filename.lastIndexOf('.') + 1);
25.
26.  fileHandler(fullPath, function(data) {
27.      res.writeHead(200, {
28.           'Content-Type': types[extension] || 'text/plain',
29.           'Content-Length': data.length
30.      });
31.      res.end(data);
32.
33.  }, function(err) {
34.      res.writeHead(404);
35.      res.end();
36.  });
37. }. });
38. var fs = require('fs');
2.
3. module.exports = function(filename, successFn, errorFn) {
4.   fs.readFile(filename, function(err, data) {
5.       if(err) {
6.            errorFn(err);
7.       } else {
8.            successFn(data);
9.       }
10.  });
11. };
12. var fs = require('fs');
2.
3. module.exports = function(filename, successFn, errorFn) {
4.   fs.readFile(filename, function(err, data) {
5.       if(err) {
6.            errorFn(err);
7.       } else {
8.            successFn(data);
9.       }
10.  });
11. };
12. {
       "rootFolder": "./static",
       "defaultIndex": "/index.html",
       "types" : {
           "htm": "text/html",
           "html": "text/html",
           "jpg": "image/jpeg",
           "jpeg": "image/jpeg",
           "png": "image/png",
           "css": "text/css",
           "js": "text/javascript",
           "json": "application/json"
       }
  }
