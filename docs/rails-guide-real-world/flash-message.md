https://guides.rubyonrails.org/action_controller_overview.html#the-flash


`app/views/layouts/application.html.erb`
```erb
<% flash.each do |name, msg| -%>
  <%= content_tag :div, msg, class: name %>
<% end -%>
```

## ケツロン
- Toastsより、alertsの方がUXよい。

`app/views/shared/_flash.html.erb`
```erb
<% flash.each do |name, msg| -%>
  <div class="<%= bootstrap_alert_class(name) %>">
    <%= msg %>
  </div>
<% end -%>
```

`app/views/layouts/application.html.erb`
```erb hl_lines="18"
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
    <%= render 'shared/flash' %>
    <%= yield %>
  </body>
</html>
```

`app/helpers/application_helper.rb`
```ruby
module ApplicationHelper
  def bootstrap_alert_class(type)
    case type
      when "notice" then "alert alert-info"
      when "success" then "alert alert-success"
      when "error" then "alert alert-danger"
      when "alert" then "alert alert-danger"
    end
  end
end
```


## Flash now
https://guides.rubyonrails.org/action_controller_overview.html#flash-now
By default, adding values to the flash will make them available to the next request, but sometimes you may want to access those values in the same request. For example, if the create action fails to save a resource and you render the new template directly, that's not going to result in a new request, but you may still want to display a message using the flash. To do this, you can use flash.now in the same way you use the normal flash:

```ruby
class ClientsController < ApplicationController
  def create
    @client = Client.new(params[:client])
    if @client.save
      # ...
    else
      flash.now[:error] = "Could not save client"
      render action: "new"
    end
  end
end
```
