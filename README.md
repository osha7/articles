# You can run database.yml through erb to test what you're getting:
erb config/database.yml

To make the default password secure:
https://stackoverflow.com/questions/18290/how-do-you-secure-database-yml

Rails stores secrets in config/credentials.yml.enc, which is encrypted and hence cannot be edited directly. We can edit the credentials by running the following command:

$ EDITOR=nano rails credentials:edit

secret_key_base: 3b7cd727ee24e8444053437c36cc66c3
default_dbpwd: <<my-secret-password>>
Now, these secrets can be accessed using Rails.application.credentials.

So your database.yml will look like this:

default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: <%= Rails.application.credentials.default_dbpwd %>
  socket: /tmp/mysql.sock

# README

rails new myarticles -d=mysql --api

https://www.youtube.com/watch?v=QojnRc7SS9o

https://github.com/bradtraversy/simple-rails-rest/blob/master/app/controllers/api/v1/articles_controller.rb


