:man_page: mongoc_collection_update_one

mongoc_collection_update_one()
==============================

Synopsis
--------

.. code-block:: c

  bool
  mongoc_collection_update_one (mongoc_collection_t *collection,
                                const bson_t *selector,
                                const bson_t *update,
                                const bson_t *opts,
                                bson_t *reply,
                                bson_error_t *error);

Parameters
----------

* ``collection``: A :symbol:`mongoc_collection_t`.
* ``selector``: A :symbol:`bson:bson_t` containing the query to match the document for updating.
* ``update``: A :symbol:`bson:bson_t` containing the update to perform.
* ``reply``: Optional. An uninitialized :symbol:`bson:bson_t` populated with the update result, or ``NULL``.
* ``error``: An optional location for a :symbol:`bson_error_t <errors>` or ``NULL``.

.. include:: includes/update-one-opts.txt

Description
-----------

This function updates at most one document in ``collection`` that matches ``selector``.

To update multiple documents see :symbol:`mongoc_collection_update_many`.

See Also
--------

`MongoDB update command documentation <https://docs.mongodb.com/master/reference/command/update/>`_ for more information on the update options.

:symbol:`mongoc_collection_update_many`

:symbol:`mongoc_collection_replace_one`

Errors
------

Errors are propagated via the ``error`` parameter.

Returns
-------

Returns ``true`` if successful. Returns ``false`` and sets ``error`` if there are invalid arguments or a server or network error.

A write concern timeout or write concern error is considered a failure.

If provided, ``reply`` will be initialized and populated with the fields ``matchedCount``, ``modifiedCount``, and optionally ``upsertedId`` if applicable. The reply must be freed with :symbol:`bson:bson_destroy`.

Example
-------
.. literalinclude:: ../examples/example-update.c
   :language: c
   :caption: example-update.c