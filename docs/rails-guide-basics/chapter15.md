## Refactor

## Step1 Extract almost same code
`app/views/articles/new.html.erb`
```erb hl_lines="2 3 4 5 6 7 8 9 10 11 12 13 14 15 16"
<h1>New Article</h1>
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>

  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>

  <p>
    <%= form.submit %>
  </p>
<% end %>
```
`app/views/articles/edit.html.erb`
```erb hl_lines="2 3 4 5 6 7 8 9 10 11 12 13 14 15 16"
<h1>Edit article</h1>
<%= form_with(model: @article, local: true) do |form| %> 
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
 
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
 
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

Create a file `app/views/articles/_form.html.erb`
```erb
<%= form_with(model: @article, local: true) do |form| %> 
  <p>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </p>
 
  <p>
    <%= form.label :text %><br>
    <%= form.text_area :text %>
  </p>
 
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

## Step2 Edit views
This is not correct. => form path is different.
`app/views/articles/new.html.erb`
```erb hl_lines="2 3 4 5 6 7 8 9 10 11 12 13 14 15 16"
<h1>New Article</h1>
<%= render 'form' %>
```

This is same.
`app/views/articles/edit.html.erb`
```erb hl_lines="2 3 4 5 6 7 8 9 10 11 12 13 14 15 16"
<h1>Edit article</h1>
<%= render 'form' %>
```

## Step3 Correct controller `def new`
```ruby hl_lines="2"
def new
  @article = Article.new
end
```