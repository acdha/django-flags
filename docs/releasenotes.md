# Release Notes

## 4.1.1

### What's new?

- `boolean` and `anonymous` conditions now accept [multiple possible string representations of truth](/conditions/#boolean) as their values.
- `parameter` conditions now accept [possible parameter values](http://localhost:7777/conditions/#parameter).

## 4.1

### What's new?

- Added the option to specifiy [required conditions](/usage/#defining-flags) that must always be met.
- Deprecated support for using a single dictionary to hold key/values of conditions for a settings-based feature flag. Support will be removed in Django-Flags 5.0. Use [a list of dictionaries or tuples instead](/settings/#flags).
- Added a [`before date` condition](/conditions) that is met whenever the current date is before the expected date.

## 4.0.3

### What's new?
- The system check introduced in 4.0.2 will no longer raise a `ProgrammingError` or an `OperationalError` when run pre-migration.

## 4.0.2

### What's new?
- Logging of non-existent conditions is now a Django system check.

## 4.0.1

### What's new?
- `condition.check()` returns a Falsy `None` instead of raising a `TypeError` when a configured condition has no function registered.

## 4.0

### What's new?

- The template functions `flag_enabled` and `flag_disabled` in both [Django](/api/django) and [Jinja2](/api/jinja2) templates now support taking keyword arguments that could be used by [custom conditions](/api/conditions).
- Jinja2 template functions are now available via a Jinja2 extension that can be [included in `settings.py`](/api/jinja2). 
- The optional `flags.middleware.FlagConditionsMiddleware` has been added to ensure that all feature flag checks throughout single request cycle use the same flag conditions.
- Support for specifying the [source of feature flags in `settings.py`](/settings#flag_sources) has been added to allow further customization and the potential to limit flags to settings or database-only.
- The "user" condition now supports custom user models. ([@callorico](https://github.com/callorico))

### Upgrading

Django-Flags 4.0 introduces backwards-incompatible changes for users of Jinja2 templates.

Previously Django-Flags provided `flags.template_functions.flag_enabled` and `flags.template_functions.flag_disabled` functions that had to be registered in the Jinja2 environment downstream. The Django-Flags documentation recommended doing so in `jinja2.Environment.globals.update()`. **`flags.template_functions` has been removed in Django-Flags 4.0.**

Jinja2 function registration is now handled by a `flags.jinja2tags.flags` Jinja2 extension. To use Django-Flags 4.0 with Jinja2 templates, the `TEMPLATES` setting in `settings.py` should to be modified to include the extension:

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.jinja2.Jinja2',
        ...
        'OPTIONS': {
            'extensions': [
                ...
                'flags.jinja2tags.flags',  # add this line to your existing settings
                ...
            ],
        }
    },
] 
```

## 3.0.2

### What's new?

- Requests are now optional the `flag_enabled` and `flag_disabled` template tags.
- Flag state form conditions are now bound when the form is created to ensure all custom conditions are available on the form. ([@callorico](https://github.com/callorico))

## 3.0.1

### What's new?

- Django 2.1 is now supported.

## 3.0

Django-Flags is a fork of the Django-only components of the [Wagtail-Flags](https://github.com/cfpb/wagtail-flags) feature flag library. This is the initial release.

