# A Sample Node.js Website

This is a sample basic Node.js website using plain HTML files and the built in http and fs modules.

This tutorial will walk you through the creation of a very basic website using only Node.js built in modules. Follow these steps to create a Node.js website:

## Steps

1. Create a folder for your Node.js project.
2. Create a home page HTML and call it `index.html`. Add the required HTML tags and some basic content in the `index.html` file. 
3. Create a second file and for now, call it `another-page.html`. Add the required HTML tags and some basic content in the `another-page.html` file.
4. Add a link in the `index.html` page to `another-page.html`. And add a link in the `another-page.html` to `index.html`. This will allow for easy testing of pages.
5. Create a new file called `app.js`. 
6. In `app.js` import the required modules:

      ```js
      var http = require('http');
      var url = require('url');
      var fs = require('fs');
      ```

7. Create an http server:

      ```js
      http.createServer(function (req, res) {
      }).listen(8080);
      ```

      This will start a web server. The server is available to test by opening a browser and using the URL `http://localhost:8080/index.html`.

8. Inside the `createServer` function add code to fetch the current URL:
      
      ```js
      var q = url.parse(req.url, true);
      var filename = "." + q.pathname;
      ```
   
9. Inside the `createServer` function, after the the previous lines of code, add code to load the appropriate HTML file based on the URL. For example the URL `http://localhost:8080/index.html` will load the `index.html` file.
      
      ```js
      fs.readFile(filename, function(err, data) {
        res.writeHead(200, {'Content-Type': 'text/html'});
        res.write(data);
        return res.end();
      });
      ```

10. Inside the `readFile` function, add code that will display an error message in case the requested URL does not match an exsting file:
      
      ```js 
      if (err) {
        res.writeHead(404, {'Content-Type': 'text/html'});
        return res.end("404 Not Found");
      } 
      ```

11. To test your Node.js website, open up a terminal, use `cd` to navigate to your project folder, and use `node app.js` to start your file. Then open a browser and visit the URL `http://localhost:8080/index.html`.

## Final Code

Your final code in `app.js` should look like this:

```js
var http = require('http');
var url = require('url');
var fs = require('fs');

http.createServer(function (req, res) {

  var q = url.parse(req.url, true);

  var filename = "." + q.pathname;

  fs.readFile(filename, function(err, data) {

    if (err) {

      res.writeHead(404, {'Content-Type': 'text/html'});
      return res.end("404 Not Found");

    } 

    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);
    return res.end();

  });

}).listen(8080);
```

> Full tutorial URL:  
> https://codeadam.ca/learning/nodejs-website.html

***

## Repo Resources

* [Visual Studio Code](https://code.visualstudio.com/)
* [Node.js](https://nodejs.org/en/)

<a href="https://codeadam.ca">
<img src="https://codeadam.ca/images/code-block.png" width="100">
</a>

