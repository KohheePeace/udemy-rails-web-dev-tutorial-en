https://api.rubyonrails.org/classes/ActiveRecord/Enum.html

## Migration
`terminal`
```bash
rails g migration add_status_to_posts status:integer
Running via Spring preloader in process 7782
      invoke  active_record
      create    db/migrate/20191204230816_add_status_to_posts.rb
```

## Edit migration file
`db/migrate/20191204230816_add_status_to_posts.rb`
```ruby
class AddStatusToPosts < ActiveRecord::Migration[6.0]
  def change
    add_column :posts, :status, :integer, default: 0
  end
end
```

```bash
rails db:migrate
```


## Edit `models/post.rb`
`models/post.rb`
```ruby
class Post < ApplicationRecord
  belongs_to :user
  has_rich_text :content
  has_one_attached :thumbnail
  enum status: [ :draft, :published ]
end
```

## Edit form
