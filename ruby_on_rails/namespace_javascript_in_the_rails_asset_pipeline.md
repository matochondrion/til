Namespacing JavaScript in the Ruby on Rails Asset Pipeline
================================================================================

When including JavaScript in Ruby on Rails, a typical workflow involves placing
a JavaScript file in the `assets/javascripts/` directory. The file is processed
by Sprockets as part of the Asset Pipeline, and then included directly on every
page of the app via the "layout" view template.

So all variables and functions initialized in the top level of these JavaScript
files are global to every page. Any code execution will be run on all pages as
well - regardless of if it is needed or not. Often this results in code called
on pages where it doesn't apply. For example, attempting to perform operations
on HTML elements that don't exist.

I'm not sure if there are noticeable performance consequences, and the code
usually fails silently without side effects. However reducing the clutter in
the global namespace reduces the chances of code collisions and difficult to
diagnose bugs.

There are numerous namespacing methods for JavaScript. A pattern I currently
like is an Immediately Invoked Function Expression (IIFE) in the form of a
"Revealing Module Pattern".

With this method we wrap the functionality in an IIFE. The IIFE returns an
object that includes, among other values, an initializing function. This
returned object is assigned to a variable in the global namespace, and
effectively creates it's own namespace for the values it contains. 

```javascript
var myNamespace = (function () {
  // definitions...
  return { init: int, mVal: myVal}
})();
```

The initializing function can then be called from the namespaced variable only
on the pages where we need it.

```html
<script>
  document.addEventListener("DOMContentLoaded", function(event) {
      myNamespace.init();
    });
</script>
```

Detailed Examples
--------------------------------------------------------------------------------

### Code Defined in `assets/javascripts/`

```javascript
var myNamespace = (function () {
    // Defined within the local scope
    var privateMethod1 = function () { /* ... */ },
        privateMethod2 = function () { /* ... */ }
    var privateProperty1 = "foobar";
    var myContainer;

    // Or
    function assignElements() {
      myContainer = $("[data-some-container]");
    }
    function init() {
      // Call the setup functions here.
      // An ideal place for variable assignment of elements when we want to
      // wait for the page to finish loading before performing the assignments.
      assignElements();
    }

    return {
        // the object literal returned here can have as many 
        // nested depths as we wish,
        // this way of doing things works best for smaller, 
        // limited-scope applications in my personal opinion
        publicMethod1: privateMethod1,

        // nested namespace with public properties
        properties:{
            publicProperty1: privateProperty1
        },

        // another tested namespace
        utils:{
            publicMethod2: privateMethod2
        },
        // the initializing method
        init: init
        // ...
    }
})();
```

### Call the Code on Pages Where Needed: `views/my_model/my_template.html.erb`

```html
<script>
  document.addEventListener("DOMContentLoaded", function(event) {
      myNamespace.init();
    });
</script>
```


Additional Information
--------------------------------------------------------------------------------

* O'Reilly: "Namespacing Fundamentals"
  - Source: https://www.oreilly.com/library/view/learning-javascript-design/9781449334840/ch13s15.html
