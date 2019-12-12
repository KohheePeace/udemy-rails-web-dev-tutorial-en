`app/views/pages/settings.html.erb`
```erb
<h1>Settings here</h1>
<%= link_to "Change Email", user_google_oauth2_omniauth_authorize_path %>
```


`app/controllers/users/omniauth_callbacks_controller.rb`
```ruby hl_lines="3 4 5 6 7 8 9 10 11 12"
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def google_oauth2
    if user_signed_in?
      data = request.env['omniauth.auth'].info
      current_user.email = data['email']

      if current_user.save
        redirect_to settings_url, success: 'Email updated.'
      else
        redirect_to settings_url, alert: current_user.errors.full_messages.join("\n")
      end
    else
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
end
```
