## Indexing behaviors
Use `_create` operation to only index a document if it does not already exist. Use `_doc` operation to upsert, i.e. create document if it doesn't exist and update it if it does. 

https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-reindex.html

Elastic has a dedicated API for re-indexing documents. Re-indexing is necessary to change existing field mappings, they cannot be updated in-place.

A re-indexing op must have a source and a destination, and the initiator must have read privileges on the source idx, and write privilege on the target idx. In addition, the source idx must not have its `_source` field disabled.

By default the behavior when a document with the same id is encountered in in source and target is