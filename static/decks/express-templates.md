# Express Templates

```js
app.set('view engine', 'jade');
app.set('views', './templates');
```
<!-- .element: class="fragment" -->

```jade
// templates/thoughts.jade
html
  head
    title= title
  body
    h1 Express is... #{descriptor}!
```
<!-- .element: class="fragment" -->

```js
var data = {
  title: 'My views on Express',
  descriptor: 'great'
};
res.render('thoughts', data);
```
<!-- .element: class="fragment" -->

^
**Finally** I'll tell you how `res.render` works!!
1. setup (*aside re: app.get, app.set*)
2. here's the template file
  - uses whitespace/nesting
  - two main ways to inject data: tagname= #{descriptor}
3. Here's how we call it 

---

# Express Templates

<ul>
  <li class="fragment">Consolidate.js</li>
  <li class="fragment">Jade</li>
</ul>

^
- can use basically any template lib

getting date into the page 
- http://jade-lang.com/reference/interpolation/
- http://jade-lang.com/reference/attributes/

|||

## Jade

```jade
html
  head
    title Hello World!
  body
    h1 I like Javascript
    p How do I like javascript? Let me count the ways...
```

```html
<html>

<head>
    <title>Hello World!</title>
</head>

<body>
    <h1>I like Javascript</h1>
    <p>How do I like javascript? Let me count the ways...</p>
</body>

</html>
```
<!-- .element: class="fragment" -->

^
- talk about nesting

|||

### Classes & IDs

```jade
.content
  h1#title I like Javascript
  h2.subitle Yes I do
  p How do I like javascript? Let me count the ways...
```

```html
<div class="content">
  <h1 id="title">I like Javascript</h1>
  <h2 class="subtitle">yes I do</h2>
  <p>How do I like javascript? let me count the ways...</p>
</div>
```
<!-- .element: class="fragment" -->

^
- makes a div w/class
- adds id to elem
- adds class to elem

|||

### Attributes

```jade
script(src='/js/main.js')

label Subscribe to our newsletter
  input(
    type='checkbox'
    name='subscribe'
    checked='checked'
  )
```

```html
<script src="/js/main.js"></script>

<label>Subscribe to our newsletter
  <input type="checkbox" name="subscribe" checked="checked" />
</label>
```
<!-- .element: class="fragment" -->

|||

<!-- .slide: data-state="exercise" -->
1. Create `homepage.jade`
2. Render it on request to `/`

Hints:
* set `view engine`
* set `views` to point to template directory

---

### Injecting Data

```jade
// infobox.jade (snippet)
.infobox
  h3= title
  p User "#{username}" has been updated
```

```js
res.render('infobox', {
  title: "Save Successful",
  username: "Sequoia"
});
```
<!-- .element: class="fragment" -->

```html
<div class="infobox">
  <h3>Save Successful</h3>
  <p>User "Sequoia" has been updated</p>
</div>
```
<!-- .element: class="fragment" -->

^
- "putting text in stuff"
- using a snippet here, normally would be full page or json

|||

<!-- .slide: data-state="exercise" -->
Request:
```no-highlight
GET /user/1
```

Response:
```html
<html>
<head>
    <title>Zeynep</title>
</head>
<body>
  <h1>User Profile</h1>
  <ul>
      <li>id: 1</li>
      <li>name: Zeynep</li>
  </ul>
</body>

</html>
```

|||

### Dynamic Attributes

```jade
// infobox.jade
.infobox(class=type)
  h3= title
  p= message
```

```js
var event = {
  type : "error",
  title: "Save Failed",
  message: "Please log in"
};
res.render('infobox', event);
```
<!-- .element: class="fragment" -->

```html
<div class="infobox error">
    <h3>Save failed</h3>
    <p>403: Please log in</p>
</div>
```
<!-- .element: class="fragment" -->

|||

### Dynamic Attributes

```js
var event = {
  type : ["success", "user-action"]
  title: "Success",
  message: "Profile Updated"
};
res.render('infobox', event);
```

```html
<div class="infobox success user-action">
    <h3>Success</h3>
    <p>Profile Updated</p>
</div>
```

|||

### Conditionals & Iteration

```jade
body.userlist
  if !users.length
    p No users!
  else
    ul
      each user in users
        li= user.name
```

^
- What do you think this will do?
- *Try it together*

|||

<!-- .slide: data-state="transition" -->
Up Next: Datastores