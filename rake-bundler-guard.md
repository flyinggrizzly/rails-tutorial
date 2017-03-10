# Rake vs Bundler vs Guard

## Bundler

Bundler is a configurator for Ruby projects, and allows you to specify gems, and versions, to be used in a project.

It has the ability to keep separate gem versions installed, and run your project with those specific versions. It's kinda like `rbenv`, but for your gems. Or better yet, a shopping list where you've said not just 'get bacon', but 'get maple-smoked streaky bacon'--you've specified which version of bacon you need. Just declare `gem 'rails', '[version number]'` in your `Gemfile` and you've got your shopping list set up.

Bundler's ability to manage multiple different versions of gems/etc means that you can end up with conflicts. Bundler fixes this for you though, by maintaing a `Gemfile.lock`.  If your `Gemfile` is your shopping list, `Gemfile.lock` is your receipt that tells you exactly what you ended up with.

You can run commands against the things you have locally: prefix your commands with `bundle exec` and bundler will run the commands with the specified gems/dependencies instead of your system's default versions/dependencies.

Despite the `bundle exec` task starter, bundler is not a taskrunner. It just sets the run-environment for anything else you do (which is where I was getting confused, because you're kinda using it to run tasks). It plays very nice with taskrunners.

## Rake

Named for `make`, Rake does the core pieces of work while you're developing. It should perform discrete tasks.

The big ones are

- `rake test # runs your tests, assuming you've configured them for minitest or Rspec`
- `rake db:[create | migrate] # for setting up databases in Rails/etc`
- anything else you can imagine

The important thing is that these should be single functions--you don't want them running a loop (that's what Guard is for).

If you've used Bundler to set up your environment, use rake with `bundle exec rake [test | db:migrate | whatever-your-command-is]`


## Guard

**[Github](https://github.com/guard/guard)**

Guard is a taskrunner for Ruby, focused on automating commands that would regularly need to be rerun/relaunched after a code change. It has a gigantor [wiki listing](https://github.com/guard/guard/wiki/Guard-Plugins) of plugins. It plays nice with `bundler`,  and kinda expects it to be used to set up `guard`.

It watches your filesystem for changes as triggers to run other dev tasks (like firing off `[bundle exec] rake test`, for example.

In which case, once you'd created the `Rakefile`, you would create a `Guardfile` to tell Guard what to do. Then you'd define a Guard task in it to watch a specific set of files, and if they changed, Guard would fire off the rake task. You'd start Guard with `[bundle exec] guard rake`, which would then run `[bundle exec] rake test` when you changed, say, one of the test files.

## Putting it all together
