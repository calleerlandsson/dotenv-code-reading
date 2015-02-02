# `dotenv`

Shim to load environment variables from `.env` into `ENV` in development.

## Usage

`.env`:

    SECRET_KEY=DONTTELLANYONE

`app.rb`:

    require "dotenv"
    Dotenv.load
    ENV["SECRET_KEY"] #=> "DONTTELLANYONE"

## Entry points

`dotenv` has multiple entry points designed for specific use cases.

### Rails app

    gem "dotenv-rails", groups: [:development, :test]

### Rake task

    require "dotenv/tasks"

    task mytask: :dotenv do
    end

### The command line

    dotenv PROGRAM

### Ruby

    require "dotenv"
    Dotenv.load

We're going to focus on the standard Ruby entry point.

# Points of interest

## Dotenv (`lib/dotenv.rb`)

- L42-46: Could be replaced with a call to `inject`.
- L44: Depends on the caller supplying a block returning a Hash-like object.
- L11: Flawed way of handling non-existent files.

## Dotenv::Environment (`lib/dotenv/environment.rb`)

- L10: Overriding kernel method `load`.
- L7: Mutation in constructor.

## Dotenv (`lib/dotenv.rb`)

- L13: Instrumentation.

## `lib/dotenv/rails.rb`

- L3: Using `ActiveSupport::Notifications`.

## Dotenv::Environment (`lib/dotenv/environment.rb`)

- L18: Actually setting the keys in `ENV`.

## Dotenv (`lib/dotenv.rb`)

- L13: Actually not instrumenting the loading, but rather the application.

# Related links

- https://github.com/bkeepers/dotenv/
- http://www.ruby-doc.org/core-2.2.0/Kernel.html#method-i-load
- http://api.rubyonrails.org/classes/ActiveSupport/Notifications.html
