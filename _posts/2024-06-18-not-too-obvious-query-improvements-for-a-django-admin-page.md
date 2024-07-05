---
title: Not Too Obvious Query Improvements for a Django Admin Page
---

Some Django projects have a demand for the admin side, often accessed by internal users. Situations like this can save a lot of development time since Django provides a built-in solution that can be extended to have more features using a fairly effort, however, sometimes the data size grows and the response time that used to be fast enough now becomes slow and painful that can even cause 504 errors.

When this issue arrives and you tried some approaches that initally worked but later simply are not effective anymore, giving the sensation of a band-aid solution, this is the time to take time and carefully review metrics and not too obvious choke points.

The idea of this post is to make you understand that sometimes some approches will come with trade-offs, like negatively impacting the page functionality.
#### Pagination (direct impact on the UX)
#### Default Sorting (direct impact on the UX)
## Other approaches not related to the Django Admin
#### The `select_related` method
#### The `prefetch_related` method and the `Prefetch` class
#### Use a read-replica database

## Takeaway
Using a cache, creating column indexes and some other approaches can be effective and enough, however, when isn't always possible to implement them for X reasons, the approaches described here can give some kind of relief.
