!!! abstract "Chapter Goal"
    - Check best practice of routes provided by rails


Ref: https://guides.rubyonrails.org/getting_started.html#getting-up-and-running


In official Rails guide they introduce

```ruby
resources :articles
```

This is a **method** to ==create best practice routes for **CRUD**==.

[As mentioned in part overview, there is a "best" way to do things in rails...](http://localhost:8000/rails-guide-basics/overview/#2-what-is-rails)

Let's add this and check it.

## Check routes of **before**

Before adding `resources :articles`, let's check current routes as you can see the difference of before and after.

`terminal`
```bash
docker-compose run web rails routes
```

Output is ...

You can see routes you wrote in last chapter, and the default routes. 

```bash hl_lines="2 3 4"
                               Prefix Verb   URI Pattern                                                                              Controller#Action
                        welcome_index GET    /welcome/index(.:format)                                                                 welcome#index
                       hello_hogehoge GET    /hello/hogehoge(.:format)                                                                hello#hogehoge
                                 root GET    /                                                                                        hello#hogehoge
        rails_mandrill_inbound_emails POST   /rails/action_mailbox/mandrill/inbound_emails(.:format)                                  action_mailbox/ingresses/mandrill/inbound_emails#create
        rails_postmark_inbound_emails POST   /rails/action_mailbox/postmark/inbound_emails(.:format)                                  action_mailbox/ingresses/postmark/inbound_emails#create
           rails_relay_inbound_emails POST   /rails/action_mailbox/relay/inbound_emails(.:format)                                     action_mailbox/ingresses/relay/inbound_emails#create
        rails_sendgrid_inbound_emails POST   /rails/action_mailbox/sendgrid/inbound_emails(.:format)                                  action_mailbox/ingresses/sendgrid/inbound_emails#create
         rails_mailgun_inbound_emails POST   /rails/action_mailbox/mailgun/inbound_emails/mime(.:format)                              action_mailbox/ingresses/mailgun/inbound_emails#create
       rails_conductor_inbound_emails GET    /rails/conductor/action_mailbox/inbound_emails(.:format)                                 rails/conductor/action_mailbox/inbound_emails#index
                                      POST   /rails/conductor/action_mailbox/inbound_emails(.:format)                                 rails/conductor/action_mailbox/inbound_emails#create
    new_rails_conductor_inbound_email GET    /rails/conductor/action_mailbox/inbound_emails/new(.:format)                             rails/conductor/action_mailbox/inbound_emails#new
   edit_rails_conductor_inbound_email GET    /rails/conductor/action_mailbox/inbound_emails/:id/edit(.:format)                        rails/conductor/action_mailbox/inbound_emails#edit
        rails_conductor_inbound_email GET    /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#show
                                      PATCH  /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#update
                                      PUT    /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#update
                                      DELETE /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#destroy
rails_conductor_inbound_email_reroute POST   /rails/conductor/action_mailbox/:inbound_email_id/reroute(.:format)                      rails/conductor/action_mailbox/reroutes#create
                   rails_service_blob GET    /rails/active_storage/blobs/:signed_id/*filename(.:format)                               active_storage/blobs#show
            rails_blob_representation GET    /rails/active_storage/representations/:signed_blob_id/:variation_key/*filename(.:format) active_storage/representations#show
                   rails_disk_service GET    /rails/active_storage/disk/:encoded_key/*filename(.:format)                              active_storage/disk#show
            update_rails_disk_service PUT    /rails/active_storage/disk/:encoded_token(.:format)                                      active_storage/disk#update
                 rails_direct_uploads POST   /rails/active_storage/direct_uploads(.:format)                                           active_storage/direct_uploads#create
```

## Check routes of **after**

Okay, so add resources...

`routes.rb`
```ruby hl_lines="5"
Rails.application.routes.draw do
  get 'welcome/index'
  get 'hello/hogehoge'
  
  resources :articles

  root 'hello#hogehoge'
end
```

`terminal`
```bash
docker-compose run web rails routes
```

Output is ...

```bash hl_lines="4 5 6 7 8 9 10 11"
                               Prefix Verb   URI Pattern                                                                              Controller#Action
                        welcome_index GET    /welcome/index(.:format)                                                                 welcome#index
                       hello_hogehoge GET    /hello/hogehoge(.:format)                                                                hello#hogehoge
                             articles GET    /articles(.:format)                                                                      articles#index
                                      POST   /articles(.:format)                                                                      articles#create
                          new_article GET    /articles/new(.:format)                                                                  articles#new
                         edit_article GET    /articles/:id/edit(.:format)                                                             articles#edit
                              article GET    /articles/:id(.:format)                                                                  articles#show
                                      PATCH  /articles/:id(.:format)                                                                  articles#update
                                      PUT    /articles/:id(.:format)                                                                  articles#update
                                      DELETE /articles/:id(.:format)                                                                  articles#destroy
                                 root GET    /                                                                                        hello#hogehoge
        rails_mandrill_inbound_emails POST   /rails/action_mailbox/mandrill/inbound_emails(.:format)                                  action_mailbox/ingresses/mandrill/inbound_emails#create
        rails_postmark_inbound_emails POST   /rails/action_mailbox/postmark/inbound_emails(.:format)                                  action_mailbox/ingresses/postmark/inbound_emails#create
           rails_relay_inbound_emails POST   /rails/action_mailbox/relay/inbound_emails(.:format)                                     action_mailbox/ingresses/relay/inbound_emails#create
        rails_sendgrid_inbound_emails POST   /rails/action_mailbox/sendgrid/inbound_emails(.:format)                                  action_mailbox/ingresses/sendgrid/inbound_emails#create
         rails_mailgun_inbound_emails POST   /rails/action_mailbox/mailgun/inbound_emails/mime(.:format)                              action_mailbox/ingresses/mailgun/inbound_emails#create
       rails_conductor_inbound_emails GET    /rails/conductor/action_mailbox/inbound_emails(.:format)                                 rails/conductor/action_mailbox/inbound_emails#index
                                      POST   /rails/conductor/action_mailbox/inbound_emails(.:format)                                 rails/conductor/action_mailbox/inbound_emails#create
    new_rails_conductor_inbound_email GET    /rails/conductor/action_mailbox/inbound_emails/new(.:format)                             rails/conductor/action_mailbox/inbound_emails#new
   edit_rails_conductor_inbound_email GET    /rails/conductor/action_mailbox/inbound_emails/:id/edit(.:format)                        rails/conductor/action_mailbox/inbound_emails#edit
        rails_conductor_inbound_email GET    /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#show
                                      PATCH  /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#update
                                      PUT    /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#update
                                      DELETE /rails/conductor/action_mailbox/inbound_emails/:id(.:format)                             rails/conductor/action_mailbox/inbound_emails#destroy
rails_conductor_inbound_email_reroute POST   /rails/conductor/action_mailbox/:inbound_email_id/reroute(.:format)                      rails/conductor/action_mailbox/reroutes#create
                   rails_service_blob GET    /rails/active_storage/blobs/:signed_id/*filename(.:format)                               active_storage/blobs#show
            rails_blob_representation GET    /rails/active_storage/representations/:signed_blob_id/:variation_key/*filename(.:format) active_storage/representations#show
                   rails_disk_service GET    /rails/active_storage/disk/:encoded_key/*filename(.:format)                              active_storage/disk#show
            update_rails_disk_service PUT    /rails/active_storage/disk/:encoded_token(.:format)                                      active_storage/disk#update
                 rails_direct_uploads POST   /rails/active_storage/direct_uploads(.:format)                                           active_storage/direct_uploads#create
```

==You see rails automatically generates **routings for CRUD**.==

This is useful after you understand get used to rails, but for beginners it ia a little bit difficult.

So, in the next chapter, we will be doing the same thing **step by step**.