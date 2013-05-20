.. image::  https://travis-ci.org/vdboor/django_polymorphic.png?branch=master
  :target: http://travis-ci.org/vdboor/django_polymorphic
  :alt: build-status

Polymorphic Models for Django
=============================

Django-polymorphic simplifies using inherited models in Django projects.
When a query is made at the base model, the inherited model classes are returned.

When we store models that inherit from a ``Project`` model...

>>> Project.objects.create(topic="Department Party")
>>> ArtProject.objects.create(topic="Painting with Tim", artist="T. Turner")
>>> ResearchProject.objects.create(topic="Swallow Aerodynamics", supervisor="Dr. Winter")

...and want to retrieve all our projects, the subclassed models are returned!

>>> Project.objects.all()
    [ <Project:         id 1, topic "Department Party">,
      <ArtProject:      id 2, topic "Painting with Tim", artist "T. Turner">,
      <ResearchProject: id 3, topic "Swallow Aerodynamics", supervisor "Dr. Winter"> ]

Using vanilla Django, we get the base class objects, which is rarely what we wanted:

>>> Project.objects.all()
    [ <Project: id 1, topic "Department Party">,
      <Project: id 2, topic "Painting with Tim">,
      <Project: id 3, topic "Swallow Aerodynamics"> ]

This also works when the polymorphic model is accessed via
ForeignKeys, ManyToManyFields or OneToOneFields.

Features
--------

* Full admin integation.
* ORM integration:

 * support for ForeignKey, ManyToManyField, OneToOneField descriptors.
 * Filtering/ordering of inherited models (``ArtProject___artist``).
 * Filtering model types: ``instance_of(...)`` and ``not_instance_of(...)``
 * Combining querysets of different models (``qs3 = qs1 | qs2``)
 * Support for custom user-defined managers.

* Uses the minumum amount of queries needed to fetch the inherited models.
* Disabling polymorphic behavior when needed.

While *django-polymorphic* makes subclassed models easy to use in Django,
we still encourage to use them with caution. Each subclassed model will require
Django to perform an ``INNER JOIN`` to fetch the model fields from the database.
While taking this in mind, there are valid reasons for using subclassed models.
That's what this library is designed for!

For more information, see the `documentation at Read the Docs <https://django-polymorphic.readthedocs.org/>`_.

License
=======

Django-polymorphic uses the same license as Django (BSD-like).