# DEVISE WITH JWT Authentication

In this project, an API for user authentication was implemented using the JSON Web Token (JWT) devise.

The following technologies were used for this:

- ruby 2.6.5
- rails 6.1.7
- pg 1.1

How to set up:

1. Clone this project
2. In the project folder run the command `bundle install`
3. Generate a token with `rake secret` and copy the value displayed on .env file. The project has a .env.example as a template
4. Run the commands to create the databases
   a. `rails db:create`
   b. `rails db:migrate`

After configuration, it is possible to run the project (`rails s`) and make tests to access the endpoints.

Some sample tests that might be helpful

1. Try to access an authenticated controller without a JWT token
   * `$ curl -XGET -H "Content-Type: application/json" http://localhost:3000/member-data`
   (Esperado que request falhe pela falta de autenticação)

2. Register an account
   * `$ curl -XPOST -H "Content-Type: application/json" -d '{ "user": { "email": "test@email.com", "password": "12345678" } }' http://localhost:3000/users`

3. Login with registered account
   * `$ curl -XPOST -H "Content-Type: application/json" -d '{ "user": { "email": "test@email.com", "password": "12345678" } }' http://localhost:3000/users/sign_in`

4. It is possible to add the `-i` flag in the request above to get the JWT token and evaluate that it is possible to login with just the token

   a. Getting the token in the header
   * `$ curl -XPOST -H "Content-Type: application/json" -i -d '{ "user": { "email": "test@email.com", "password": "12345678" } }' http://localhost:3000/users/sign_in`

   b. Logging in with the obtained token
   * `$ curl -XGET -H "Authorization: Bearer <TOKEN JWT HERE>" -H "Content-Type: application/json" http://localhost:3000/member-data`

5. Finally, we can logout, which includes the JWT Token in the deny list and does not allow it to be used again for login (ps: a new token is generated with each new login)
   * `$ curl -XDELETE -H "Authorization: Bearer <TOKEN JWT HERE>" -H "Content-Type: application/json" http://localhost:3000/users/sign_out`
