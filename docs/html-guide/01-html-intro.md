# Chapter 2 HTML Introduction

!!! abstract "Chapter Goals"
    - Understand what is HTML
    - Make a basic HTML file
    - Browse HTML file in a web browser


## What is HTML ?

From wikipedia...

> Hypertext Markup Language (HTML) is the standard markup language for ___==documents designed to be displayed in a web browser==___.

https://en.wikipedia.org/wiki/HTML

## What is web browser?
Web browser is something like below...
![Web-browser-screenshot](https://digitalesklassenzimmer.files.wordpress.com/2015/08/webbrowser.png)
Image from: https://digitalesklassenzimmer.files.wordpress.com/2015/08/webbrowser.png


## Let's write basic HTML!
We will use the example of below link. This is because it is reliable than me.

https://www.w3schools.com/html/html5_intro.asp


![ss](../img/html-guide/w3-school-html.png)


## 
In `terminal`
```bash
mkdir html-test # make directory
cd html-test # change directory
touch test.html # make file
```


In `test.html` (NOTE: I added some **`indent`** to the example.)
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Title of the document</title>
</head>

<body>
  Content of the document......
</body>

</html>
```

Open this html file in chrome (**web browser**).

`terminal`
```bash
# under html-playground folder
open test.html
```

![Screenshot](../img/html-guide/first-html-example.png)

## Finish!
Do you notice that we have achieved the definition of HTML?

=> ==**Display documents in a web browser**==

In the next chapter, we will be learning the meaning of html code in this chapter!