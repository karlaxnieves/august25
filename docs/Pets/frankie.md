---
title: Frankie
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  image: https://files.readme.io/f0bc35e-IMG_5829.jpeg
  robots: noindex
next:
  description: ''
---
Data types in Gantry encode the way data should be interpreted, regardless of the format it is in when it is logged. 

## How are data types used in Gantry?

The data type for each field determines how that field can be used in Gantry. For example:

- How that data is displayed in the data table
- What alerts, metrics, and projections can be computed on the field

## Available data types

The following types are available in Gantry:



### Array types

Gantry has built in support for one-dimensional Array types, which are logged as Python lists of native Python types: `str`, `float`, `int`, `bool`. Arrays are inherently high-dimensional, like Text, so Gantry often uses Projections to better understand their content. For example, length is a property that can be monitored for all arrays using the `vector.length` Projection. For numerical arrays, `vector.<min, max. norm>` Projections can be computed to in order to observe other scalar scalar properties such as statistics (mean), extrema (min, max), and norms (L1, L2). Filtering on Arrays is also possible using the `Array contains` filter, which will return any record whose Array field contains an exact or partial match for at least one element. For example, an `“Array contains”` filter for the substring `"is"` would return any Record with an `Array<str>` field with any element containing `"is"`, such as `["this is", "an array", "of strings"]`. This can be useful for filtering multi-label lists or tag attributes that might be part of an application.

## Schema inference

Gantry infers the schema for an application based on the first batch of data that logged. As more data is logged, new fields that appear are automatically added to the schema. To change the type of a field, the schema needs to be edited.

### Supported types and inferencing logic

