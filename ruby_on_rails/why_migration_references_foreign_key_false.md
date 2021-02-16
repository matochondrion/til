WHY DO MIGRATION REFERENCE COLUMN'S FOREIGN KEY DEFAULT TO FALSE?
================================================================================

NOTE: These are mostly quotes from a reddit discussion:

To add a DB column that references another table, you use references (or
`belongs_to`) in migrations. For instance, the following example is given in the
official guide on Active Record migrations:


```
class AddUserRefToProducts < ActiveRecord::Migration[5.0]
  def change
    add_reference :products, :user, foreign_key: true
  end
end
```

The API documentation clarifies that the `:foreign_key` option sets a foreign key
constraint, presumably at the database level.

---

It's worth mentioning that Rails implements OO polymorphism using Single Table
Inheritance. This is done by adding two columns (object type, object ID) to a
table. When querying a related object, ActiveRecord finds an associated record
using the `type` to identify the table to join, and `id` to find the record.

**This prevents an FK constraint, since the constraint can't refer to multiple
tables.**

---

DHH and by extension, the Rails community, had decided that referential
integrity is an application-layer concern, and not a database concern. See this
2011 post:
`https://stackoverflow.com/questions/3438731/referential-integrity-in-rails`

It didn't take long for people to realize that callbacks at the application
level can fail in non-transactional ways (`dependent: :destroy`, for example is
just a `before_destroy` callback, which can be halted for a number of reasons).

tl;dr - people thought you could sprinkle on the referential integrity, but you
can't.


---

Source: `https://www.reddit.com/r/rails/comments/7swwx4/in_migrations_why_does_references_or_belongs_to/?utm_source=share&utm_medium=ios_app&utm_name=iossmf`
