# Heroku notes

- Super flexible deployment platform
- Easy Git and CLI integration
- Deploy the same you would push to a repo

## Setting up heroku on your machine

This will install the Heroku CLI tools, which allow you to manage live apps, and test apps locally, from the command line.

### Installation

OS X: `brew install heroku`

Debian/'Buntu:

  ```bash
  sudo apt-get install software-properties-common # debian only
  $ sudo add-apt-repository "deb https://cli-assets.heroku.com/branches/stable/apt ./"
  $ curl -L https://cli-assets.heroku.com/apt/release.key | sudo apt-key add -
  $ sudo apt-get update
  $ sudo apt-get install heroku
  ```

### Setup

`heroku login # this works even if you have 2fa set up. It's kinda boss`

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
