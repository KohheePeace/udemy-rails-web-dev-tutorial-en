!!! abstract "Chapter Goals"
    - Learn 3 writings style of javascript

In this chapter, we'll be learning the different writings style of javascript.

This is the same things we did in CSS chapter.

## 1. `object.onclick = function(){myScript};`

This is what we did in the last chapter.

```js
document.getElementById('alert').onclick = function () {
  // you can get used to and remember method like this
  window.alert('Alert!!!!!!!!!!');     
}
```

## 2. `<element onclick="...">`
1. comment out existing code.
```js
// another example
// document.getElementById('alert').onclick = function () {
//   // you can get used to and remember method like this
//   window.alert('Alert!!!!!!!!!!');     
// }
```

2. add `onclick`
```js
<div id="alert" onclick="window.alert('Alert!!!!!!!!!!');">Alert Click!</div>
```

Check it also works.

## 3. `object.addEventListener("click", myScript);`
1. delete `onclick="..."`
```js
<div id="alert">Alert Click!</div>
```

2. add `object.addEventListener("click", myScript);`
```js hl_lines="7 8 9 10 11"
// another example
// document.getElementById('alert').onclick = function () {
//   // you can get used to and remember method like this
//   window.alert('Alert!!!!!!!!!!');     
// }

document.getElementById("alert").addEventListener("click", clickAlert);

function clickAlert() {
  window.alert('Alert!!!!!!!!!!');
}
```


## Separate js file
This is important to understand Bootstrap js.

`script4.js`
```js
// document.getElementById('demo').onclick = function changeContent() {
//   document.getElementById('demo').innerHTML = "Help me";
//   document.getElementById('demo').style = "Color: red";
// }

// Get Target element
let demoElement = document.getElementById('demo');

// Add onclick function to the #demoElement.
// you can skip function name 'changeContent'
demoElement.onclick = function () {
  demoElement.innerHTML = "Help me";
  demoElement.style = "Color: red";
}

// another example
// document.getElementById('alert').onclick = function () {
//   // you can get used to and remember method like this
//   window.alert('Alert!!!!!!!!!!');     
// }

document.getElementById("alert").addEventListener("click", clickAlert);

function clickAlert() {
  window.alert('Alert!!!!!!!!!!');
}

// example of onmouseover
document.getElementById('hover-me').onmouseover = function () {
  console.log('Hover!!!!!!!!!!');     
}
```

`test4.html`
```html hl_lines="25"
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <div id="demo">Click here</div>
    <div id="alert">Alert Click!</div>

    <div id="hover-me">Hover me!</div>

    <!-- Optional JavaScript -->
    <!-- <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script> -->
    <!-- <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script> -->
    <!-- <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script> -->
    <script src="script4.js"></script>
  </body>
</html>
```

You see it also works.

## Refs
https://www.w3schools.com/jsref/event_onclick.asp