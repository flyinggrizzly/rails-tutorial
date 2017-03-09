## MVC (model - view - controller)

Separates code and data from the way they are displayed.

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
