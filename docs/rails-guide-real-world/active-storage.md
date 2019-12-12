!!! info
    GoogleのCORSの設定が面倒だったので、AWSに変更する。

https://guides.rubyonrails.org/active_storage_overview.html

## Setup Rails side

`terminal`
```bash
rails active_storage:install
Copied migration 20191203231057_create_active_storage_tables.active_storage.rb from active_storage
```

`20191203231057_create_active_storage_tables.active_storage.rb`
```ruby
# This migration comes from active_storage (originally 20170806125915)
class CreateActiveStorageTables < ActiveRecord::Migration[5.2]
  def change
    create_table :active_storage_blobs do |t|
      t.string   :key,        null: false
      t.string   :filename,   null: false
      t.string   :content_type
      t.text     :metadata
      t.bigint   :byte_size,  null: false
      t.string   :checksum,   null: false
      t.datetime :created_at, null: false

      t.index [ :key ], unique: true
    end

    create_table :active_storage_attachments do |t|
      t.string     :name,     null: false
      t.references :record,   null: false, polymorphic: true, index: false
      t.references :blob,     null: false

      t.datetime :created_at, null: false

      t.index [ :record_type, :record_id, :name, :blob_id ], name: "index_active_storage_attachments_uniqueness", unique: true
      t.foreign_key :active_storage_blobs, column: :blob_id
    end
  end
end
```

```bash
rails db:migrate
```


`Gemfile`
```
...
gem "google-cloud-storage", "~> 1.11", require: false
```

```bash
bundle
```

## Setup Google cloud side
https://medium.com/@pjbelo/setting-up-rails-5-2-active-storage-using-google-cloud-storage-and-heroku-23df91e830f8


Go to console
https://console.cloud.google.com/


## Edit `storage.yml`
```yaml hl_lines="18 19 20 21 22"
test:
  service: Disk
  root: <%= Rails.root.join("tmp/storage") %>

local:
  service: Disk
  root: <%= Rails.root.join("storage") %>

# Use rails credentials:edit to set the AWS secrets (as aws:access_key_id|secret_access_key)
# amazon:
#   service: S3
#   access_key_id: <%= Rails.application.credentials.dig(:aws, :access_key_id) %>
#   secret_access_key: <%= Rails.application.credentials.dig(:aws, :secret_access_key) %>
#   region: us-east-1
#   bucket: your_own_bucket

# Remember not to checkin your GCS keyfile to a repository
google:
  service: GCS
  project: Kakuru
  credentials: <%= Rails.application.credentials.gcs_storage.to_json %>
  bucket: text_bucket_1

# Use rails credentials:edit to set the Azure Storage secret (as azure_storage:storage_access_key)
# microsoft:
#   service: AzureStorage
#   storage_account_name: your_account_name
#   storage_access_key: <%= Rails.application.credentials.dig(:azure_storage, :storage_access_key) %>
#   container: your_container_name

# mirror:
#   service: Mirror
#   primary: local
#   mirrors: [ amazon, google, microsoft ]
```


## Edit Credentials
`termianl`
```bash
EDITOR="code --wait" bin/rails credentials:edit
```

