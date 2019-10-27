We learned in last chapter that jQuery is easy writing alternative of javascirpt.

So, let's replace existing code by jQuery.


`test4.html`
![jquery-replace-onclick-search](../img/jquery-guide/jquery-replace-onclick-search.gif)

Replace click
https://api.jquery.com/click/

Replace innerHTML
https://api.jquery.com/html/

Repalce style
https://api.jquery.com/css/

##  Replace innerHTMl
```html
// Get Target element
let demoElement = document.getElementById('demo');

// Add onclick function to the #demoElement.
// you can skip function name 'changeContent'
demoElement.onclick = function () {
  demoElement.innerHTML = "Help me";
  demoElement.style = "Color: red";
}
```
becomes

```html
$("#demo").click(function() {
  $("#demo").html("Help me");
  $("#demo").css({ color: "red" });
});
```

## Replace alert
```html
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

becomes

```html
$("#alert").click(function() {
  window.alert('Alert!!!!!!!!!!');
})
```

## Repalce getElementsByClassName

https://api.jquery.com/class-selector/

```html
// getElementsByClassName exmaple
// Notice that this is plural
let testElements = document.getElementsByClassName('test');

testElements[0].onclick = function () {
  alert('Hello test 0');
}

testElements[1].onclick = function () {
  alert('Hello test 1');
}
```

becomes

```html
$(".test")[0].click(function () {
  alert('Hello test 0');
});

$(".test")[1].click(function () {
  alert('Hello test 0');
});
```