!!! abstract "Chapter Goal"
    - U: Update => Update article.

We are in the middle of learning **CRUD**.

* [x] C: Create
* [x] R: Read
* [ ] ==U: Update==
* [ ] D: Delete

https://guides.rubyonrails.org/getting_started.html#updating-articles

![rails-flow-diagram.png](../img/rails-guide-basics/rails-flow-diagram.png)

## Step1 Routes
Add a routes for edit page.
`routes.rb`
```ruby
get '/articles/:id/edit', to: 'articles#edit', as: 'edit_article'
```

This makes same route with

```
resources :articles
```

## Step2 Controller
`app/controllers/articles_controller.rb`
```ruby
class ArticlesController < ApplicationController
  ...
  def edit
    @article = Article.find(params[:id])
  end
  ...
end
```

## Step3 Views
`app/views/articles/edit.html.erb`
```erb hl_lines="3"
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

Check views output...

![article-edit-form.png](../img/rails-guide-basics/article-edit-form.png)

You see form field is initially filled with article data.

## Step4 Try update
![try-article-update.gif](../img/rails-guide-basics/try-article-update.gif)

!!! info
    1. Click "Update Article" button
    2. Hit `"/articles/1"` url with method PATCH (form method is "post" but you see hidden input.)
    ![hidden-input-patch.png](../img/rails-guide-basics/hidden-input-patch.png)
    3. Error happened `No route matches [PATCH] "/articles/1"`