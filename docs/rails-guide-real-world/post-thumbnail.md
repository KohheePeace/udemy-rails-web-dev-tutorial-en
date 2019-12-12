## Migration
`terminal`
```bash
rails g migration add_thumbnail_to_posts thumbnail:string
Running via Spring preloader in process 6860
      invoke  active_record
      create    db/migrate/20191204214947_add_thumbnail_to_posts.rb
```

Then

```bash
rails db:migrate
```

## Edit Form
`app/views/posts/_form.html.erb`

```erb
...
<div class="field">
  <%= form.label :thumbnail %>
  <%= form.file_field :thumbnail %>
</div>
...
```

## Edit Controller
`app/controllers/posts_controller.rb`
```ruby
private
    ...

    # Never trust parameters from the scary internet, only allow the white list through.
    def post_params
      params.require(:post).permit(:title, :content, :thumbnail)
    end
```

## Edit Model
`models/post.rb`
```ruby
class Post < ApplicationRecord
  ...
  has_one_attached :thumbnail
end
```

## Edit form
`app/views/posts/_form.html.erb`
```erb
<div class="field">
  <%= form.label :status %>
  <%= form.select :status, Post.statuses.keys.to_a, {} %>
</div>
```


## Show views
```erb
<%= image_tag(@post.thumbnail, width: 200) if @post.thumbnail.attached? %>
```

## Edit Controller
`app/controllers/posts_controller.rb`
```ruby
  ...
  def post_params
    params.require(:post).permit(:title, :content, :thumbnail, :status)
  end
```

## Edit pages#home
`app/controllers/pages_controller.rb`
```ruby
class PagesController < ApplicationController
  def home
    if user_signed_in?
      @posts = Post.published
      render 'home_after_login'
    else
      render 'home_before_login'
    end
  end
  ...
end
```