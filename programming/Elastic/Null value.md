Fields that contain `null` or an empty array are treated as non-fields: they do not trigger dynamic [[Mapping]], and cannot be searched or indexed.

NB that empty strings are not considered null values: it is valid to, e.g., submit a `match` query for empty string values.

If potentially-null fields should be indexed and searchable, create an explicit [[Mapping]] for the field in `mappings.properties.[property_name].null_value`.  When a  document with an explicit `null` value for this field is indexed, the `null_value` will be swapped in, and will be searchable just like any other field value.

The `null_value` must be same type as the mapping `type`.

The `null_value` only influences indexing, it does not modify the `_source` document.

NB that an empty array is NOT an explicit `null` value, and will not be replaced with `null_value` at search time--it will be invisible to Elastic except in `_source`. Replace empty arrays with explicit `null` before the document is indexed.