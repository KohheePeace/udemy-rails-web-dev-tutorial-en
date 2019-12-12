Instead of `slug` we are using `username`
`terminal`
```bash
bundle
rails g migration AddUsernameToUsers username:uniq
rails db:migrate
```

## 大まかな流れ
とりあえず、emailの頭をusernameにする。
