Best Practices
=============

The following are locally agreed upon best practices. As often as possible,
these will inherit from practices within the larger open source development
community at large. These best practices may, and likely will, change in the
future. But that change will be incorporated via group consensus and documented
here.

* [Documentation](documentation.md)
* [Project README's](project_readme.md)
* [Deployment](deployment.md)


General
-------

* These are not to be blindly followed; strive to understand these and ask
  when in doubt.
* Don't duplicate the functionality of a built-in library.
* Don't swallow exceptions or "fail silently." Exceptions should be logged or
  passed up the stack.
* Don't write code that guesses at future functionality.
* Exceptions should be exceptional.
* [Keep the code simple].

[Keep the code simple]: http://www.readability.com/~/ko2aqda2

Object-Oriented Design
----------------------

* Avoid global variables.
* Avoid long parameter lists.
* Limit collaborators of an object (entities an object depends on).
* Limit an object's dependencies (entities that depend on an object).
* Prefer composition over inheritance.
* Prefer small methods. Between one and ten lines is best.
* Prefer small classes with a single, well-defined responsibility. When a
  class exceeds 100 lines, it may be doing too many things.
* [Tell, don't ask].

[Tell, don't ask]: http://robots.thoughtbot.com/post/27572137956/tell-dont-ask

Ruby
----

* Follow the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide)
* Follow the [RSpec Guidelines with Ruby](http://betterspecs.org/)
* Use rbenv and include a .ruby-version file to specify the Ruby version for the project
* Avoid optional parameters. Does the method do too much?
* Avoid monkey-patching.
* Always use generators such as `rails new` and `rails generate migration
  XYZ` rather than managing tasks by hand.
* Generate any additional [Bundler binstubs] needed for the project that are not
  supplied by rails generators and add them to version control.
* Prefer `private` when indicating scope. Use `protected` only with comparison
  methods like `def ==(other)`, `def <(other)`, and `def >(other)`.

[Bundler binstubs]: https://github.com/sstephenson/rbenv/wiki/Understanding-binstubs

Bundler
-------
* Use a [pessimistic version] in the `Gemfile` for gems that follow semantic
  versioning, such as `rspec`, `factory_girl`, and `capybara`.
* Use [versionless] `Gemfile` declarations for gems that are safe to update
  often, such as pg, thin, and debugger.
* Use an [exact version] in the `Gemfile` for fragile gems, such as Rails.

[exact version]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
[pessimistic version]:
http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
[versionless]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
