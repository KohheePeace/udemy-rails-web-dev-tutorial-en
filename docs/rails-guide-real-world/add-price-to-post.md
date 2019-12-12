### Why use money gem ?
https://blog.bigbinary.com/2013/01/14/handling-money-in-ruby.html


### Step1 Install money-rails gem
https://github.com/RubyMoney/money-rails

```Gemfile
gem 'money-rails', '~>1.12'
```

```bash
bundle
```

```bash
rails g money_rails:initializer
Running via Spring preloader in process 35863
      create  config/initializers/money.rb
```

You can edit default configuration by this file.
`config/initializers/money.rb`


### Step 2 Add monetization column to Post
https://github.com/RubyMoney/money-rails#migration-helpers

`terminal`
```bash
rails g migration MonetizePost
```

`db/migrate/20191209044824_monetize_post.rb`
```ruby hl_lines="3"
class MonetizePost < ActiveRecord::Migration[6.0]
  def change
    add_monetize :posts, :price
  end
end
```

```bash
rails db:migrate
```

This adds `price_cents` and `price_currency` to posts tables.

## Edit Post model
`app/models/post.rb`
```ruby hl_lines="8"
class Post < ApplicationRecord
  belongs_to :user
  has_many :comments
  has_rich_text :content
  has_one_attached :thumbnail
  enum status: [ :draft, :published ]
  paginates_per 10
  monetize :price_cents
end
```

## Add price field to post form
https://stackoverflow.com/questions/18898947/rails-number-field-alternative-for-decimal-values

`app/views/posts/_form.html.erb`
```erb
...
  <div class="field">
    <%= form.label :content %>
    <%= form.rich_text_area :content %>
  </div>

  <div class="field">
    <%= form.label :price %>
    <%= form.number_field :price, step: :any %>
  </div>
...
```

## Edit posts controller
`app/controllers/pages_controller.rb`
```ruby
  ...
  def post_params
    params.require(:post).permit(:title, :content, :thumbnail, :status, :price)
  end
```

## Edit Show page
`app/views/posts/show.html.erb`
```erb
...
<p>
  <strong>User:</strong>
  <%= @post.user_id %>
</p>

<p>
  <strong>Price:</strong>
  <%= humanized_money_with_symbol @post.price %>
</p>
...
```