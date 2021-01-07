NAMESPACED CLASSES IN RAILS
================================================================================


CLASSES CAN'T BE AUTOMATICALLY FOUND IN SUB-DIRECTORIES
--------------------------------------------------------------------------------

In large rails projects it makes sense to move related classes for Models,
Controllers, Views, etc into subdirectories.

Once moved, the classes are no longer automatically found by Rail's autoloader.


TL;DR
--------------------------------------------------------------------------------

Place the classes in a namespace...or in other words, a `module`, where the
module's name is the same as the sub-directory's name.


SOLUTIONS
--------------------------------------------------------------------------------


1. Configure the autoloader to look in the new directories
  - https://edgeguides.rubyonrails.org/configuring.html

2. Place the classes in a namespace...or in other words, a `module`, where the
   module's name is the same as the sub-directory's name.


IN RUBY THERE ARE TWO PAYS TO DEFINE A CLASS INSIDE A MODULE
--------------------------------------------------------------------------------

The "standard" way is to nest the class inside of the module:

```ruby
module MyModule
  class MyClass
    # ....
  end
end
```

The "shortcut" way using `::` notation:

```ruby
class MyModule::MyClass
    # ....
end
```

They are similar but the lookup behavior for constants is different. Using the
first method you do not need to previs constant names with the module's
namespace qualifier. Ie, the code inside `MyClass` does not need to add th
`MyModule::`` qualifier.

Using the "shortcut" method, those references will require the `MyModule::`
prefix because Ruby will not look inside `MyModule` for those names.

Also in plain Ruby, the module prefix will need to already have been defined
before you use it. Rails blurs the line a bit because sometimes the autoloader
will define it for you. But basically, using the non-shortcut method is
simplest.



ENCLOSINBG MODUELS ARE NOT CONSIDERED WHEN INERERING TABLE NAMES
--------------------------------------------------------------------------------

Read more about this at:

http://apidock.com/rails/ActiveRecord/Base/table_name/class


SOURCES
--------------------------------------------------------------------------------

https://randycoulman.com/blog/2014/12/09/namespaced-classes-in-rails/
