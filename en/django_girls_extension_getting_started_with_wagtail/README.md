# Django Girls extension: Getting started with Wagtail

> **Info** This tutorial assumes you have already been through the main [Django Girls tutorial](https://tutorial.djangogirls.org/).

## What is Wagtail

Django is a great framework in its own right, but what makes it shine is the community around it. Web developers facing similar problems when building websites teamed up to create all sorts of tools that build upon the Django framework. One such tool is Wagtail, a _CMS_ (Content Management System) that solves the problem of writing and editing the content of websites collaboratively.

## Why do you need a CMS?

Maybe you don't! Django, a web application framework, can be used to create any kind of site or web app. On the other hand, Wagtail is specifically made to build sites that contain a lot of content, most likely with people from different disciplines collaborating to build the site: content writers and editors; but also developers, designers, marketers, and more. If you want to make a blog, portfolio, business site, or any kind of other site where content and collaboration are key – you will benefit from using a CMS.

## Wagtail installation

> **Note** This section assumes you have already [started your virtualenv and installed Django](https://tutorial.djangogirls.org/en/django_installation/).

Go to your console with `virtualenv` activated and run `pip install wagtail~=2.1.0` to install Wagtail:

```
(myvenv) ~$ pip install wagtail~=2.1.0
Collecting wagtail~=2.1.0
[...]
Installing collected packages: [...], wagtail
Successfully installed [...] [wagtail-2.1
```

And that should be it!

## Configuring Wagtail for your Django site

http://docs.wagtail.io/en/v2.1/getting_started/integrating_into_django.html
