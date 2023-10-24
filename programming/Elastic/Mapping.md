Exist to provide a way to tell Elastic what kind of data it should treat a field as being

## Dynamic mapping

Every field in an indexed record must have a mapping. If there is no explicit mapping for a field, it is created automatically. The type of a dynamic field is [inferred based on the underlying JSON value.](https://www.elastic.co/guide/en/elasticsearch/reference/current/dynamic-field-mapping.html#dynamic-field-mapping) 

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