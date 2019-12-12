https://github.com/kaminari/kaminari

## Install Gem
`Gemfile`
```
gem 'kaminari'
```

`terminal`
```
bundle
```

## Make Dummy data
`terminal`
```bash
rails c
```
`db/seeds.rb`
```ruby
40.times do |n|
  post = Post.create(
    title: "hogehoge-#{n}",
    content: "content-#{n}",
    status: :published,
    user_id: 2
  )
end
```


`terminal
```bash
rails db:seed
```

## Use kaminari
`app/controllers/pages_controller.rb`
```ruby hl_lines="4"
class PagesController < ApplicationController
  def home
    if user_signed_in?
      @posts = Post.published.page(params[:page])
      render 'home_after_login'
    else
      render 'home_before_login'
    end
  end

  def settings
  end
end
```

`app/views/pages/home_after_login.html.erb`
Just add
```erb
<%= paginate @posts %>
```

```erb hl_lines="22"
<h1>Posts</h1>

<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>User</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <% @posts.each do |post| %>
      <tr>
        <td><%= post.title %></td>
        <td><%= post.user_id %></td>
        <td><%= link_to 'Show', post %></td>
      </tr>
    <% end %>
  </tbody>
</table>
<%= paginate @posts %>
```

## Edit default per page
1 page, 25posts is the default settings.
I will change this to
1page, 10 posts.
`models/post.rb`
```ruby hl_lines="6"
class Post < ApplicationRecord
  belongs_to :user
  has_rich_text :content
  has_one_attached :thumbnail
  enum status: [ :draft, :published ]
  paginates_per 10
end
```


## Customize pager
https://github.com/kaminari/kaminari#customizing-the-pagination-helper
`terminal`
```bash
rails g kaminari:views bootstrap4
Running via Spring preloader in process 10045
      downloading app/views/kaminari/_first_page.html.erb from kaminari_themes...
      create  app/views/kaminari/_first_page.html.erb
      downloading app/views/kaminari/_gap.html.erb from kaminari_themes...
      create  app/views/kaminari/_gap.html.erb
      downloading app/views/kaminari/_last_page.html.erb from kaminari_themes...
      create  app/views/kaminari/_last_page.html.erb
      downloading app/views/kaminari/_next_page.html.erb from kaminari_themes...
      create  app/views/kaminari/_next_page.html.erb
      downloading app/views/kaminari/_page.html.erb from kaminari_themes...
      create  app/views/kaminari/_page.html.erb
      downloading app/views/kaminari/_paginator.html.erb from kaminari_themes...
      create  app/views/kaminari/_paginator.html.erb
      downloading app/views/kaminari/_prev_page.html.erb from kaminari_themes...
      create  app/views/kaminari/_prev_page.html.erb
```