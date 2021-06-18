---
title: How I dealt with export data to spreadsheet from django admin
updated: 2021-06-18 20:10
---

I had a need to export content from django admin and I knew that django-import-export package could be used for that.

Unfortunately I couldn't use because the project was already using to import data from admin page the core package that currently django-import-export package uses, the notorious package called tablib.

So, to preserve the default of project I chosed to develop using the tablib package and here's what I did.

To turn the code more generic as possible for others export needs, I decided to develop a simple export module class based on [builder](https://refactoring.guru/design-patterns/builder) pattern...

```
class SpreadsheetBuilder:

    def __init__(self, *args, **kwargs):
        super().__init__(self, *args, **kwargs)

    ...

    def build_spreadsheet(self):
        ...

    ...
```

and make the admin class inherit from it...

```
class BlogAdmin(SpreadsheetBuilder, admin.ModelAdmin):

    def __init__(self, *args, **kwargs):
        super().__init__(self, *args, **kwargs)
```

Using like this, I can offer the flexibility of use the default methods of SpreadsheetBuilder class or to override any of methods that I included into him and will not force me to create an instance of class for use it, avoiding myself to be repetitive and making the things more clean.

The order of inheritance is important, because the ModelAdmin super class of django wasn't developed to make possible multiple inheritance, so I changed the order of inheritance to make my new class to call and pass the parameters for the ModelAdmin constructor class.
