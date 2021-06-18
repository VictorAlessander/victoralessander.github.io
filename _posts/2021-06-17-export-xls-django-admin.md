---
title: How I dealt with export data through spreadsheets from django admin
updated: 2021-06-17 22:54
---

I had a need to export content from django admin and I knew that django-import-export package could be used for that.

Unfortunately I couldn't use because the project was already using to import data from admin page the core package that currently django-import-export package uses, the notorious package called tablib.

So, to preserve the default of project I chosed to develop using the tablib package and here's what I did.

To turn the code more generic as possible for others export needs, I decided to develop a export module class...

```
class SpreadsheetExportHandler:

    def __init__(self, *args, **kwargs):
        super().__init__(self, *args, **kwargs)

    ...
```

and make the admin class inherit from it...

```
class BlogAdmin(SpreadsheetExportHandler, admin.ModelAdmin):

    def __init__(self, *args, **kwargs):
        super().__init__(self, *args, **kwargs)
```

I could do using the [builder](https://refactoring.guru/design-patterns/builder) pattern too, but I judge that this is enough for what I needed.

Using like this, I can offer the flexibility of use the default methods of SpreadsheetExportHandler class or to override any of methods that I included into him and will not force me to create an instance of class for use it, avoiding myself to be repetitive and making the things more clean.

The order of inheritance is important, because the ModelAdmin super class of django wasn't developed to make possible multiple inheritance, so I changed the order of inheritance to make my new class to call and pass the parameters for the ModelAdmin constructor class.
