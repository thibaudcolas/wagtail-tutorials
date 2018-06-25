# Django Girls extension: Getting started with Wagtail

> **Info** This tutorial assumes you have already been through the main [Django Girls tutorial](https://tutorial.djangogirls.org/).

## What is Wagtail

Django is a great framework in its own right, but what makes it shine is the community around it. Web developers facing similar problems when building websites teamed up to create all sorts of tools that build upon the Django framework. One such tool is Wagtail, a _CMS_ (Content Management System) that solves the problem of writing and editing the content of websites collaboratively.

## Why do you need a CMS?

Maybe you don't! Django, a general web application framework, can be used to create any kind of site or web app. On the other hand, Wagtail is specifically made to build sites that contain a lot of content, most likely with people from different disciplines collaborating to build the site: content writers and editors; but also developers, designers, marketers, and more. You will benefit from a CMS if you want to make a blog, portfolio, business site, or any kind of site where content and collaboration are key.

## Wagtail installation

> **Note** This section assumes you have already [started your virtualenv and installed Django](https://tutorial.djangogirls.org/en/django_installation/).

Go to your console with `virtualenv` activated and run `pip install wagtail~=2.1.0` to install Wagtail:

{% filename %}command-line{% endfilename %}

```
(myvenv) ~$ pip install wagtail~=2.1.0
Collecting wagtail~=2.1.0
[...]
Installing collected packages: [...], wagtail
Successfully installed [...] [wagtail-2.1
```

And that should be it!

## Configuring Wagtail for your Django site

Now, we need to configure your existing Django site to use Wagtail.

### Changing settings

Let's make some changes in `mysite/settings.py`. Open the file using your code editor.

We'll start by telling Django about all of Wagtail's components. Find the `INSTALLED_APPS` setting in your settings file, and replace it with:

{% filename %}mysite/settings.py{% endfilename %}

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',

    'wagtail.contrib.forms',
    'wagtail.contrib.redirects',
    'wagtail.embeds',
    'wagtail.sites',
    'wagtail.users',
    'wagtail.snippets',
    'wagtail.documents',
    'wagtail.images',
    'wagtail.search',
    'wagtail.admin',
    'wagtail.core',

    'modelcluster',
    'taggit',
]
```

Then, in the `MIDDLEWARE` section just below, add the following lines right at the end of the array:

{% filename %}mysite/settings.py{% endfilename %}

```python
'wagtail.core.middleware.SiteMiddleware',
'wagtail.contrib.redirects.middleware.RedirectMiddleware',
```

Finally, we'll add something to give a bit of flavour to our site – a site name to display in the admin, with the `WAGTAIL_SITE_NAME` setting. This can be anything you want:

{% filename %}mysite/settings.py{% endfilename %}

```python
WAGTAIL_SITE_NAME = 'Django Girls Blog'
```

### Adding Wagtail to the database

We've already made a database when setting up Django – now we just need to add Wagtail’s tables to it. From your console, use `python manage.py migrate` and you should see something like this:

{% filename %}command-line{% endfilename %}

```
(myvenv) ~$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, blog, contenttypes, sessions, taggit, wagtailadmin, wagtailcore, wagtaildocs, wagtailembeds, wagtailforms, wagtailimages, wagtailredirects, wagtailsearch, wagtailusers
Running migrations:
  Applying taggit.0001_initial... OK
  [...]
  Applying wagtailusers.0006_userprofile_prefered_language... OK
```

### Django URLs for Wagtail

The last configuration step is to update our existing Django URLs to add new ones for Wagtail. Let's open `mysite/urls.py` with your code editor, and replace the file's content with:

{% filename %}mysite/urls.py{% endfilename %}

```python
from django.conf.urls import url, include
from django.contrib import admin
from django.conf import settings
from django.conf.urls.static import static

from wagtail.admin import urls as wagtailadmin_urls
from wagtail.documents import urls as wagtaildocs_urls
from wagtail.core import urls as wagtail_urls


urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^cms/', include(wagtailadmin_urls)),
    url(r'^documents/', include(wagtaildocs_urls)),
    url(r'^pages/', include(wagtail_urls)),
    url(r'', include('blog.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

Line by line,

- `wagtailadmin_urls` is the administration interface for Wagtail. This is separate from the Django admin (`admin.site.urls`).
- `wagtaildocs_urls` is the location from where document files (for example PDFs) stored on your site will be available.
- `wagtail_urls` is the base location for pages created with Wagtail. Here, we configure it to only manage pages starting with `pages/` so Django keeps full control over other pages.

---

And now we're good to go! From the directory that contains your site's `manage.py` file, start the server with `python manage.py runserver`:

{% filename %}command-line{% endfilename %}

```
(myvenv) ~$ python manage.py runserver
```

Head to `http://127.0.0.1:8000/cms` to access the Wagtail administration interface. To log in, use the same account you made for Django.
