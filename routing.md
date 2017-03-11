# Routing in Rails

## Controllers and routers

The controllers determine what information is returned to the browser. But the routers (`config/routes.rb`) help determine which controllers/methods to use based on what the browser has requested.

A basic route would look like this:

```
get '/goodbye', to: 'application#goodbye'
```

where `get` is the HTTP method being received, `/goodbye` is the resource requested/updated, and in `application#goodbye` `application` references *which* controller file (named `application_controller.rb` or `foo_controller.rb` if referenced by `foo#goodbye`), and `goodbye` denotes the method to use within that controller. (whoof. that was a sentence.)

*[More on routing](http://guides.rubyonrails.org/routing.html)* @todo('read up on Rails routing')

### Redirecting

You can redirect in `config/routes.rb` too. It looks like this:

```
get '/redirect-me', to: redirect('/new-destination')

get '/new-destination', to: 'application#new_destination_method'
```

## Resource(s)

These are super important. Rich on Rails has a [good article](https://richonrails.com/articles/understanding-rails-routing) breaking this down. Good thing to note:

Resources are kinda like modules for common routing patterns. If you have a user model, chances are you'll want all kinds of `GET`, `POST` whatever actions on a bunch of different views, with different controllers...

Rather than force you to write it all out by hand, you can declare `resources :users` in your route file, or `resource :users` or whatever symbol is appropriate. Generally, if the thing is an instance of a class (like user Mike is of class User), use `resources`, with the 's'. If it's a one off (say, your home page), user `resource`, no 's'.
