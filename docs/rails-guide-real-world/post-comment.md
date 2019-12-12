https://guides.rubyonrails.org/getting_started.html

## Make Comment model
`terminal`
```bash
rails g model Comment body:text user:references post:references
```

```
rails db:migrate
```

## Edit model
`models/post.rb`
```ruby hl_lines="3"
class Post < ApplicationRecord
  belongs_to :user
  has_many :comments
  has_rich_text :content
  has_one_attached :thumbnail
  enum status: [ :draft, :published ]
  paginates_per 10
end
```

`models/user.rb`
```ruby
class User < ApplicationRecord
  ...
  has_many :comments, dependent: :destroy
  ...
end
```


`config/routes.rb`
```ruby
resources :posts do
  resources :comments, only: [:create]
end
```

`comments_controller.rb`
https://stackoverflow.com/questions/16530532/rails-4-insert-attribute-into-params

```ruby
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(comment_params.merge(user_id: current_user.id))
    redirect_to post_path(@post)
  end
 
  private
    def comment_params
      params.require(:comment).permit(:body)
    end
end
```

`app/views/posts/show.html.erb`
```erb
...
<h2>Add a comment:</h2>
<%= form_with(model: [ @post, @post.comments.build ], local: true) do |form| %>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>

<h2>Comments</h2>
<% @post.comments.includes(:user).each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.user.name %>
  </p>
 
  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>
```