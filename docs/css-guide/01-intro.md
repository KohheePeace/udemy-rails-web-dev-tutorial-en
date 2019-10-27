!!! abstract "Chapter Goals"
    - Understand what is CSS
    - Try CSS
    - Learn CSS syntax
    - Learn 3 writing styles of CSS

## What is CSS ?
> Cascading Style Sheets (CSS) is ==a style sheet language== used for describing the presentation of a document written in a markup language like HTML.[1] CSS is a cornerstone technology of the World Wide Web, alongside HTML and JavaScript.[2]

https://en.wikipedia.org/wiki/Cascading_Style_Sheets


!!! summery
    **CSS is a language for styling**

That's it and let's try it.

### Let's try it!

`test.html`
```html hl_lines="20 21 22 23"
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Title of the document</title>
</head>

<body>
  <h1>Here is a title.</h1>
  <h2>Here is a subtitle.</h2>

  <ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>
</body>

</html>
<style>
  h1 { color: white; background: navy; }
  ul { background: #FFFF33; }
</style>
```
![First style tag](../img/css-guide/first-style-tag.png)

You see that ==CSS is a language for styling==.

## Check the CSS syntax

```css
  h1 { color: white; ... }
  /* target { css-property: property value; } */
```

1. target-element can be HTML tag (`h1`, `ul`, `li`...), Class or ID( We will check it in [the next chapter](/css-guide/02-class-and-id/)).
2. You don't need to memorize all **css-property**. You will gradually get used to it.

## Ref Links
https://www.w3schools.com/whatis/whatis_css.asp