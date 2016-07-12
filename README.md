# Likeno

[![Build Status](https://travis-ci.org/mezuro/likeno.png?branch=master)](https://travis-ci.org/mezuro/likeno)
[![Code Climate](https://codeclimate.com/github/mezuro/likeno.png)](https://codeclimate.com/github/mezuro/likeno)
[![Test Coverage](https://codeclimate.com/github/mezuro/likeno/badges/coverage.svg)](https://codeclimate.com/github/mezuro/likeno)

Likeno is the Mezuro Team's take on RESTful APIs integration with Rails applications. It tries to mimic ActiveRecord's API.

Basically back in 2013, the Mezuro team was getting started with micro services. In order to keep the code clean and following Rails' standards we looked at [active_resource](https://github.com/rails/activeresource) and it proved to not fulfill our requirements about nested objects and [her](https://github.com/remiprev/her) which also has failed the same way. With those frustations in mind we started coding all the CRUD requests using `faraday_middleware` but still giving flexibility for custom requests whenever necessary. Likeno is the final product of this.


It's name come from the fact that by itself Likeno has no purpose at all. It only lives associated to another softwares, providing them with the necessary methods for RESTful APIs. So we can say that Likeno has a symbiosis relation with other applications. This leads us to lichens which are a good symbiosis example. As the Mezuro project has lots of Esperanto words, we finally get to Likeno: is the Esperanto word for lichen.

## Contributing

Please, have a look the wiki pages about development workflow and code standards:

* https://github.com/mezuro/mezuro/wiki/Development-workflow
* https://github.com/mezuro/mezuro/wiki/Standards

## Installation

Add this line to your application's Gemfile:

    gem 'likeno'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install likeno

### Important note about Ruby versions older than 2.2.2

Likeno depends on [activesupport](https://github.com/rails/activesupport) to work.
AS version 5 dropped support for Ruby versions older than 2.2.2. Unfortunately,
RubyGems does not take that into account while selecting a Gem version to be installed.
It will attempt to install version 5 and fail in many cases.

If your project is not using Rails (which will already lock the AS version to it's own),
you need to add the following snippet to your Gemfile if you want to keep support
for those old Ruby versions.

```ruby
# Active Support 5 drops Ruby < 2.2.2 support. We still want to support it, so
# manually add a maximum version bound for incompatible Ruby versions.
if Gem::Version.new(RUBY_VERSION) < Gem::Version.new('2.2.2')
    gem 'activesupport', '< 5'
end
```

If you are installing Likeno manually as outlined earlier, you must install a version
of f AS compatible with your Ruby installation first, by running the following command:

    gem install activesupport -v '< 5'

## Usage

Likeno provides default actions for communicating with Rails applications following the scaffold routes. All communication is assumed to use JSON. Specially have a look at the methods from `Likeno::Entity`:

* C `create`
* R `find` (retrieve)
* U `update`
* D `destroy`

Additionally we provide other useful methods:

* `save` and `save!`
* `to_hash`
* `==`


We hope to make available soon a full documentation on RDoc that will make easier to understand all this.

A good example on how to get everything from Likeno should be KalibroClient (https://github.com/mezuro/kalibro_client). So, have a look there for some examples.

### Custom Requests

Likeno allows the creation of custom requests. For example:

```ruby
class MyClass
  def my_custom_request(...)
    action = 'my_action'
    params = {}
    method = :get
    prefix = ''
    Likeno::Entity.request(action, params, method, prefix) # The path used will be '/my_classes/my_action'
  end
end
```

It returns a `hash` with the response body.

## Versioning

Kolekti follows the [semantic versioning](http://semver.org/) policy.
