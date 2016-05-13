# django-nested-inlines

## *SilverFix'es Fork bugfix & changes*
- [inlines.js] **Fixed severe bug with number of TOTAL_FORMS when adding a new nested**
- [tabular.html] Fixed look 'n feel of the nested table (dynamic colspan handling)
- [admin.py] Fixed exception using it with a no-deletable inline
- [project structure] Deleted inlines.min.js
- [admin.py] NestedModelAdmin was pointing to wrong js filename
- [admin.py] Fixed a bug that would be skip any custom validation in clean() method
- [admin.py] [**Big thanks to @nastasi-oq**] Fixed a bug that would be raise exception if save_as_new enabled

## Overview

[Django issue #9025](http://code.djangoproject.com/ticket/9025)

Patches have been submitted, and repositories forked, but no one likes to use
either one. Now, nested inlines are available in an easy-to-install package.

### Issues

The Javascript portion of this app is currently buggy. The Python portion
should be solid. Please test and file issues and pull requests to improve
it!

## Installation

Uninstall django-nested-inlines if you install this package from other repository

`pip uninstall django-nested-inlines`

and install dj-nested-inlines

`pip install dj-nested-inlines`

## Usage

`nested_inlines.admin` contains three `ModelAdmin` subclasses to enable
nested inline support: `NestedModelAdmin`, `NestedStackedInline`, and
`NestedTabularInline`. To use them:

1. Add `nested_inlines` to your `INSTALLED_APPS` **before**
`django.contrib.admin`. This is because this app overrides certain admin
templates and media.
2. Import `NestedModelAdmin`, `NestedStackedInline`, and `NestedTabularInline`
wherever you want to use nested inlines.
3. On admin classes that will contain nested inlines, use `NestedModelAdmin`
rather than the standard `ModelAdmin`.
4. On inline classes, use `Nested` versions instead of the standard ones.
5. Add an `inlines = [MyInline,]` attribute to your inlines and watch the
magic happen.

## Example

	from django.contrib import admin
	from nested_inlines.admin import NestedModelAdmin, NestedStackedInline, NestedTabularInline
	from models import A, B, C
	
	class MyNestedInline(NestedTabularInline):
		model = C
	
	class MyInline(NestedStackedInline):
		model = B
		inlines = [MyNestedInline,]
	
	class MyAdmin(NestedModelAdmin):
		inlines = [MyInline,]
	
	admin.site.register(A, MyAdmin)

## Credits

This package is mainly the work of other developers. I've only taken their
patches and packaged them nicely for ease of use. Credit goes to:

- Gargamel for providing the base patch on the Django ticket.
- Stefan Klug for providing a fork with the patch applied, and for bugfixes.

See [Stefan Klug's repository](https://github.com/stefanklug/django/tree/nested-inline-support-1.5.x).
