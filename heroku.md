# Heroku notes

- Super flexible deployment platform
- Easy Git and CLI integration
- Deploy the same you would push to a repo

## Creating a heroku app

First, make sure you have the heroku CLI tools installed (on a Mac, `brew` is a good option).

```
heroku create # creates new Heroku app
git push heroku master # pushes master git branch to heroku for deployment
heroku rename [new name] # renames the app, new URL is [new name].herokuapp.com
heroku open # opens app at [app name].herokuapp.com
heroku logs --tail # tails the logs from the live heroku app
```

```
heroku local # runs the app up locally as it would be deployed on Heroku
```

It's worth noting that if you have a

```ruby
group :development, :test do
  .
  .
  .
end
```

group in your Gemfile, Heroku *doesn't* build with this. It will use the `:production` group.
