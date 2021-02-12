BEST PRACTICE FOR WHEN AND WHERE TO CREATE ASSOCIATED RECORDS
================================================================================

They can be created in multiple places including. Say you have a `Group` and
that group may or may not have a `location`. But if it does have a `location`
then is also needs to have a `kiosk_mode`:

* A) Create right away when you create the first record. Eg, if you have a
  `group` and then create an associated `location`, the `Location` model could
  have a callback that creates a `kiosk_mode` record for the `group` after the
  `locaiton` has been created.

  This could also be done inside a transaction statement that creates both the
  `group.location` and `group.kiosk_mode` at the same time.
 
* B) Or instead you could create the `kiosk_mode` when it's needed using a
  `find_or_create_by` during the Controller action that requests the
  `kiosk_mode` belonging to the `group`, thus creating it only as-needed. The
  `kiosk_mode` will exist by the time the page is rendered if it didn't at the
  time the page was requested.


Strategy A keeps the object creation closer to the models where they belong
logically and it's easier to test.

Strategy A could create unnecessary objects that aren't needed while B only
creates objects if they're definitely going to be used. However it's a little
strange in terms of HTTP verbs. Eg, if someone makes a `GET` request that kicks
off the creation of the object, the object creation doesn't logically match the
request. Although, `GET` isn't really referring to the `kiosk_mode`, it's likely
referring to the `group` object and the `kiosk_mode` creation is just a
secondary result of that `GET` request.

Either method could be valid depending on the needs of the app. For further
exploration of when option A or B might be more appropriate see this helpful
ThoughtBot article:

https://thoughtbot.com/blog/when-to-create


  
