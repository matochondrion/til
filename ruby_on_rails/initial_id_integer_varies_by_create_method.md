THE INITIAL ID FOR A MODEL DEPENDS ON THE WAY IT'S CREATED
================================================================================

In an RSpec suite, the first record of a Modal will have an `id` of `1`.
However if other records of the Model have been created in previous tests, the
first record of the modal can have an id of `2` instead. Even if the `id_seq`
has been reset to the initial value of `1`.

If no records have been created in the test suite yet, the `id_seq` from the db
will be `1` , and the first record created will also have an id of 1. 

If previous records have been created in other tests, but there are `0` records
in the current test and the `id_seq` has the same initial value of  `1` , the
next record can have an id of 2 .

I've tested this on in Rails 5.2.4.4 using a PostgreSQL database.
