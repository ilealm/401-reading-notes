[ HOME ](README.md)
# Read 27 - Django Models

> When designing your models it makes sense to have separate models for every "object".

- Once we've decided on our models and field, we need to think about the relationships. 
- Django allows you to define relationships that are:
  - one to one (OneToOneField), 
  - one to many (ForeignKey) and
  - many to many (ManyToManyField).

### Model Definition
- Models are usually defined in an application's models.py file.
- They are implemented as subclasses of django.db.models.Model, and can include fields, methods and metadata. 

```
from django.db import models

class MyModelName(models.Model):
    """A typical class defining a model, derived from the Model class."""

    # Fields
    my_field_name = models.CharField(max_length=20, help_text='Enter field documentation')
    ...

    # Metadata
    class Meta: 
        ordering = ['-my_field_name']

    # Methods
    def get_absolute_url(self):
        """Returns the url to access a particular instance of MyModelName."""
        return reverse('model-detail-view', args=[str(self.id)])
    
    def __str__(self):
        """String for representing the MyModelName object (in Admin site etc.)."""
        return self.my_field_name
```

### Fields
-  Model can have an arbitrary number of fields, of any type — each one represents a column of data that we want to store in one of our database tables.

```
my_field_name = models.CharField(max_length=20, help_text='Enter field documentation')
```

#### Common field arguments

**help_text:** Provides a text label for HTML forms (e.g. in the admin site), as described above.
verbose_name: A human-readable name for the field used in field labels. If not specified, Django will infer the default verbose name from the field name.

**default:** The default value for the field. This can be a value or a callable object, in which case the object will be called every time a new record is created.

**null:** If True, Django will store blank values as NULL in the database for fields where this is appropriate (a CharField will instead store an empty string). The default is False.

**blank:** If True, the field is allowed to be blank in your forms. The default is False, which means that Django's form validation will force you to enter a value. This is often used with null=True , because if you're going to allow blank values, you also want the database to be able to represent them appropriately.

**choices:** A group of choices for this field. If this is provided, the default corresponding form widget will be a select box with these choices instead of the standard text field.

**primary_key:** If True, sets the current field as the primary key for the model (A primary key is a special database column designated to uniquely identify all the different table records). If no field is specified as the primary key then Django will automatically add a field for this purpose.

## Creating and modifying records

- To create a record you can define an instance of the model and then call save().

```
# Create a new record using the model's constructor.
record = MyModelName(my_field_name="Instance #1")

# Save the object into the database.
record.save()

# Access model field values using Python attributes.
print(record.id) # should return 1 for the first record. 
print(record.my_field_name) # should print 'Instance #1'

# Change record by modifying the fields, then calling save().
record.my_field_name = "New Instance Name"
record.save()

```

## Searching for records
- You can search for records that match certain criteria using the model's objects attribute
- We can get all records for a model as a QuerySet, using objects.all(). The QuerySet is an iterable object, meaning that it contains a number of objects that we can iterate/loop through.
- filter() method allows us to filter the returned QuerySet to match a specified text or numeric field against particular criteria.

```
all_books = Book.objects.all()

wild_books = Book.objects.filter(title__contains='wild')
number_wild_books = wild_books.count()

```

# Django admin site

The Django admin application can use your models to automatically build a site area that you can use to create, view, update, and delete records. This can save you a lot of time during development, making it very easy to test your models and get a feel for whether you have the right data. The admin application can also be useful for managing data in production, depending on the type of website. The Django project recommends it only for internal data management

### Registering models 

In admin.py in the catalog application (/locallibrary/catalog/admin.py). It currently looks like this — note that it already imports django.contrib.admin:

```
from django.contrib import admin
```

### Creating a superuser

In order to log into the admin site, we need a user account with Staff status enabled. In order to view and create records we also need this user to have permissions to manage all our objects.  You can create a "superuser" account that has full access to the site and all needed permissions using manage.py.

```
python3 manage.py createsuperuser
python3 manage.py runserver
```
