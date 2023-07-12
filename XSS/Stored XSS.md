
Spawn 2 containers

set cookie in one of the containers

to check if cookie is set
1)console.log(document.cookie)
2)Dev tool -> Storage ->Cookie

to check for XSS first try HTML injection coz that is likely to work


in the input field
```html
<h1>test</h1>
```

html injection working now try for XSS

```js
<script>prompt(1)</script>
```

go in other container and we get prompt so it is stored

to get the cookie of other users

```js
<script>alert(document.cookie)</script>
```


if http only flag set, JS cannot access the cookies
