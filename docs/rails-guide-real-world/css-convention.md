https://tech.basicinc.jp/articles/147
上のように、
やる。


## Example...
`app/views/shared/_navbar.html.erb`

```erb hl_lines="2"
<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-light" data-relative-path="app-views-shared-navbar">
...
```

ならば、

`app/assets/stylesheets/shared/_navbar.scss`
```scss
[data-relative-path="app-views-shared-navbar"] {
  .logo {
    color: red!important;
  }
  
  .navbar-avatar-img {
    width: 2rem;
    height: 2rem;
  }
}
```