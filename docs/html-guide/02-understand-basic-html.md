# Understand basic HTML 

!!! abstract "Chapter Goals"
    - Understand last chapter HTML code
    - Acquire the habit of googling


## Check the meaning of the HTML code of the last chapter.
==The most important thing is always **googling it!**==

This is the code we used in the last chapter.

`test.html`
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

Let's check this code from top to bottom.

### 1. `<!DOCTYPE html>`
Let's google "**what is doctype in html**"

![What is Doctype of html](../img/html-guide/what-is-doctype-of-html.png)  

I choose this link https://www.w3schools.com/tags/tag_doctype.asp

![What is Doctype link](../img/html-guide/what-is-doctype-link.png)  
> The <!DOCTYPE> declaration must be the very first thing in your HTML document, before the <html> tag.

> The <!DOCTYPE> declaration is not an HTML tag; ==**it is an instruction to the web browser about what version of HTML the page is written in.**==

So, if you want to use HTML4 version...
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```



### 2. `<head>`
Let's google **"what is head tag of html"**

![What is head tag of html](../img/html-guide/what-is-head-tag-of-html.png)  

> ==**the `<head>` tag is used to contain specific information about a web page**==, often referred to as metadata.

https://www.computerhope.com/jargon/h/html-head-tag.htm


### 3. `<meta charset="UTF-8">`
Let's google **"meta charset=UTF-8"**

![What is meta charset of html](../img/html-guide/what-is-meta-charset-of-html.png)  

> The HTML charset Attribute is used to specify the character encoding for the HTML document. 

According to the below link, charset can be...

```
- UTF-8: It specify the character encoding for Unicode.
- ISO-8859-1: It specify the character encoding for the Latin alphabet.
```

https://www.geeksforgeeks.org/html-meta-charset-attribute/


If you change the charset and add content like below...

It does not display correctly.

```html hl_lines="9"
<!DOCTYPE html>
<html>
<head>
  <meta charset="ISO-8859-1">
  <title>Title of the document</title>
</head>

<body>
  Бзиа збаша (Bzia zbaşa), Фэсапщы, Ç'kemi, ሰላም, and even right-to-left writing such as this السلام عليكم
</body>

</html>
```

![meta-charset-check](../img/html-guide/meta-charset-check.png)  

ref: https://stackoverflow.com/questions/29869743/what-is-meta-charset-utf-8

### 4. `<title>`
You can easily understand what is `<title>` tag.
![What is title tag of html](../img/html-guide/what-is-title-tag-of-html.gif)

### 5. `<body>`
![What is body tag of html](../img/html-guide/what-is-body-tag-of-html.png)  

> The HTML `<body>` tag defines the main content of the HTML document or the section of the HTML document ==that will be directly visible on your web page.== 

https://www.techonthenet.com/html/elements/body_tag.php