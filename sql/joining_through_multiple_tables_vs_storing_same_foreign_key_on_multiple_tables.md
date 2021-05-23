Joining Through Multiple Tables vs Storing Same Foreign Key on Multiple Tables
================================================================================

Question: Is it better to join through a table that is several relations away,
or to store the foreign key of that table directly on the referencing table?

Eg. We have tables:

```sql
--- Table: family_details
family_details.id
family_details.name

--- Table: family_members
family_members.id
family_members.family_detail_id

--- Table: family_pets
family_pets.id
family_pets.family_member_id

--- Is this foreign-key a good or bad idea?
family_pets.family_detail_id
```

If we want to retrieve the family `name` of a `family_pets` record, we could
create a multiple table join from the `family_pets` to `family_members` and
then to `family_details`. Or we could add a `family_detail_id` on the
`family_pets` table to join the `family_pets` table directly to the
`family_details` table.

However, If the grandchild table is not meaningfully associated with the
grandparent table, it's preferable to join through multiple tables rather than
circumvent the relationship path by associating the tables directly.

In this case, do not add a `family_pets.family_detail_id` foreign key. The
`family_pet` belongs to a `family_member` and not to `family_details`.  Adding
`family_pets.family_detail_id` would be a form of de-normalized data and should
be avoided unless there is a performance issue. If performance becomes a
problem it's justifiable to consider associating the grandchild table with the
grandparent table directly.

> The standard is not to store unnecessarily redundant information, including
> redundant Foreign Key information that could be derived through
> relations/joins.
> 
> In practice this means, storing only the direct relationships' FKeys, and not
> secondary or implicit FKey info. For performance reasons you may at some point
> decide to try "short-circuiting" a relation, but technically that's a form of
> de-normalization. You can do it, but you only should do it when the need is
> apparent, in other words, proper normalization should always be the default,
> anything else needs to significantly justify itself.}
> 
> source: https://stackoverflow.com/a/18475178

### Sources

* https://blog.codinghorror.com/maybe-normalizing-isnt-normal/
* https://stackoverflow.com/questions/18474481/sql-and-storing-foreign-keys-on-multiple-tables-vs-joining-through-tables-for-qu
* https://www.sqlservercentral.com/forums/topic/would-you-store-foreign-key-from-grandparent-tables-why-or-why-not 


