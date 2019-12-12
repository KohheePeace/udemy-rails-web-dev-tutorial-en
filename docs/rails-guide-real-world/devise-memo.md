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
```bash hl_lines="1"
rails generate devise:install
Running via Spring preloader in process 62116
      create  config/initializers/devise.rb
      create  config/locales/devise.en.yml
===============================================================================

Some setup you must do manually if you haven't yet:

  1. Ensure you have defined default url options in your environments files. Here
     is an example of default_url_options appropriate for a development environment
     in config/environments/development.rb:

       config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }

     In production, :host should be set to the actual host of your application.

  2. Ensure you have defined root_url to *something* in your config/routes.rb.
     For example:

       root to: "home#index"

  3. Ensure you have flash messages in app/views/layouts/application.html.erb.
     For example:

       <p class="notice"><%= notice %></p>
       <p class="alert"><%= alert %></p>

  4. You can copy Devise views (for customization) to your app by running:

       rails g devise:views

===============================================================================
```


## Step3 
`config/environments/development.rb`
```ruby
  ...
  # Config for devise
  config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

## Step4 Create User model with devise
`terminal`
```bash
rails generate devise User
Running via Spring preloader in process 62242
      invoke  active_record
      create    db/migrate/20191201172418_devise_create_users.rb
      create    app/models/user.rb
      invoke    test_unit
      create      test/models/user_test.rb
      create      test/fixtures/users.yml
      insert    app/models/user.rb
       route  devise_for :users
```

`db/migrate/20191201172418_devise_create_users.rb`
```ruby
# frozen_string_literal: true

class DeviseCreateUsers < ActiveRecord::Migration[6.0]
  def change
    create_table :users do |t|
      ## Database authenticatable
      t.string :email,              null: false, default: ""
      t.string :encrypted_password, null: false, default: ""

      ## Recoverable
      t.string   :reset_password_token
      t.datetime :reset_password_sent_at

      ## Rememberable
      t.datetime :remember_created_at

      ## Trackable
      # t.integer  :sign_in_count, default: 0, null: false
      # t.datetime :current_sign_in_at
      # t.datetime :last_sign_in_at
      # t.inet     :current_sign_in_ip
      # t.inet     :last_sign_in_ip

      ## Confirmable
      # t.string   :confirmation_token
      # t.datetime :confirmed_at
      # t.datetime :confirmation_sent_at
      # t.string   :unconfirmed_email # Only if using reconfirmable

      ## Lockable
      # t.integer  :failed_attempts, default: 0, null: false # Only if lock strategy is :failed_attempts
      # t.string   :unlock_token # Only if unlock strategy is :email or :both
      # t.datetime :locked_at


      t.timestamps null: false
    end

    add_index :users, :email,                unique: true
    add_index :users, :reset_password_token, unique: true
    # add_index :users, :confirmation_token,   unique: true
    # add_index :users, :unlock_token,         unique: true
  end
end
```

`app/models/user.rb`
```ruby
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
end
```

`config/routes.rb`
```ruby hl_lines="2"
Rails.application.routes.draw do
  devise_for :users
  get 'pages/home'
  root 'pages#home'
end
```


`terminal`
```bash
rails db:migrate
```

## Step4 Check migration file
https://github.com/plataformatec/devise/wiki/How-To:-Change-an-already-existing-table-to-add-devise-required-columns
```ruby
class AddDeviseToUsers < ActiveRecord::Migration[5.0]
  def change
    change_table :users do |t|
      ## Database authenticatable
      t.string :email#,              null: false, default: ""
      t.string :encrypted_password, null: false, default: ""

      ## Recoverable
      t.string   :reset_password_token
      t.datetime :reset_password_sent_at

      ## Rememberable
      t.datetime :remember_created_at

      ## Trackable
      t.integer  :sign_in_count, default: 0, null: false
      t.datetime :current_sign_in_at
      t.datetime :last_sign_in_at
      t.inet     :current_sign_in_ip
      t.inet     :last_sign_in_ip

      ## Confirmable
      # t.string   :confirmation_token
      # t.datetime :confirmed_at
      # t.datetime :confirmation_sent_at
      # t.string   :unconfirmed_email # Only if using reconfirmable

      ## Lockable
      # t.integer  :failed_attempts, default: 0, null: false # Only if lock strategy is :failed_attempts
      # t.string   :unlock_token # Only if unlock strategy is :email or :both
      # t.datetime :locked_at


    end

    add_index :users, :email,                unique: true
    add_index :users, :reset_password_token, unique: true
    # add_index :users, :confirmation_token,   unique: true
    # add_index :users, :unlock_token,         unique: true
  end
end
```


## Step5 Add `omniauth-google-oauth2` gem
https://github.com/zquestz/omniauth-google-oauth2

`Gemfile`
```
gem 'omniauth-google-oauth2'
```

`terminal`
```
bundle
```

## Step6 Google API Setup
1. Go to 'https://console.developers.google.com'
2. Select your project.
3. Go to Credentials, then select the "OAuth consent screen" tab on top, and provide an 'EMAIL ADDRESS' and a 'PRODUCT NAME'
4. Wait 10 minutes for changes to take effect.

## Step6.5 Create User model
```bash
rails g migration AddOmniauthToUsers name:string image:string google_uid:string:uniq
```

## Step7 Edit credentials
`terminal`
```
docker-compose run -e EDITOR="vim" web rails credentials:edit
```

```bash
google:
  client_id: fejioafjeioafhewhgweaifejaio
  client_secret: fjfoaiejfwncaeiowjfeiaofneoawnceawaw
```

## Step8
Edit `config/initializers/devise.rb`
```ruby
  # config.omniauth :github, 'APP_ID', 'APP_SECRET', scope: 'user,public_repo'
  config.omniauth :google_oauth2, Rails.application.credentials.google[:client_id], Rails.application.credentials.google[:client_secret], {
    scope: 'email,profile'
  }
```

## Step9
`config/routes.rb`
```ruby
Rails.application.routes.draw do
  devise_for :users, controllers: { omniauth_callbacks: 'users/omniauth_callbacks' }
  devise_scope :user do
    get 'sign_in', :to => 'devise/sessions#new', :as => :new_user_session
    get 'sign_out', :to => 'devise/sessions#destroy', :as => :destroy_user_session
  end
  ...
end
```
https://github.com/plataformatec/devise/wiki/OmniAuth:-Overview#using-omniauth-without-other-authentications

## Step10
`/app/models/user.rb`
```ruby
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :omniauthable, omniauth_providers: [:google_oauth2]
end
```

## Step11
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
    google_uid = access_token.uid
    data = access_token.info
    user = User.where(email: data['email']).first

    unless user
      user = User.create(
        google_uid: google_uid,
        image: data['image'],
        name: data['name'],
        email: data['email']
      )
    end
    user
  end
```

## Step 8 Views
```erb
<%= link_to "Sign in with Google", user_google_oauth2_omniauth_authorize_path %>
```
