Static Attributes in Factory Bot Are Deprecated
===============================================================================

Two Ways to Define Attributes
-------------------------------------------------------------------------------

#### Dynamic:
```ruby
factory :robot do
  name { "Ralph" }
end
```

#### Static:
```ruby
factory :robot do
  name "Ralph"
end
```

With *dynamic*, every time you build a new `:robot` instance, you will get a new
"Ralph" string for the `name`.

With *static*, you will always get the same string object in memory.  If the
static string is mutated during a test, it will be mutated for all tests, which
causes *problems*.

Types of Problems
-------------------------------------------------------------------------------
* If an object is changed once, it will be changed for all instances of that
  factory.
* Time attributes, eg: `Time.now` can be particularly confusing.
* Using persistent _records_ with _static_ attributes can be confusing as well
  since every instance will be associated with the same persistent record.

```ruby
factory :robot do
  friend Person.create!(name: "Daniel")
end
```

***Static attributes in factory bot are deprecated***

Source
-------------------------------------------------------------------------------

https://thoughtbot.com/blog/deprecating-static-attributes-in-factory_bot-4-11
