=====
BIB
=====


Bib is a simple Django app to log all request made to the server and responses sent from the server.

<img src="https://raw.githubusercontent.com/fuzz-productions/bib/master/bib/static/img/fuzzbib.png" width=150px/>

Quick start to Implement Existing Project
-----------

1. Pip install:

   ```
   $ pip install git://github.com/fuzz-productions/bib.git#egg=Bib
   ```

2. Add to requirements.txt:

    ```
    django-bootstrap3==6.2.2
    -e git://github.com/fuzz-productions/bib.git#egg=Bib
    ```

3. Add "bootstrap3" and "bib" to your INSTALLED_APPS setting like this:

    ```
    INSTALLED_APPS = (
        ...
        'bootstrap3',
        'bib',
    )
    ```

4. Add bib middleware to your settings:

    ```
    MIDDLEWARE_CLASSES = (
        ...
        'bib.middleware.DumpRequestToLogMiddleware',
    )
    ```


5. Include the bib URLconf in your project urls.py like this::

    ```python
    url(r'^bib/', include('bib.urls')),
    ```

6. Run `python manage.py migrate` to create the bib models.

7. In your `settings.py`, set the API_VERSION equal to your the current version and make sure all your URLS are using that reference to the API_VERSION. For example, if you're on 1.0, in `settings.py`:

    ```python
    API_VERSION = 'v1.0'
    ```

   Then in your `urls.py`

   ```
   url(r"^%s/articles/(?P<article_id>.+)/?" % settings.API_VERSION, views.article)
   ```

   Or if you're using Django Rest Framework's router:

   ```
   router.register(r"%s/articles/?" % settings.API_VERSION, views.ArticleViewSet)
   ```

8. Run bib migrations: `./manage.py migrate`

9. After hitting the API a few times, visit http://localhost:8000/bib/ to see all requests and responses.

**Note:** In settings, make sure that `debug=True`. Be sure to turn debug off in production or else your database will be bloated with Bib objects.

TO DOs
-----------

* Set up management command to remove Bib objects based on date.
* Support for passing in a device ID to allow for a list view specific to one device
* Dashboard breakdown by status codes
* Ability to query for specific events
* Events collated by session, user, request
* Fixed links to specific logs
* Accordian UI doesn't deal with back very well maybe scrap the whole concept
* Render request headers
* Finish Test App test suite
* Make sure pep8 compliant
