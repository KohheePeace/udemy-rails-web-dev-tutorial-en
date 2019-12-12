##Step1 Install libraries

https://getbootstrap.com/docs/4.3/getting-started/download/#yarn
https://gist.github.com/yalab/cad361056bae02a5f45d1ace7f1d86ef

`terminal`
```
yarn add bootstrap jquery popper.js
```


## Step2 Edit `packs/application.js`

```js hl_lines="11"
// This file is automatically compiled by Webpack, along with any other files
// present in this directory. You're encouraged to place your actual application logic in
// a relevant structure within app/javascript and only use these pack files to reference
// that code so it'll be compiled.

require("@rails/ujs").start()
require("turbolinks").start()
require("@rails/activestorage").start()
require("channels")

import 'bootstrap/dist/js/bootstrap';

// Uncomment to copy all static images under ../images to the output folder and reference
// them with the image_pack_tag helper in views (e.g <%= image_pack_tag 'rails.png' %>)
// or the `imagePath` JavaScript helper below.
//
// const images = require.context('../images', true)
// const imagePath = (name) => images(name, true)
```


## Step3 Edit `config/webpack/environment.js`

`config/webpack/environment.js`

```js
const { environment } = require('@rails/webpacker')
const webpack = require('webpack')

environment.plugins.prepend(
  'Provide',
  new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery',
    jquery: 'jquery',
    Popper: ['popper.js', 'default'],
  })
)

module.exports = environment
```

Ref: https://github.com/rails/webpacker/blob/master/docs/webpack.md#plugins

## Step 4 Styles
### Step1 Rename `app/assets/stylesheets/application.css`
Rename `app/assets/stylesheets/application.css` => `app/assets/stylesheets/application.scss`

### Step2 Import bootstrap css
https://stackoverflow.com/questions/47618780/rails-precompiled-assets-missing-node-modules

`app/assets/stylesheets/application.scss`
```scss
/*
 * This is a manifest file that'll be compiled into application.css, which will include all the files
 * listed below.
 *
 * Any CSS and SCSS file within this directory, lib/assets/stylesheets, or any plugin's
 * vendor/assets/stylesheets directory can be referenced here using a relative path.
 *
 * You're free to add application-wide styles to this file and they'll appear at the bottom of the
 * compiled file so the styles you add here take precedence over styles defined in any other CSS/SCSS
 * files in this directory. Styles in this file should be added after the last require_* statement.
 * It is generally better to create a new file per style scope.
 *
 *= require_tree .
 *= require_self
 */
 @import "bootstrap/scss/bootstrap";
```

## Meta tag
`app/views/layout/application.html.erb`
```erb hl_lines="8 9 10"
<!DOCTYPE html>
<html>
  <head>
    <title>Myapp</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= render "shared/navbar" %>
    <%= yield %>
  </body>
</html>

```


## Add $ to window
https://stackoverflow.com/questions/55895494/is-not-defined-when-installing-jquery-in-rails-via-webpack
`packs/application.js`
```js
...
window.jQuery = $;
window.$ = $;
```