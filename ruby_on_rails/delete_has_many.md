DELETE HAS_MANY ASSOCIATION WITHOUT DESTROYING THE RECORD
================================================================================

If you want to delete an assocation from a `has_many` collection, without
destroying the associated record, possibly because it's still being referenced
by other records, use `#delete`. 

Eg: `list_version.intervals.delete(list_version)` 

https://guides.rubyonrails.org/v3.2.2/association_basics.html

4.4.1.4 collection.delete(object, …)
The collection.delete method removes one or more objects from the collection by
deleting records in the join table. This does not destroy the objects.

```
@part.assemblies.delete(@assembly1)
```
