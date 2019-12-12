## Change navbar if user_singned_in?
`app/views/pages/home.html.erb`
```erb hl_lines="8"
<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-light">
  <a class="navbar-brand font-weight-bold" href="#">Logo</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <% if user_signed_in? %>
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav ml-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item">
        <%= link_to "Logout",destroy_user_session_path, method: :delete, class: "nav-link" %>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
      </li>
    </ul>
  </div>
  <% else %>
    <a class="btn btn-warning my-2 my-sm-0 ml-auto" href="/users/sign_up" role="button">Sign Up</a>
  <% end %>
</nav>
<!-- # Navbar -->
```

## Shared views
https://guides.rubyonrails.org/layouts_and_rendering.html#using-partials
`app/views/shared/_navbar.html.erb`
```erb
<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-light">
  <a class="navbar-brand font-weight-bold" href="#">Logo</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <% if user_signed_in? %>
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav ml-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item">
        <%= link_to "Logout",destroy_user_session_path, method: :delete, class: "nav-link" %>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
      </li>
    </ul>
  </div>
  <% else %>
    <a class="btn btn-warning my-2 my-sm-0 ml-auto" href="/users/sign_up" role="button">Sign Up</a>
  <% end %>
</nav>
<!-- # Navbar -->
```

`app/views/layouts/application.html.erb`
```erb hl_lines="13"
<!DOCTYPE html>
<html>
  <head>
    <title>Myapp</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= render "shared/navbar" %>
    <%= yield %>
  </body>
</html>
```

## Rendering different views
https://stackoverflow.com/questions/15923664/rendering-different-views-in-one-action
`routes.rb`
```ruby

```


## Gem annotate
Ref: https://github.com/ctran/annotate_models#configuration-in-rails​

Gemfile

group :development do
  ...
  gem 'annotate'
end
​```

`terminal`
```bash
bundle
rails g annotate:install
​
Running via Spring preloader in process 53096
create  lib/tasks/auto_annotate_models.rake