The following table details supported types, and the logic used to infer that type. Note that for primitive & array primitive types, Gantry relies on [type checking logic built into pyarrow](https://arrow.apache.org/docs/python/api/datatypes.html#type-checking) 

| Gantry Data Type | Inferencing Logic                                                                                                                                                                |
| :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Float            | If the value is a pyarrow floating point numeric type                                                                                                                            |
| Text             | if the value is a pyarrow string type                                                                                                                                            |
| Integer          | if the value is a pyarrow integer type                                                                                                                                           |
| Boolean          | if the value is a pyarrow boolean type                                                                                                                                           |
| Categorical      | if the set of values in the batch consist of strings where the average string has less than 2 words in it (basically if the values are mostly 1 word strings)                    |
| ID               | if the value is an instance of a python uuid object, or is a string representation of a uuid object                                                                              |
| Datetime         | if it is a pandas timestamp object or if the string can be parsed using `pandas.to_datetime`                                                                                     |
| UnixTime         | Time from Unix Epoch in ms or seconds. Since this is impossible to distinguish from large integers, this must be manually set as UnixTime.                                       |
| ArrayString      | if the value is a pyarrow list with the list's `value_type` being a pyarrow string                                                                                               |
| ArrayFloat       | if the value is a pyarrow list with the list's `value_type` being a pyarrow float                                                                                                |
| ArrayInteger     | if the value is a pyarrow list with the list’s value_type being a pyarrow integer                                                                                                |
| ArrayBoolean     | if the value is a pyarrow list with the list’s value_type being a pyarrow boolean                                                                                                |
| ArrayID          | if the values contain arrays which consist of values that can be inferred as ID types                                                                                            |
| Image            | Currently, we assume files stored in s3 are images, and so if the value is an s3 url, we infer the column to be an Image. We plan to support other sources in the future.        |
| Audio            | Currently, we assume files stored in GCS are audio, and so if the value is a GCS presigned url, we infer the column to be Audio. We plan to support other sources in the future. |
| Json             | Currently yet unsupported, this must be manually set.                                                                                                                            |
| Embedding        | If the set of values in a batch is a pyarrow list with the list's `value_type` being float, all lists are the same length, and the length is at least 512.                       |
| Unknown          | If the value does not match any of the other types. This servers as a catch all default value for inference.                                                                     |

### Mixed columns

If a column contains mixed primitives or mixed array primitives, then the type of the column will be set to `Unknown`. For more complex string types, such as Image or Audio, the column will only be inferred as that type if the majority of the values are that type. Otherwise, the column will be set to `Unknown`.

### Nested schema

Gantry supports nested schema inference. `.` is reserved to represent a nested field. Any `.` characters in the field name will be converted to `_`.

Here is an example of data with nested fields:

```python
{
  "integer": {
    "feature.1": 1,
    "feature.2": 2,
    "feature_3": 3
  },
  "categorical": {
    "feature_1": "category.1",
    "feature.2": "category.2"
  },
  "text.feature.1": "Hello, World"
}
```



Gantry infers the above schema as follows:

| Field                 | Type        |
| :-------------------- | :---------- |
| numeric.feature_1     | Integer     |
| numeric.feature_2     | Integer     |
| numeric.feature_3     | Integer     |
| categorical.feature_1 | Categorical |
| categorical.feature_2 | Categorical |
| text_feature_1        | Text        |

## Handling bad data

Gantry does data cleaning to handle bad data for primitives. Future support is planned for cleaning more complex types.

[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Data Cleaning",
    "0-0": "Integer",
    "0-1": "If the bad value is a:  \n- Float: Floats get set to `null`  \n- Boolean: True gets set to 1 and False gets set to 0.  \n- String: If the value can be parsed as an Integer or Float, it will be, then Floats get further casted to Integers. If not, the value gets set to `null`.",
    "1-0": "Float",
    "1-1": "If the bad value is a:  \n- Integer: Integers work fine and get casted as Float.  \n- Boolean: True gets set to 1.0 and False gets set to 0.0.  \n- String: If the value can be parsed as a Float, then it will be, otherwise it will be set to `null`.",
    "2-0": "Boolean",
    "2-1": "If the bad value is a:  \n- Integer: If the value is equal to 0 then it gets set to False. If it equal to 1 it gets set to True.  \n- Float: If the value is equal to 0.0 then it gets set to False. If it is equal to 1.0 it gets set to True.  \n  \nAll other values and strings get set to `null`.",
    "3-0": "Text",
    "3-1": "All values get casted to a string, and `null` values stay as `null`"
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]

## Editing the schema

Sometimes the schema will be inferred incorrectly, or the data type of a field will change. To edit a schema manually:

1. Use the sidebar to navigate to the ingestion page:

![](https://files.readme.io/2dc7380-edit_schema_first_ingestion.png "edit_schema_first_ingestion.png")



2. Click the three dots on the right side of the page to change the data type:

![](https://files.readme.io/b54e041-click_dots.png "click_dots.png")



## Example: data types and schemas

```python
gantry.log_record(
    application="my_app",
    inputs={
        "numerical_feature_1": 1.1,
        "numerical_feature_2": 87,
        "categorical_feature_1": "cat_A",
        "text_feature_1": "cat_A is one of our categories",
        "image_feature_1": "s3://bucket/image.jpg",
        "audio_feature_1": "https://storage.googleapis.com/example-presigned-audio.mp3",
    },
    ...
)
```



In this example, there are a few ambiguities in how the data will be handled:

- Both of the inputs `numerical_feature_*` are numbers, but they each have different Python data types.
- The inputs `categorical_feature_1` and `text_feature_1` are both represented as strings in Python, but the former is meant to be interpreted as a category and the latter as text.
- All of `text_feature_1`, `image_feature_1`  , `audio_feature_1` are strings, but the first one is just text, whereas the latter two should be specially treated as Image and Audio.

Data types are stored in an application’s Schema. The Schema maps fields to Gantry data types. The following is an example schema for the example application above:

| Field                 | Type        |
| :-------------------- | :---------- |
| numerical_feature_1   | Integer     |
| numerical_feature_2   | Float       |
| categorical_feature_1 | Categorical |
| text_feature_1        | Text        |
| image_feature_1       | Image       |
| audio_feature_1       | Audio       |