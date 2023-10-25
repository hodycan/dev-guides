# fields reference.md
TODO learn ForeignKey.on_delete values
TODO learn ForeignKey.related_name

https://docs.djangoproject.com/en/4.2/ref/models/fields/


## common fields

#### CharField
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#charfield)
for small- to large-sized strings

#### TextField
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#charfield)
for large amounts of text

#### DateTimeField
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#datefield)

DateField.auto_now
: Automatically set the field to now every time the object is saved

DateField.auto_now_add
: Automatically set the field to now when the object is first created

#### DecimalField
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#decimalfield)
DecimalField.max_digits
: The maximum number of digits allowed in the number. Note that this number must be greater than or equal to decimal_places.

DecimalField.decimal_places
: The number of decimal places to store with the number.

#### DurationField
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#durationfield)
A field for storing periods of time - modeled in Python by timedelta.

#### EmailField
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#emailfield)

#### IntegerField
: safe for -2147483648 to 2147483647

#### BooleanField
: True or False. default None when Field.default isn't defined.



## relationship fields
[docs](https://docs.djangoproject.com/en/4.2/ref/models/fields/#module-django.db.models.fields.related)

#### ForeignKey
many to one relationship

Behind the scenes, Django appends "_id" to the field name to create its database column name. In the docs example, the database table for the Car model will have a manufacturer_id column.

ForeignKey.on_delete
: What to do when referenced object is deleted
- CASCADE - also deletes the object containing the foreign key
- PROTECT - Prevent the delete the referenced object
- RESTRICT - ?? Only allows if it also references another object that is also being deleted in the same operation. e.g. Artist, Album, Song
- SET_DEFAULT - Set the ForeignKey to its default value; a default for the ForeignKey must be set.

ForeignKey.related_name
: The name to use for the relation from the related object back to this one


#### ManyToManyField
behind the scenes, django creates intermediary join table

ManyToManyField.symmetrical
: only for relationship to class' self. e.g. Person class - if you are my friend then I am your friend.

#### OneToOneField
Similar to ForeignKey with unique=True, but the reverse side of the relation will directly return a single object



## other fields
AutoField
BigAutoField
BigIntegerField
BinaryField
DateField
FileField
FileField and FieldFile
FilePathField
FloatField
GenericIPAddressField
ImageField
JSONField
PositiveBigIntegerField
PositiveIntegerField
PositiveSmallIntegerField
SlugField
SmallAutoField
SmallIntegerField
TimeField
URLField
UUIDField
Relationship fields
Database Representation
Arguments
Database Representation
Arguments



## default values

instantiate models with parameter `default`.

mutable objects MUST be wrapped in a callable. e.g. a default dict for JSONField

```
def contact_default():
    return {"email": "to1@example.com"}

contact_info = JSONField("ContactInfo", default=contact_default)
```

For foreign keys, defaults should value of the field they reference (by default set to pk), instead of model instances.
