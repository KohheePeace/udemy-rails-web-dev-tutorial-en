## Devise Google Login

## Step1 Install Devise gem
`Gemfile`
```
gem 'devise'
```

`terminal`
```
bundle
```

## Step2 
```bash
rails generate devise:install
```


## Step3 
`config/environments/development.rb`
```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

## Step4
`config/routes.rb`
```bash
rails generate devise User
rails db:migrate
```

### Step5 Add `omniauth-google-oauth2` gem
https://github.com/zquestz/omniauth-google-oauth2

`Gemfile`
```
gem 'omniauth-google-oauth2'
```

`terminal`
```
bundle
```

### Step6 Google API Setup
1. Go to 'https://console.developers.google.com'
2. Select your project.
3. Go to Credentials, then select the "OAuth consent screen" tab on top, and provide an 'EMAIL ADDRESS' and a 'PRODUCT NAME'
4. Wait 10 minutes for changes to take effect.

### Step6.5 Create User model
```bash
rails g migration AddOmniauthToUsers name:string image:string google_uid:string:uniq
```

### Step7 Edit credentials
`terminal`
```
docker-compose run -e EDITOR="vim" web rails credentials:edit
```

```bash
google:
     client_id: fejioafjeioafhewhgweai
     client_secret: fjfoaiejfwncaeiowjfeiaofaw
```

### Step8
Edit `config/initializers/devise.rb`
```ruby
  # config.omniauth :github, 'APP_ID', 'APP_SECRET', scope: 'user,public_repo'
  config.omniauth :google_oauth2, Rails.application.credentials.google[:client_id], Rails.application.credentials.google[:client_secret], {
    scope: 'email,profile'
  }
```

### Step9
`config/routes.rb`
```ruby
devise_for :users, controllers: { omniauth_callbacks: 'users/omniauth_callbacks' }
```

### Step10
`/app/models/user.rb`
```ruby
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable, :omniauthable, omniauth_providers: [:google_oauth2]
end
```

### Step11
Now we just add the file `app/controllers/users/omniauth_callbacks_controller.rb`:
```ruby
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def google_oauth2
      # You need to implement the method below in your model (e.g. app/models/user.rb)
      @user = User.from_omniauth(request.env['omniauth.auth'])

      if @user.persisted?
        flash[:notice] = I18n.t 'devise.omniauth_callbacks.success', kind: 'Google'
        sign_in_and_redirect @user, event: :authentication
      else
        session['devise.google_data'] = request.env['omniauth.auth'].except(:extra) # Removing extra as it can overflow some session stores
        redirect_to new_user_registration_url, alert: @user.errors.full_messages.join("\n")
      end
  end
end
```

`/app/models/user.rb`
```ruby
def self.from_omniauth(access_token)
    data = access_token.info
    user = User.where(email: data['email']).first

    unless user
      user = User.create(
        name: data['name'],
        email: data['email'],
        password: Devise.friendly_token[0,20]
      )
    end
    user
end
```

### Step 8 Views
```erb
<%= link_to "Sign in with Google", user_google_oauth2_omniauth_authorize_path %>
```

## Check Devise routes
```ruby
#config/routes.rb
Rails.application.routes.draw do  
  devise_for :users
  get 'pages/home'
  root 'pages#home'
end
```

`terminal`
```bash
        new_user_session GET    /users/sign_in(.:format)                                                                 devise/sessions#new
            user_session POST   /users/sign_in(.:format)                                                                 devise/sessions#create
    destroy_user_session DELETE /users/sign_out(.:format)                                                                devise/sessions#destroy
      new_user_password GET    /users/password/new(.:format)                                                            devise/passwords#new
      edit_user_password GET    /users/password/edit(.:format)                                                           devise/passwords#edit
          user_password PATCH  /users/password(.:format)                                                                devise/passwords#update
                        PUT    /users/password(.:format)                                                                devise/passwords#update
                        POST   /users/password(.:format)                                                                devise/passwords#create
cancel_user_registration GET    /users/cancel(.:format)                                                                  devise/registrations#cancel
  new_user_registration GET    /users/sign_up(.:format)                                                                 devise/registrations#new
  edit_user_registration GET    /users/edit(.:format)                                                                    devise/registrations#edit
      user_registration PATCH  /users(.:format)                                                                         devise/registrations#update
                        PUT    /users(.:format)                                                                         devise/registrations#update
                        DELETE /users(.:format)                                                                         devise/registrations#destroy
                        POST   /users(.:format)                                                                         devise/registrations#create
```

After...

```ruby
#config/routes.rb
Rails.application.routes.draw do  
  devise_for :users, skip: [:registrations, :passwords]
  get 'pages/home'
  root 'pages#home'
end
```


`terminal`
```bash
                     new_user_session GET      /users/sign_in(.:format)                                                                 devise/sessions#new
                         user_session POST     /users/sign_in(.:format)                                                                 devise/sessions#create
                 destroy_user_session DELETE   /users/sign_out(.:format)                                                                devise/sessions#destroy
user_google_oauth2_omniauth_authorize GET|POST /users/auth/google_oauth2(.:format)                                                      devise/omniauth_callbacks#passthru
 user_google_oauth2_omniauth_callback GET|POST /users/auth/google_oauth2/callback(.:format)                                             devise/omniauth_callbacks#google_oauth2
```