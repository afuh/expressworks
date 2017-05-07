# expressworks

https://github.com/azat-co/expressworks

### HELLO WORLD! (Exercise 1 of 8)
Create an Express.js app that outputs "Hello World!" when somebody goes to `/home`.
```javascript
const express = require('express');
const app = express();

app.get('/home', (req, res) => {
  res.end('Hello World!')
})
app.listen(process.argv[2])
```
###  STATIC (Exercise 2 of 8)
This exercise is about serving static assets like HTML files.
There are many ways to do it, but we want you to apply static middleware to serve the file `index.html`.
```javascript
const express = require('express');
const app = express();

app.use(express.static(process.argv[3]))

app.listen(process.argv[2])
```
### PUG (Exercise 3 of 8)
Create an Express.js app with a home page rendered by the Pug template engine.
The home page should respond to `/home`.
```shell
$ npm i pug --save
```
```javascript
const express = require('express');
const app = express();

app.set('view engine', 'pug');
app.set('views', process.argv[3]);

app.get('/home', (req, res) => {
  res.render('index', {
    date: new Date().toDateString()
  })
})

app.listen(process.argv[2]);
```
### GOOD OLD FORM (Exercise 4 of 8)
Forms are important. This exercise will teach you how to process the traditional (non-AJAX) web form.
```shell
$ npm i body-parser --save
```
```javascript
const express = require('express');
const bodyparser = require('body-parser')
const app = express();

app.use(bodyparser.urlencoded({extended: false}))

app.post('/form', (req, res) => {
  res.send(req.body.str.split('').reverse().join(''))
})

app.listen(process.argv[2])
```
### STYLISH CSS (Exercise 5 of 8)
HTML without styles is boring so this exercise will teach you how to use Stylus with Express on the fly.
```shell
$ npm i stylus --save
```
```javascript
const express = require('express');
const stylus = require('stylus')
const app = express();

app.use(stylus.middleware(process.argv[3]));
app.use(express.static(process.argv[3]))

app.listen(process.argv[2])
```
###  PARAM PAM PAM (Exercise 6 of 8)
This exercise is about using URL parameters.
For example, if you have /message/526aa677a8ceb64569c9d4fb, then you should know how to
extract that value which is an ID of the message.

Create an Express.js server that processes PUT `/message/:id` requests
and produces a SHA-1 hash of the current date combined with the ID from the URL.
```javascript
const express = require('express');
const app = express();

app.put('/message/:id', (req, res) => {
  const id = req.params.id;
  const str = require('crypto')
    .createHash('sha1')
    .update(new Date().toDateString() + id)
    .digest('hex')
  res.send(str);
})

app.listen(process.argv[2])
```
###  WHAT'S IN QUERY (Exercise 7 of 8)
Oftentimes, we need to process the data from the URL query string (urlencoded).

Write a route that extracts data from the query string in the GET `/search` URL
route, e.g. `?results=recent&include_tabs=true` and then outputs it back to
the user in JSON format.
```javascript
const express = require('express');
const app = express();

app.get('/search', (req, res) => {
  const query = req.query;
  res.send(query)
})

app.listen(process.argv[2])
```
### JSON ME (Exercise 8 of 8)
Most of the times we're building RESTful API servers with JSON.

Write a server that, when it receives a GET, reads a file, parses it to JSON,
and responds with that content to the user.
```javascript
const express = require('express');
const fs = require('fs');
const app = express();

app.get('/books', (req, res) => {
  fs.readFile(process.argv[3], (err, data) => {
    if (err) return res.sendStatus(500)
    res.json(JSON.parse(data))
  })
})

app.listen(process.argv[2] || 3000)
```
