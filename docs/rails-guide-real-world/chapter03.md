## Authentication with Devise gem


## Step1
`Gemfile`
```
gem 'devise'
```

`terminal`
```bash
docker-compose run web bundle
```

## Step2
`terminal`
```bash
rails generate devise:install
```

## Step3
`config/environments/development.rb`
Add below code to the bottom...
```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

## Step4
`terminal`
```bash
rails generate devise User
```

`termianl`
```bash
docker-compose run web rails db:migrate
```

## Step5
`terminal`
```bash
rails generate devise:views
```