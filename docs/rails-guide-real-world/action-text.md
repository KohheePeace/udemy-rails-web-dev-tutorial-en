## Ref
https://edgeguides.rubyonrails.org/action_text_overview.html

## Start

`terminal`
```bash
rails action_text:install
Copying actiontext.scss to app/assets/stylesheets
      create  app/assets/stylesheets/actiontext.scss
Copying fixtures to test/fixtures/action_text/rich_texts.yml
      create  test/fixtures/action_text/rich_texts.yml
Copying blob rendering partial to app/views/active_storage/blobs/_blob.html.erb
      create  app/views/active_storage/blobs/_blob.html.erb
Installing JavaScript dependencies
         run  yarn add trix@^1.0.0 @rails/actiontext@^6.0.1 from "."
yarn add v1.15.2
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > webpack-dev-server@3.9.0" has unmet peer dependency "webpack@^4.0.0".
warning "webpack-dev-server > webpack-dev-middleware@3.7.2" has unmet peer dependency "webpack@^4.0.0".
[4/4] 🔨  Building fresh packages...
success Saved lockfile.
warning Your current version of Yarn is out of date. The latest version is "1.19.2", while you're on "1.15.2".
info To upgrade, run the following command:
$ brew upgrade yarn
success Saved 2 new dependencies.
info Direct dependencies
├─ @rails/actiontext@6.0.1
└─ trix@1.2.2
info All dependencies
├─ @rails/actiontext@6.0.1
└─ trix@1.2.2
✨  Done in 11.84s.
Adding trix to app/javascript/packs/application.js
      append  app/javascript/packs/application.js
Adding @rails/actiontext to app/javascript/packs/application.js
      append  app/javascript/packs/application.js
Copied migration 20191202185130_create_active_storage_tables.active_storage.rb from active_storage
Copied migration 20191202185131_create_action_text_tables.action_text.rb from action_text
```


```bash
rails db:migrate
```

## Active Model Storage with google cloud.

```ruby
# app/models/post.rb
class Post < ApplicationRecord
  ...
  has_rich_text :content
end
```

`app/views/posts/_form.html.erb`
```erb
  <div class="field">
    <%= form.label :content %>
    <%= form.rich_text_area :content %>
  </div>
```

## 10.2 Cross-Origin Resource Sharing (CORS) configuration
https://edgeguides.rubyonrails.org/active_storage_overview.html#cross-origin-resource-sharing-cors-configuration

### Install gsutil
https://cloud.google.com/storage/docs/gsutil_install

