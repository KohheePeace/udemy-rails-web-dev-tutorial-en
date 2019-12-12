# Memo jQuery

https://github.com/rails/webpacker/blob/master/docs/webpack.md#plugins

## 7 Reasons NOT to use a Content Delivery Network
https://www.sitepoint.com/7-reasons-not-to-use-a-cdn/

---


`terminal`
```bash
yarn add jquery
```

## Webpack ProvidePlugin

https://webpack.js.org/plugins/provide-plugin/

=> **To make `$` or `jQuery` use everywhere**
> ProvidePlugin
> ==Automatically load modules instead of having to import or require them everywhere.==
> 
>
```
new webpack.ProvidePlugin({
  identifier: 'module1',
  // ...
});
```

## Usage: jQuery
https://webpack.js.org/plugins/provide-plugin/#usage-jquery

To automatically load jquery we can simply point both variables it exposes to the corresponding node module:

```js
new webpack.ProvidePlugin({
  $: 'jquery',
  jQuery: 'jquery'
});
```
Then in any of our source code:

```js
// in a module
$('#item'); // <= just works
jQuery('#item'); // <= just works
// $ is automatically set to the exports of module "jquery"
```

## Useful Links
### webpacker link
https://stackoverflow.com/questions/33998262/jquery-ui-and-webpack-how-to-manage-it-into-module

### jquery webpacker
[Managing jQuery plugin dependency in webpack](https://stackoverflow.com/questions/28969861/managing-jquery-plugin-dependency-in-webpack)
https://github.com/Eonasdan/bootstrap-datetimepicker/issues/1662
https://stackoverflow.com/questions/39823699/use-jquery-ui-with-webpack-having-a-particular-file-structure