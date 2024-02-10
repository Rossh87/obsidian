Exist to provide a way to tell Elastic what kind of data it should treat a field as being

## Dynamic mapping

Every field in an indexed record must have a mapping. If there is no explicit mapping for a field, it is created automatically. The type of a dynamic field is [inferred based on the underlying JSON value.](https://www.elastic.co/guide/en/elasticsearch/reference/current/dynamic-field-mapping.html#dynamic-field-mapping) Note especially that a string-based field that fails date and number detection will be dynamically set to type `text`, not `keyword`.

By default, dynamic mapping is enabled. It can be enabled/disabled at the top level of mappings, or on inner fields (in `properties`). `dynamic` can be set to 1 of 4 values, each with a different behavior:
1. `true (default)`: new fields are added to the existing mapping
2. `runtime`: new fields are added as [[Runtime Fields]]. They are not indexed.
3. `false`: new fields are ignored, but will be present in `_source` field of returned hits. Ignored fields can't be searched and are not indexed.
4. `strict`: error if a field without an explicit mapping is detected.

Get fine-grained dynamic mapping control with [dynamic templates](https://www.elastic.co/guide/en/elasticsearch/reference/current/dynamic-templates.html). 

## Explicit mapping

Set with 
```python
# PUT my-idx-01
{
	"mappings": {
	# ...mappings
	}
}

# or
# PUT my-idx-01/_mapping
{
  # ...mappings
}
```

In general, an explicit mapping is necessary for anything other than the default. E.g. setting custom analyzers or tokenizers for a `text` field, creating a multi-field, setting a text-based field as type `keyword` rather than `text`, etc.


## Field types
There are a large number of [possible field types](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-types.html), many of which are specialized. some of the most common are:
- `text` types: unstructured string types, e.g. text descriptions, user-submitted content, etc.
- `keyword` types: use to store specific structured content (e.g. ids, tags), often searched with `term`
- `numeric` types: different sizes and precisions are available. Optimized for `range` queries.
- `spatial` types: usual suspects, geojson points and shapes etc.
- `object` type: type of a JSON object structure. Not usually necessary to explicitly map to this type, as it is inferred by the presence of sub-properties in the mapping declaration. When indexing records with a large number of different, arbitrary fields and subfields, use `flattened` type to store the entire object as a single field. This prevents a mapping explosion from a dynamic mapping being created for each field/subfield, but each leaf value is indexed as a string keyword without any analysis of number/date detection, which limits options for querying. However, it is still possible to specify subfields.
- `nested` type: Elastic has no concept of inner hierarchies: all inner fields are flattened into a simple list of field names and values. e.g:
```python
{
 "group": "fans":
 "names": {"first": "alice", "last":"white"}, {"first": "jon", "last":"smith"}
}
```
will become:
```python
{
 "group": "fans",
 "names.first": ["alice", "jon"],
 "names.last": ["white", "smith"],
}
```
To index arrays of objects and maintain the relationship between specific field values and specific objects, use the `nested` field type. Internally, this creates a separate Lucene document for each object in the array, plus a parent document. At query time the parent and children can be stitched back together if desired. This field type is expensive to index and query, and should only be used if it is important to query for matches on specific subdocuments.

Note there is no array type; any field can have 0 or more values, but all must be of the same field type. If a field has more than 1 value, queries will match any of the values.