
!!! abstract "Chapter Goals"
    - Learn how to use **class** and **id** for css styling target

## Class and ID
In addition to HTML tag like `<h1>`, you can use `class` and `id` as an **css target**.

And this is more common way to apply CSS.

Let's edit `test.html` file like below.

`test.html`
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Title of the document</title>
  <link rel="stylesheet" href="test.css">
</head>

<body>
  <h1>Here is a title.</h1>
  <h2>Here is a subtitle.</h2>

  <ul>
    <li id="coffee" class="drink">Coffee</li>
    <li class="drink tea">Tea</li>
    <li class="drink">Milk</li>
  </ul>
</body>

</html>
```
`test.css`
```css
h1 { color: white; background: navy; }
ul { background: #FFFF33; }
.drink {
  color: red;
}
.tea {
  font-weight: bold;
}
#coffee {
  text-decoration: underline;
}
```

The output is like below...
![Class and Id](../img/css-guide/class-and-id.png)

## Summery
We learned super basics of CSS.

You may still wonder the content is too short and website still looks boring.

But don't be mind!

In the next section we will learn **Bootstrap** and the website looks better!