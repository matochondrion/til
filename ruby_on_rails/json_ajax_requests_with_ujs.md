JSON Requests With AJAX in Rails 5.2
================================================================================

2021-06-28 Mon

Contents
--------------------------------------------------------------------------------

* Why using Rails friendly tools is easier and alternatives
* jQuery-ujs vs Rails-ujs Pros, Cons, and Complications
* Displaying the Flash message by reloading with page with JavaScript

TL;DR: 
--------------------------------------------------------------------------------

* Rather than sending JSON as a standard `POST` or `PATCH` request it's
  easier to use JavaScript AJAX tools like `jquery.ajax`, and then send an
  HTML or JavaScript Controller respond - depending on the situation.
* Rails has two built in "Unobtrusive JavaScript" tools for making AJAX
  requests, with automated Rails CSRF compatibility:
  "jQuery-ujs" and "Rails-ujs"
  - https://guides.rubyonrails.org/security.html
* While Rails-ujs is newer with more features it's currently not documented as
  well as jQuery-ujs, and has some quirks. Making jQuery-ujs the preferred
  method for now, at least in Rails 5.2
* Example JSON PATCH request:
  ```javascript
$.ajax({
  type: "PATCH", 
  url: "/groups/2/access_roles/permissions_template_permissions/2",
  data: {"boo": "far"},
  success: function(data, textStatus, jqXHR){},
  error: function(jqXHR, textStatus, errorThrown){}
})
  ```


Why using Rails friendly tools is easier and alternatives
--------------------------------------------------------------------------------

* Use AJAX tools even if we're not fully implementing AJAX since they make CSRF
  more convenient
  - https://guides.rubyonrails.org/working_with_javascript_in_rails.html#cross-site-request-forgery-csrf-token-in-ajax
* Further information on Rails CSRF

jQuery-ujs vs Rails-ujs Pros, Cons, and Complications
--------------------------------------------------------------------------------

* Why Rails is replacing jQuery-ujs with Rails-ujs
  - Stimulus
* Problems with using jQuery-ujs
  - Slowly becoming outdated
* Problems with using Rails-ujs
  - Will need to update how responses are handled to be compatible with new
    format
  - Sending JSON requests with `Rails.ajax` doesn't to have issues with the
   `data` argument...it only accepts a string and the string and the entire
   string become a key with no value - although `$.ajax()` still seems to work
   as before even when using `rails-ujx` instead of `jquery_ujx`
  - https://www.bitesite.ca/blog/ruby-on-rails-6-with-jquery-ujs
  - https://learnetto.com/blog/rails-ajax
* Related resources:
  - https://api.jquery.com/jquery.ajax/
  - https://dev.to/nejremeslnici/migrating-from-jquery-ujs-to-rails-ujs-k9m
  - https://jonathanpike.net/2016/02/diving-into-jquery-ujs
  - https://github.com/rails/jquery-ujs/wiki
  - https://www.cloudbees.com/blog/unobtrusive-javascript-via-ajax-rails
  - https://www.w3schools.com/jquery/ajax_post.asp
  - https://edgeguides.rubyonrails.org/working_with_javascript_in_rails.html

Displaying the Flash message by reloading with page with JavaScript
--------------------------------------------------------------------------------

  - https://jonathanpike.net/2016/02/responding-to-ajax
  - https://jonathanpike.net/2016/02/responding-to-ajax
