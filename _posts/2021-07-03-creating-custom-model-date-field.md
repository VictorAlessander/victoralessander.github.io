---
title: Creating custom field on django model
---

I have a need to receive a date without the day, so the format is %Y-%m. I tried to evaluate if Django have a field that can be used for this situation, but for all the built-in date fields that Django have, all of them have the format with day attribute and does not support edit this format to have only the year and month.

Well, the field refers to a year/month reference, so it's ilogic to have the day with, so instead choose to use a third-party package to do this thing, I chosed to build my own custom date field.

Using any of third-party package I can have more than I really need and I will depend from the package maintainers to keep the code updated and upgrades will need to pass for some kind of avaliation, so with me building on my own, this process can be skipped. Although, I could customize using the third-party package as a scaffold for what I need, but still, I would like to have a full control of what I want or what I need to do with the field.

Django docs shows how to get started with [custom model fields](https://docs.djangoproject.com/en/3.2/howto/custom-model-fields/) and additionally with [custom lookups](https://docs.djangoproject.com/en/3.2/howto/custom-lookups/).

For me, I chose to use the CharField as a base class to build the custom date field that I called as YearMonthField.

```
from django.db.models import CharField


class YearMonthField(CharField):
  pass
```
