<h1>How to install Devise in Rails 3.x</h1>

Devise is a flexible authentication solution for Rails based on Warden. Devise handles authentication across the entire stack. It has the following features

Rack based
MVC based on Rails engines
Allows you to have multiple roles (or models/scopes) signed in at the same time
Modularity concept: use just what you really need
It’s composed of 12 modules:

Database Authenticatable
Token Authenticatable
Omniauthable
Confirmable
Recoverable
Registerable
Rememberable
Trackable
Timeoutable
Validatable
Lockable
Steps to install the Devise

Step#1

Add the following gem in your Gemfile

    gem 'devise'

Then run

bundle install
Step#2

To invoke the Devise in your application, run the devise generator

 rails g devise:install
The generator will install an initialize, which describes all devise’s configuration options.

Step#3

Create a model “User” using devise to handle authentication.

 rails g devise User
This generator creates a few interesting things like a model file, a migration and a devise_for in route.

Step#4

Run the migration

 rake db:migrate
Step#5

Devise provides some helper methods to recognize a user after sign in and default route paths for “sign in”, “sign up” and “sign out”.
We can modify our ‘app/views/layout/application.html.erb’ file to allow us to “sign out”, “sign in” and “sign up” by writing the following block

 <div>
<% if user_signed_in? %>
Signed in as <%= current_user.email %>. Not you?
<%= link_to "Sign out", destroy_user_session_path,:method => :delete %>
<% else %>
<%= link_to "Sign up", new_user_registration_path %> or
<%= link_to "Sign in", new_user_session_path %>
<% end %>
</div>
Configuring views

Since Devise is an engine, all its views are packaged inside the devise gem.
Get all the view files for devise by running the following generate command

 rails generate devise:views
You can also configure the message language, mailer from address and other things by editing the devise config files as located in following locations

devise.en.yml – config/locales
devise.rb – config/initializers
Then you are done to use the app with authentication!
