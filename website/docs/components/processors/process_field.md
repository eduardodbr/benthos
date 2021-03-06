---
title: process_field
type: processor
status: deprecated
---

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the contents of:
     lib/processor/process_field.go
-->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

:::warning DEPRECATED
This component is deprecated and will be removed in the next major version release. Please consider moving onto [alternative components](#alternatives).
:::

A processor that extracts the value of a field [dot path](/docs/configuration/field_paths)
within payloads according to a specified [codec](#codec), applies a list of
processors to the extracted value and finally sets the field within the original
payloads to the processed result.


<Tabs defaultValue="common" values={[
  { label: 'Common', value: 'common', },
  { label: 'Advanced', value: 'advanced', },
]}>

<TabItem value="common">

```yaml
# Common config fields, showing default values
process_field:
  codec: json
  path: ""
  result_type: string
  processors: []
```

</TabItem>
<TabItem value="advanced">

```yaml
# All config fields, showing default values
process_field:
  codec: json
  path: ""
  result_type: string
  processors: []
  parts: []
```

</TabItem>
</Tabs>

The result can be marshalled into a specific data type with the field
[`result_type`](#result_type).

It's therefore possible to use this codec without any child processors as a way
of casting string values into other types. For example, with an input JSON
document `{"foo":"10"}` it's possible to cast the value of the
field foo to an integer type with:

```yaml
process_field:
  path: foo
  result_type: int
```

## Codecs

### `json`

Parses the payload as a JSON document, extracts and sets the field using a dot
notation path.

### `metadata`

Extracts and sets a metadata value identified by the path field.

## Fields

### `codec`

A [codec](#codec) to use in order to extract (and set) the target field.


Type: `string`  
Default: `"json"`  
Options: `json`, `metadata`.

### `path`

A [dot path](/docs/configuration/field_paths) pointing to the target field.


Type: `string`  
Default: `""`  

### `result_type`

The final data type to marshal the processing result into. The `discard` type is a special case that discards the result of the processing steps entirely.


Type: `string`  
Default: `"string"`  
Options: `string`, `int`, `float`, `bool`, `object`, `discard`.

### `processors`

A list of child processors to execute on the extracted value.


Type: `array`  
Default: `[]`  

### `parts`

An optional array of message indexes of a batch that the processor should apply to.
If left empty all messages are processed. This field is only applicable when
batching messages [at the input level](/docs/configuration/batching).

Indexes can be negative, and if so the part will be selected from the end
counting backwards starting from -1.


Type: `array`  
Default: `[]`  

## Alternatives

The [`branch` processor](/docs/components/processors/branch) offers a
more flexible and robust way to perform the actions of this processor.

