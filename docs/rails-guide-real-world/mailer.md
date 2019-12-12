https://sendgrid.com/docs/for-developers/sending-email/rubyonrails/

`terminal`
```bash
rails generate mailer CommentNotifierMailer
Running via Spring preloader in process 15278
      create  app/mailers/comment_notifier_mailer.rb
      invoke  erb
      create    app/views/comment_notifier_mailer
      invoke  test_unit
      create    test/mailers/comment_notifier_mailer_test.rb
      create    test/mailers/previews/comment_notifier_mailer_preview.rb
```


`app/mailers/comment_notifier_mailer.rb`
```ruby
class CommentNotifierMailer < ApplicationMailer
  default :from => 'any_from_address@example.com'

  def send_new_comment_emai(user)
    @user = user
    mail( :to => @user.email,
    :subject => 'Thanks for signing up for our amazing app' )
  end
end

```

`app/views/user_notifier_mailer/send_signup_email.html.erb`
```erb
<!DOCTYPE html>
<html>
  <head>
    <meta content='text/html; charset=UTF-8' http-equiv='Content-Type' />
  </head>
  <body>
    <h1>Thanks for signing up, <%= @user.name %>!</h1>
    <p>Thanks for joining and have a great day! Now sign in and do
awesome things!</p>
  </body>
</html>
```

`app/controllers/comments_controller.rb`
```ruby hl_lines="5 6 7"
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(comment_params.merge(user_id: current_user.id))
    author = @post.user
    # Deliver email to notify new comment created to post author.
    CommentNotifierMailer.send_new_comment_email(author).deliver
    redirect_to post_path(@post)
  end
 
  private
    def comment_params
      params.require(:comment).permit(:body)
    end
end
```

`config/environment.rb`
```ruby
# Load the Rails application.
require_relative 'application'

# Initialize the Rails application.
Rails.application.initialize!

ActionMailer::Base.smtp_settings = {
  :user_name => Rails.application.credentials.sendgrid[:user_name],
  :password => Rails.application.credentials.sendgrid[:password],
  :domain => 'yourdomain.com',
  :address => 'smtp.sendgrid.net',
  :port => 465,
  :authentication => :plain,
  :enable_starttls_auto => true
}
```

## Edit credentials
Go to https://app.sendgrid.com/settings/api_keys
and check credentials


**If credentials not update, please run**
```
spring stop
```

Click **Create API Key** button

```bash
EDITOR="code --wait" rails credentials:edit
```

```yaml
...
sendgrid:
  user_name: jfieofhewafw
  password: fehowiahfoeaifhewu
```

