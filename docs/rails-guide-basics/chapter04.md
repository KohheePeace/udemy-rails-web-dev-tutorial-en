!!! abstract "Chapter Goal"
    - Check best practice routes provided by rails

Ref: https://guides.rubyonrails.org/getting_started.html#getting-up-and-running

We are in the middle of learning **CRUD**.

* [ ] ==C: Create==
* [ ] R: Read
* [ ] U: Update
* [ ] D: Delete

![rails-flow-diagram.png](../img/rails-guide-basics/rails-flow-diagram.png)

## Step1
`routes.rb`

```ruby hl_lines="6"
Rails.application.routes.draw do
  get 'welcome/index'
  get 'hello/hogehoge'
  
  # resources :articles
  get 'articles/new'

  root 'hello#hogehoge'
end
```

This means...

!!! info
    1. If user visit http://localhost:3000/articles/new
    2. Call articles controller's new action


## Step2 Controller
Make `app/controllers/articles_controller.rb`
```ruby
class ArticlesController < ApplicationController
  def new
  end
end
```
*Class name corresponds to filename
`articles_controller.rb` => `ArticlesController`

## Step3 Views
Make `app/views/articles` folder (*plural) and `app/views/articles/new.html.erb`
```erb
<h1>New Article</h1>
```

![new-article-ss](../img/rails-guide-basics/new-article-ss.png)

In the next chapter, we will ==**make a form**== in this page.