proof of concept for breaky breaky
==================================

Based on `a conversation`_ (started by `revsys, here`_) about
dynamic ``{% extends %}`` in DTL, I'm now doing my due-diligence because
apparently I might be wrong, having not checked for a few years.

`I don't think I am`_, though.

Given the template ``template_1.html`` in the `django CMS installation docs`_,
changing the ``{% extends "base.html" %}`` to anything which might resolve to
a variable or filter prevents any placeholders from being discovered, in either
the template itself, or the parent it would extend. This is understandable,
because the parser/renderer may not have enough context to resolve the actual
parent template, but to say its without problems may be incorrect.

I think the minimal test case is::

  {% extends "base.html"|default:"base.html" %}

Try it out:

- clone this project.
- pip install django-cms
- python manage.py migrate
- python manage.py createsuperuser
- python manage.py runserver
- figure out how to add pages and stuff. I've not used django CMS since 2.4,
  so its all a bit confusing. Muddle through until you've got ``Template One``
  and ``Template Two`` each bound to a page.
- The one using ``Template Two`` probably lacks any placeholders, which for me
  also involved losing the Structure/Content button group.

.. _a conversation: https://twitter.com/yakkys/status/762917703275384832
.. _revsys, here: https://twitter.com/revsys/status/762751628571213829
.. _I don't think I am: https://github.com/divio/django-cms/search?q=is_variable_extend_node
.. _django CMS installation docs: http://docs.django-cms.org/en/release-3.3.x/how_to/install.html#creating-templates
