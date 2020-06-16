# django-query-params
Django app providing template tags and JavaScript functions for query string management.

## Template Tag Library

To install the app, type:

```bash
(venv)$ pip install django-query-params
```

Then add `"query_params"` to the `INSTALLED_APPS` in the settings.

To use the template tags in templates:

```djangotemplate
{% load query_params_tags %}

{% modify_query param_to_remove another_param_to_remove param_to_change="new-value" another_param_to_change="new-value" %}

{% add_to_query param_to_remove another_param_to_remove param_to_add="new-value" another_param_to_add="new-value" %}

{% remove_from_query param_to_remove another_param_to_remove="value" %}
```

## JavaScript Library

```djangotemplate
{% load static %}
<script src="{% static 'query_params/js/query_params.js' %}"></script>

<script>
var url1 = modify_query(
    location, 
    ['param_to_remove', 'another_param_to_remove'], 
    {
        param_to_change: 'new-value',
        another_param_to_change: 'new-value'
    }
);

var url2 = add_to_query(
    location,
    ['param_to_remove', 'another_param_to_remove'],
    {
        param_to_add: 'new-value',
        another_param_to_add: 'new-value'
    }
);

var url3 = remove_from_query(
    location,
    ['param_to_remove'],
    {
        another_param_to_remove: 'value'
    }
);
</script>
```

## Example

Let's say the current URL is:  
`https://example.com/posts/?page=2&sort=by-date&tag=environment&tag=sustainability`

### modify_query

```djangotemplate
{% modify_query page tag="ecological" %}
```

will render:

`/posts/?sort=by-date&amp;tag=ecological`

### add_to_query

```djangotemplate
{% add_to_query page tag="ecological" %}
```

will render:

`/posts/?sort=by-date&amp;tag=ecological&amp;tag=environment&amp;tag=sustainability`

### remove_from_query

```djangotemplate
{% remove_from_query page tag="environment" %}
```

will render:

`/posts/?sort=by-date&amp;tag=sustainability`
