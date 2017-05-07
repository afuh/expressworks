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
