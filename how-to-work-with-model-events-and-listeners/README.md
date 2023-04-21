
## Laravel 10 How To Work with Model Events And Listeners

In Laravel, Model Events and Listeners are a way to hook into the lifecycle of an Eloquent model and perform some action when certain events occur.

### What are Model Events in Laravel?

A Model in Laravel application provides an abstraction for working with a database table with a high-level API. Among these APIs, events are which are fired when actions are performed on the model.

Here are the following events which we can use with laravel model –

1. ``creating`` and ``created``: Fires before and after records have been created.
2. ``updating`` and ``updated``: Fires before and after records are updated.
3. ``saving`` and ``saved``: Fires before and after records are saved (i.e created or updated).
4. ``deleting`` and ``deleted``: Fires before and after records are deleted or soft-deleted.
5. ``restoring`` and ``restored``: Fires before and after soft-deleted records are restored.
6. ``retrieved``: Fires after records have been retrieved.

### See Complete Article, [Click here](https://onlinewebtutorblog.com/laravel-10-how-to-work-with-model-events-and-listeners/)