This is a download key of json...
```json
{
  "type": "service_account",
  "project_id": "fjeioafhewa-190913",
  "private_key_id": "feajohfeoa",
  "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQDG1NKHBdKIJQT+\nSo183KHbYJLV1pVZmqMDcO4djTfdqNiPJfxt0+u7GJJ2zXzX7vHZS/bLJvsS6yN5\numH+HYerZXa2k5vofd4IcZn91t/GJRLbrLv3lBNOwMrGvSvd3H1uxBZ9lXST1PaR\n1ggYiOJWG+mfoea/grYq2\neZqaH/L7fOKuIs8B/ItBQR05bMWcfAE1HnmOKzmpqs84Dj4IndnXAoMg4UVN7mPn\nw5Flvgh5LesTr4oCNHpyS4AkfYmw8cMhjqkNBYWqK0tShqp8htATOk0tTAtRG+g+\nEDWu7h5rAgMBAAECggEADgC8CO1Ui+kLhnsqpsIFFiWhgbTYlNRqqZng8yzYY+B5\ny+8RbYywu975patIIQ7/cl3CtkD7CrSLrY1+TD65KM1/BFG197QxmGejwDhLTzGa\nN+Vc4Y1IpNG4FjIJblkSbmQZ72NAsA6eBNxNeqjdQ9I3jfieaofjeaw4XEoJ2cblpwzp02rSGNI\n9zshMjMoeNnoCUum3thg6X38UuczPman++PBwtfkrsyc7jbZluJnqQtwfEEwuf1+\nIRrduxCmu74SOdLqeN00xLf/t5OLtP5MLaaEFbydu8syltB9N+ZChoSCFAcbCFtW\njlTNi2nclcgtWh3SwkwnKXz4CVVOPF1uB/RNGolTdQKBgQD1PvyLXfvTkrb5rjtX\fjeiowafjwa/Ix8UBUxjqNjTPxcfpQ4ptuA8bMsuoAwapbDdBGt\n5mlqbJM/5tNjYskNreXtfJaIq2F/gx2lWtxwsrh7UUwDgbTeKFWkkr0ej9TNnoRV\nQch3WcgcBdieOAaMGwI72qb1XwKBgQDPjM6NetyC+2emOW2AhEfDpBvJLU2yjzVQ\nBofzK5iW2fuXUzjOPz0r3gV+N1sPvJGaGtGda/RfVZupCw62I7hhOIddptzOx+W8\ngcQHrcR+z354YGTagn0Jnzx1wBNR6Rvz8JP1ryV8yCbIkKPpAo/livyTlpWWxUtA\nDNmdC3hGdQKBgQDjhBaIOJ2KLz7+rSuyOOEe4hqChXdWv1CcyKDDmVlIYhn2rdir\ni/d6BQ7NxEQ/tlRG8HPX2AFaaVgKZWCNYweCys1kaADN3/RDc4OuaXnBurSNthbH\ns150Uukgxk/tpOQlgWfKcLNwaeDzDM8ZxRhz2N/zV10Zk0JHsjrFSli/owKBgQCX\nap52UR/23vrrJhJhJCBG9r7eshJxJlE6pMkh+rhDtZv69lgG/9Pc4QkY38GrZWLE\nDrTGKDAMLSR22v5Mmxq0sszu4gFNSkCsme8tuvQTn8UghRKO54vZLTaqoQp3Q52F\nBgqrvq+WrV6+C+fI4nmgeRlzgvR3HlCb1cQc8nU40QKBgD2hTUf1e8/IoDBxBnom\nlLv6tXLE4klczAr1dtksz1PW9OqbFo5wHkecDeEsR/WXnxOuQ+WUeQYTLywIAP+W\ndv5EoeKIQwZAmVoFx/+hHqfr3fK+M5MWMHFl6OrkPLP8N6HrzTCq2L/9t9BZwpKj\nue2l0/Bqv9Zn2RLlErD8Yeqe\n-----END PRIVATE KEY-----\n",
  "client_email": "rails-active-storage-teser@fekoafewajoi-190913.iam.gserviceaccount.com",
  "client_id": "fjewioafe",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/rails-active-storage-teser%fejaiofwe-190913.iam.gserviceaccount.com"
}
```

```
1. Copy and paste this to vscode editor
2. Delete {} and ""
3. Only `private_key` needes double quotes "", so add "" to it.
4. Paste this to credentials
```

