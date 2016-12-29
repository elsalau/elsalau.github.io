---
layout: post
title:  "[Line Login] Integrate Line Login with Rails 4"
date:   2016-10-06 12:38:52 +0800
categories: line rails4
---

Recently I got a task to create a website with Line Login feature. This feature allows users to login with their Line account to 3rd party websites by using OAuth2.0.

After user login and grant priveleges to 3rd party website, Line will provide following user information:

1. User's nickname
2. User's ID
3. User's profile image URL
4. User's statue message

```
{
  "displayName":"Brown",
  "mid":"u0047556f2e40dba2456887320ba7c76d",
  "pictureUrl":"http://example.com/abcdefghijklmn",
  "statusMessage":"Hello, LINE!"
}
```

and the pictureUrl supports 2 sizes:

```
# Profile image thumbnails
  200x200: http://example.com/abcdefghijklmn/large
  51x51:   http://example.com/abcdefghijklmn/small

```

[Line's developer site](https://developers.line.me/) suggest to implement Line Login with following steps:

1. Create a business account at the Business Center
2. Select LINE Login on your business account page
3. Create a Channel
4. Integrate LINE’s user authentication process into website
5. Use REST APIs from website
6. Test website
7. Publish website

The most important steps should be step 4, and here's
how I implemented it with Rails 4

### Framwork

- Ruby on Rails
  - Ruby:  2.2.5
  - Rails: 4.2.7
  - Gems: [omniauth-line](https://github.com/kazasiki/omniauth-line)

### MVC
- User model
  - Stores user infomation after authentiation & authorization

- Pages controller
  - index action
    - render view

- Sessions controller
  - create action
      - login
      - Uses Omniauth to get user data from Line
  - destroy action
      - logout

- Index view
  - Display welcome message and button to login
  - Display user profile after login

### How to integrate
**Line channel configuration:**

- Add production callback url, the link should look like this:
  {% highlight bash %}
  https://example.com/auth/line/callback
  #https is mandatory
  {% endhighlight %}

**Rails configuration:**

- Install 'omniauth-line' gem
  {% highlight bash %}
  $gem install omniauth-line
  {% endhighlight %}

- Configure provider infomation
  {% highlight ruby %}
  #config/initializers/omniauth.rb
  Rails.application.config.middleware.use OmniAuth::Builder do
    provider :line, ENV['CHANNEL_ID'], ENV['CHANNEL_SECRET']
  end
  OmniAuth.config.on_failure = Proc.new do |env|
    SessionsController.action(:action_failure).call(env)
  end
  {% endhighlight %}

- Configure routes for callback and logout
  {% highlight ruby %}
  Rails.application.routes.draw do
    root 'pages#index'
    get '/auth/:provider/callback', to: 'sessions#create'
    delete '/logout', to: 'sessions#destroy'
  end
  {% endhighlight %}

- Configure Sessions Controller for create, destroy action
  {% highlight ruby %}
  def create
    begin
      @user = User.from_omniauth(request.env['omniauth.auth'])
      session[:user_id] = @user.id
      flash[:success] = "Welcome, #{@user.username}!"
    rescue
      flash[:warning] = "There was an error occured..."
    end
    redirect_to root_path
  end

  def destroy
    if current_user
      session.delete(:user_id)
      flash[:success] = 'Ciao!'
    end
    redirect_to root_path
  end

  def auth_failure
    redirect_to root_path
  end
  {% endhighlight %}

- Generate migration file to store user data
  {% highlight ruby %}
  create_table :users do |t|
    t.string :provider, null: false
    t.string :uid, null: false
    t.string :access_token
    t.string :username
    t.string :image_url
    t.string :status_msg
    t.timestamps null: false
  end

  add_index :users, :provider
  add_index :users, :uid
  add_index :users, [:provider, :uid], unique: true
  {% endhighlight %}
- Configure user.rb to save user data
  {% highlight ruby %}
  class << self
    def from_omniauth(auth_hash)
      user = find_or_create_by(uid: auth_hash['uid'], provider: auth_hash['provider'])
      user.username = auth_hash['info']['name']
      user.image_url = auth_hash['info']['image']
      user.status_msg = auth_hash['info']['description']
      user.access_token = auth_hash['credentials']['token']
      user.save!
      user
    end
  end
  {% endhighlight %}
- Configure views to display user info after user login

all the works should be done by now!


Note:

Sometimes Line Login service is not stable, you may encountered issues to login, or not redirecting after login, if you're sure the callback url you configure is correct, maybe Line service is down.


[My sample repo](https://github.com/elsalau/line-login-demo)


