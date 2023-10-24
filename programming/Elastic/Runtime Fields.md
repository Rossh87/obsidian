Runtime fields aren't indexed, they're retrieved at query time . This makes data ingestion fast and is flexible, and decreases storage costs b/c indices are smaller, but search performance will be worse. Simplifies mapping decisions b/c fields can be added after indexing occurs.

Runtime fields can later be turned into indexed fields. When this happens, queries that reference the runtime field will automatically use the indexed field without any change to the query.

Often a better alternative to `script` fields. `script` fields can only fetch values, but runtime fields can be used in queries and aggregations. 