```yaml
google:
  client_id: 506850218952-adm8bestc98siuoegh1u5f5e87df8r9b.apps.googleusercontent.com
  client_secret: o-7wXKl7EYiW85pZdsg-Cdo6
gcs_storage:
  type: service_account
  project_id: fjeioafeawp
  private_key_id: jiojohifenaowifwnao
  private_key: "-----BEGIN PRIVATE KEY-----\joij+\nSo183KHbYJLV1pVZmqMDcO4djTfdqNiPJfxt0+u7GJJ2zXzX7vHZS/bLJvsS6yN5\numH+HYerZXa2k5vofd4IcZn91t/GJRLbrLv3lBNOwMrGvSvd3H1uxBZ9lXST1PaR\n1ggYiOJWG+fjeawoif/grYq2\neZqaH/L7fOKuIs8B/ItBQR05bMWcfAE1HnmOKzmpqs84Dj4IndnXAoMg4UVN7mPn\nw5Flvgh5LesTr4oCNHpyS4AkfYmw8cMhjqkNBYWqK0tShqp8htATOk0tTAtRG+g+\nEDWu7h5rAgMBAAECggEADgC8CO1Ui+kLhnsqpsIFFiWhgbTYlNRqqZng8yzYY+B5\ny+8RbYywu975patIIQ7/cl3CtkD7CrSLrY1+TD65KM1/BFG197QxmGejwDhLTzGa\nN+Vc4Y1IpNG4FjIJblkSbmQZ72NAsA6eBNxNeqjdQ9I34XEoJ2cblpwzp02rSGNI\n9zshMjMoeNnoCUum3thg6X38UuczPman++PBwtfkrsyc7jbZluJnqQtwfEEwuf1+\nIRrduxCmu74SOdLqeN00xLf/t5OLtP5MLaaEFbydu8syltB9N+ZChoSCFAcbCFtW\njlTNi2nclcgtWh3SwkwnKXz4CVVOPF1uB/RNGolTdQKBgQD1PvyLXfvTkrb5rjtX\ncaDqUyX2DfHlOS5wZyHmhJhp/Ix8UBUxjqNjTPxcfpQ4ptuA8bMsuoAwapbDdBGt\n5mlqbJM/5tNjYskNreXtfJaIq2F/gx2lWtxwsrh7UUwDgbTeKFWkkr0ej9TNnoRV\jiofea+2emOW2AhEfDpBvJLU2yjzVQ\nBofzK5iW2fuXUzjOPz0r3gV+N1sPvJGaGtGda/RfVZupCw62I7hhOIddptzOx+W8\ngcQHrcR+z354YGTagn0Jnzx1wBNR6Rvz8JP1ryV8yCbIkKPpAo/livyTlpWWxUtA\nDNmdC3hGdQKBgQDjhBaIOJ2KLz7+rSuyOOEe4hqChXdWv1CcyKDDmVlIYhn2rdir\ni/d6BQ7NxEQ/tlRG8HPX2AFaaVgKZWCNYweCys1kaADN3/RDc4OuaXnBurSNthbH\ns150Uukgxk/tpOQlgWfKcLNwaeDzDM8ZxRhz2N/zV10Zk0JHsjrFSli/owKBgQCX\nap52UR/23vrrJhJhJCBG9r7eshJxJlE6pMkh+rhDtZv69lgG/9Pc4QkY38GrZWLE\nDrTGKDAMLSR22v5Mmxq0sszu4gFNSkCsme8tuvQTn8UghRKO54vZLTaqoQp3Q52F\nBgqrvq+WrV6+C+fI4nmgeRlzgvR3HlCb1cQc8nU40QKBgD2hTUf1e8/IoDBxBnom\nlLv6tXLE4klczAr1dtksz1PW9OqbFo5wHkecDeEsR/WXnxOuQ+WUeQYTLywIAP+W\ndv5EoeKIQwZAmVoFx/+hHqfr3fK+M5MWMHFl6OrkPLP8N6HrzTCq2L/9t9BZwpKj\nue2l0/Bqv9Zn2RLlErD8Yeqe\n-----END PRIVATE KEY-----\n"
  client_email: rails-active-storage-teser@joijojfeawhoi.iam.gserviceaccount.com
  client_id: jiofoiwejfawe
  auth_uri: https://accounts.google.com/o/oauth2/auth
  token_uri: https://oauth2.googleapis.com/token
  auth_provider_x509_cert_url: https://www.googleapis.com/oauth2/v1/certs
  client_x509_cert_url: https://www.googleapis.com/robot/v1/metadata/x509/rails-active-storage-teser%40fjeioafeawp.iam.gserviceaccount.com
```

## Environment Settings
Edit below code...

`config/environments/development.rb`
```ruby
  ...
  config.active_storage.service = :google
```

`config/environments/production.rb`
```ruby
  config.active_storage.service = :google
```


## Enable gcs json-api
![../img/rails-guide-real-world/enable-gcs-json-api.png](../img/rails-guide-real-world/enable-gcs-json-api.png)


## Edit model
`models/user.rb`
```ruby hl_lines="10"
class User < ApplicationRecord
  extend FriendlyId
  friendly_id :name, use: :slugged, slug_column: :username

  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :omniauthable, omniauth_providers: [:google_oauth2]

  has_many :posts, dependent: :destroy
  has_one_attached :avatar
...
end
```

!!! note
    - `image` column for default google image url
    - `avatar` => you don't need column but for active storage avatar.

## Edit form

```erb
<%= form.file_field :avatar %>
```

## Edit show page and Navbar
`app/views/users/show.html.erb`
```erb
<% if @user.avatar.attached? %>
  <%= image_tag(url_for(@user.avatar), width: 200, class: "navbar-avatar-img") %>
<% else %>
  <img src="<%= @user.image %>" alt="" class="navbar-avatar-img">
<% end %>
```

and

Navbar

`app/views/shared/_navbar.html.erb`
```erb
  <% if current_user.avatar.attached? %>
    <%= image_tag(url_for(current_user.avatar), width: 200, class: "navbar-avatar-img") %>
  <% else %>
    <img src="<%= current_user.image %>" alt="" class="navbar-avatar-img">
  <% end %>
```

## Controller
```ruby hl_lines="2"
def user_params
  params.require(:user).permit(:name, :avatar)
end
```


## Image Preview...
https://apidock.com/rails/ActionView/Helpers/FormHelper/file_field

https://stackoverflow.com/questions/4459379/preview-an-image-before-it-is-uploaded