## MVC (model - view - controller)

Separates code and data from the way they are displayed.

**Models** are your content and interaction models (a User will need to have a list of all instances of the class, detailed views for each instance/user, the ability to add, modify, delete, etc).

**Views** are template HTML/erb files into which information we want to present to the user is interpolated. They're also ruby files, so they can do some work on their own (this shouldn't be extensive. Separation of concerns and all that).

**Controllers** figure out which model is being called, which methods to use, and which views to fill out. This works hand in hand with your `config/routes.rb` file, which determines the type of request, and hands it to the right controller to finish the work.

## Example

Browser requests `/users`

This hits `config/routes.rb`, which sees that there was a `GET` request for `'/users'`. It checks itself and finds

```ruby
get '/users', to: 'users#index'
```

which tells it when you see a `GET` request for `'/users'`, send that to the `user_controller.rb` file and use the method `index`, which will probably show a list/index of all users in the system.

It hands this over to the controller, which queries the databse (or whatever) for the user list, and then grabs the view it needs for this.

The view receives all the information, gets compiled, and the controller hands this back to the browser.

## Notes

Not all methods in a controller will render out a view--some of them will be called by other methods, and their job may be database related, or whatever.6
