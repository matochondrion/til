WIP: Where to Put POROs in Rails Directory Structure
================================================================================

2021-05-09

Contents
--------------------------------------------------------------------------------

[TODO: link to sections]

* What Are POROs
* Why Use POROs
* Types of POROs
* Modules and Concerns vs Classes
* Namespacing syntax
* Simple Rules For PORO Directory Structure in Rails
* Testing POROs

What Are POROs
--------------------------------------------------------------------------------

Why Use POROs
--------------------------------------------------------------------------------

From the often referenced article, ["7 Patterns to Refactor Fat ActiveRecord
Models"](https://codeclimate.com/blog/7-ways-to-decompose-fat-activerecord-models/).
Re: Single Responsibility Principle (SRP):

> "Anything related to what a user does" is not a *single*
> responsibility...ActiveRecord classes handle persistence, associations and
> not much else.
>
> As you add more intrinsic complexity (read: features!) to your application,
> the goal is to spread it across a coordinated set of small, encapsulated
> objects (and, at a higher level, modules)...you'll end up with a set of simple
> objects with well-defined interfaces working together...

The author discourages use of "concerns" that are only mixed into one model -

> "Don't Extract Mixins From Fat Models"

She feels single-use concerns like this "make it harder to identify and
implement the decompositions and extractions necessary to clarify the model",
and encourages composition instead of inheritance for better domain model
clarity.

> To favor composition over inheritance is a design principle that gives the
> design higher flexibility. It is more natural to build business-domain classes
> out of components than trying to find commonality between them and creating a
> family tree.
> ref: https://en.wikipedia.org/wiki/Composition_over_inheritance

Types of POROs
--------------------------------------------------------------------------------

See ["7 Patterns to Refactor Fat ActiveRecord Models"](https://codeclimate.com/blog/7-ways-to-decompose-fat-activerecord-models/)
for more detailed definitions.

* **Value Objects**
  - Extract Value Objects: simple objects whose equality depends on their value
    rather than their identity. Usually immutable:
    - Ruby Standard Library examples: `Date`, `URI`, and `Pathname`
    - Rails app examples: `PhoneNumber`, `Money`, and `Rating`
  - Anything more than basic text fields and counters are candidates for Value
    Object extraction.
* **Service Objects**
  - Extract Service Objects: complex actions
  - Eg: pull out a `User#authenticate` method into a `Users::Authenticator`
* **Form Objects**
  - Extract Form Objects: when multiple ActiveRecord models might be updated by
    a single form submission.
  - "...far cleaner than using `accepts_nested_attributes_for`..."
    - Why?
* **View Objects**
  - Introduce View Objects: for logic needed specifically for view purposes
    without cluttering the global space with Rails view "helpers"
  - Also called "Presenter" or "View Models". The "Presenter" term can be
    confusing due to some using it for a different meaning. Jay Fields uses the
    term "Presenter" for an object similar to the "Form Object" above.
* **Query Objects**
  - Extract Query Objects: for complex SQL queries littering your ActiveRecord
    subclasses (either as scopes or class methods)
  - Responsible for returning a result set based on business rules
  - Eg, a `AbandonedTrialQuery` that could be used in a background worker to
    send emails
  - Don't test in isolation - test the object and database together to make
    sure the result contains the correct rows, order, etc.
* **Policy Objects**
  - Extract Policy Objects: Complex read operations
  - Like which users are considered active for analytical purposes
  - Similar to "Service Objects" but "Service Objects" are for write operations
    and "Policy Objects" are for read operations.
  - Also similar to "Query Objects" except "Query Objects" execute SQL to
    return a result while "Policy Objects" rely on domain models already loaded
    into memory.
* **Decorators**
  - Extract Decorators: to layer on functionality to existing operations
  - Service a similar purpose as callbacks
  - Useful when a callback only needs to run in certain circumstances or
    including it in the model would give the model too many responsibilities.
  - Eg, posting a comment on a blog post might trigger a post to someone's
    facebook wall, but that doesn't mean that logic should be hardwired into
    the `Comment` class
  - A sign that a callback has too many responsibilities are slow and brittle
    tests, or the need to stub out side effects in unrelated test cases
  - "Decorators" differ from "Service Objects" because they layer on
    responsibilities to to existing interfaces. Once decorated, collaborators
    treat the instance as if it were the original object type but with
    additional responsibilities

ref: https://codeclimate.com/blog/7-ways-to-decompose-fat-activerecord-models/

Modules and Concerns vs Classes
--------------------------------------------------------------------------------

Only extract modules and concerns if two or more classes share the same
functionality. Avoid extracting module specific 

Namespacing Syntax
--------------------------------------------------------------------------------

Use nested namespacing to avoid Ruby constant lookup issues in Rails.

```ruby
# Bad:
class User::Validate
# ...
end

# Good:
class User
  class Validate
  # ...
  end
end
```

Simple Rules For PORO Directory Structure in Rails
--------------------------------------------------------------------------------

There isn't an industry standard for where to put POROs. Taking the advice of
several articles, here are the rules and directory structure that make the
most sense to me:

* POROs that simplify Models can go in `app/models/concerns` if they are shared
  among more than one model, or in a namespaced folder related to the model
  that uses them, `app/models/users/valid.rb`.
  - ref: https://dev.to/sulmanweb/plain-old-ruby-objects-poros-in-rails-fat-models-3l7f
* POROs that can be shared among multiple applications or even made into gems
  go in `lib/`
* View/presenter POROs go in the Model's namespace
  - Needs details in TIL
  - ref: http://blog.vladimir-rybas.com/blog/2014/08/15/a-way-to-organize-poros-in-rails/

```
├── app
│   ├── decorators            # Decorators could have their own directory 
│   │                         # but may make more sense in model namespace
│   ├── forms                 # Forms are shared between models, could go
│   │                         # here or in models directory
│   ├── models
│   │   ├── concerns          # Shared concerns and modules
│   │   │   └── verifiable.rb # Shared concern
│   │   ├── forms             # Shared form objects could go here
│   │   │   └── combo_form.rb
│   │   ├── user.rb           # User ActiveRecord model
│   │   ├── users             # Users namespace
│   │   │   ├── valid.rb      # PORO for just the `User` model
│   │   │   ├── user_list.rb  # View/Presenter PORO
│   │   │   └── decorator.rb  # View/Presenter PORO
│   │   └── value_objects     # Shared Value Objects
│   │
│   ├── services              # Services could have their own directory 
│   │                         # but may make more sense in model namespace
│   ├── value_objects         # Value Objects could have their own directory 
│   │                         # but may make more sense in model namespace
│   └── queries               # Query Objects could have their own directory 
│                             # but may make more sense in model namespace
│
├── controllers               # Do NOT use POROs like this for controllers
│   │                         # Controllers only responsible for HTTP activities
│   │                         # View related POROs go in the Model's namespace
│   │                         # eg: app/models/users/user_list.rb
│   ├── dashboard_controller  # BAD
│   │   └── user_list_spec.rb # BAD
│   └── dashboard_controller_spec.rb
├── lib                       # Shared between multiple apps
├── specs
:   └── models
.       ├── users
        │   └── valid.rb      # Can test POROs invidvidually and...
        └── user.rb           # as when used in composition with other classes
```
 
Testing POROs
--------------------------------------------------------------------------------

Tests can be written in sub-folders for the individual PORO,
`specs/models/users/valid_spec.rb`

Many times the author [see
comments](http://blog.vladimir-rybas.com/blog/2014/08/15/a-way-to-organize-poros-in-rails/)
tests controllers through `request` specs instead of class specs to avoid
testing the implementation. Rather he just tests that the results from the
controller are correct - unless the logic is complex and needs to be tested
separately.
