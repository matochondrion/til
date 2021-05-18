Using a PostgreSQL ENUM Data Type Instead of Integer
================================================================================

The Rails way of creating an `enum` is to use a column with an `integer`
data type and then associate the integers with values in the Model.

However with PostgreSQL you can create an `ENUM` data type with the enum
values predefined.

The advantage is that when looking at raw the data in the database, the values
describe what they represent. Eg, `"pdf"`, `"csv"`, `"xlsx"`; rather than `0`,
`1`, `2`. The disadvantage is it's not the typical Rails way of doing things
and could cause confusion.

Other Tips
--------------------------------------------------------------------------------

* Whether using a PostgreSQL `ENUM` or standard `integer` data type, define the
  enum values in the Model with a Hash:

  ```ruby
  enum file_type: { pdf: "pdf", xlsx: "xlsx", csv: "csv" }
  # OR
  enum file_type: { csv: 0, pdf: 1, xlsx: 2 }
  ```

* Use prefixes and suffixes if they help describe the enum values:

  ```ruby
  enum file_type: { pdf: "pdf", xlsx: "xlsx", csv: "csv" }, _suffix: true
  # OR
  enum file_type: { pdf: 0, csv: 1, xlsx: 2}, _suffix: true

  # instance.file_type_pdf?
  # > true
  ```


Further Reading
--------------------------------------------------------------------------------

* https://naturaily.com/blog/ruby-on-rails-enum
* https://til.hashrocket.com/posts/b492fb26ec-rails-enums-and-postgresql-enums
* https://medium.com/@diegocasmo/using-postgres-enum-type-in-rails-799db99117ff
