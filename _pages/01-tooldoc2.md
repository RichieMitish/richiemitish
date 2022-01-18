---
layout: single
title: "Visual editor tool documentation"
excerpt: "Description, parameters and usage examples for one of the platform's Visual editor tools"
header:
  teaser: /assets/images/teasers/tooldoc.png
toc: true
toc_sticky: true
---

<div class="usecase">

  <br>
  <strong>USE CASE</strong><br><br>

  <strong>Problem</strong><br>
  The ETL platform had a Visual editor that allowed building a data transformation flow diagram with its tools. Each tool required a documentation page for it, the one that would provide both technical info on how exactly the tool transforms data and a couple of examples for it.<br><br>

  <strong>Solution</strong><br>
  <em>Data merging tools</em> pages with <em>Aggregate by Values</em> page (for that very tool) among others.<br>
  Each tool had a dedicated page that listed the tool's description, parameters to set, JSON-code templates and a couple of "original stats - the tool set a certain way - the resulting stats" style examples.<br><br>
  <a href="/assets/images/teasers/tooldoc.png"><img src="/assets/images/teasers/tooldoc.png"></a><br>
  &nbsp;

</div>

&#x261D; **Tech name:** `transform/mapper`<br>
&nbsp;&nbsp;&nbsp;&nbsp; [Composable](components_list.html#composable-components){: .demolink}, [Skippable](components_list.html#skippable-components){: .demolink}<br>

**MM Visual editor diagram node:**
<div><img src="/assets/images/tooldoc//valuemapper.png"></div>

## Description
The component maps the field by the set pattern, created the target field and puts the mapping result in the target field.

---

## Parameters
- **`targetField`** [required] - the result (defined in `map` or `map.replace` fields) will be put here. Should not be the primary field unless needed for a very particular reason
- **`field`** [required] - the field being mapped
- **`map`** [required] - mapping scenario:
  - **`pattern`** - if this (regular expressions allowed) is found in the mapped field, component stores the corresponding result (defined below) in the target field; can be an empty string
  - **`replace`** - the result that will be stored in target field if the word/expression defined in `pattern` is found in mapped field
- **`default`** [string] - if no patterns, defined above, are found, this will be put in the target field.
  
  If `"replace": "true", "skipIfExists": "false"`,`targetField` contains values and they're not empty, those values will not be rewritten with the `default` one.
  {: .notice--info}
- **`replace`** [default: `false`] - see [Skippable components](components_list.html#skippable-components){: .demolink}
- **`skipIfExists`** [default: `false`] - see [Skippable components](components_list.html#skippable-components){: .demolink}

**Regexp:** use `/u` modifier to make sure Cyrillic characters presence will not make the component fail.
{: .notice--info}

### Notes
The component can also be used as the copying component for any non-`date` type `entities` groups, see example 2 below.

**Important:** `originalId` will not get copied (same as for the [**New Column by Original Values**](comp_newcolumnbyoriginalvalues.html){: .demolink}) when copying with this component.
{: .notice--warning}

---

## JSON-code templates

- MM Visual editor
  ```json
  [
    {
      "field": "_entitiesKey1_beingMapped_",
      "targetField": "_entitiesKey2_mappedTo_",
      "map": [
        {
          "pattern": "_regexpAllowed_",
          "replace": "_whatToPutInTargetField_"
        }
      ],
      "default": "_defaultValue_",
      "replace": true,
      "skipIfExists": false 
    }
  ]
  ```
- Full component code
  ```json
  {
    "name": "transform/mapper",
    "params": [
      {
        "field": "_entitiesKey1_beingMapped_",
        "targetField": "_entitiesKey2_mappedTo_",
        "map": [
          {
            "pattern": "_regexpAllowed_",
            "replace": "_whatToPutInTargetField_"
          }
        ],
        "default": "_defaultValue_",
        "replace": true,
        "skipIfExists": false 
      }
    ],
    "comment": "any information"
  }
  ```

---

## **- EXAMPLES -**

## 1. General example

1. The original stats:

    | campaign_name | view | 
    | ---------- | ------  |
    | someapp_ios_j002r | 5 |
    | android_2app | 3 |
    | coolcmpgn_IOS_777 | 10 |
    | andr_pickme-cmp | 10 |

2. In each `campaign_name` value there's a platform identifier/marker - `ios`, `android`, `andr`.<br>
To add `platform` entities group and fill it with data - in accordance with the platform identifier in the `campaign_name` fields - map it:

    ``` json
    {
      "targetField": "platform",
      "field": "campaign_name",
      "map": [
        {
          "pattern": "/andr|android/i",
          "replace": "Android"
        },
        {
          "pattern": "/ios/i",
          "replace": "iOS"
        }
      ],
      "default": "N/A"
    }
    ```

3. The resulting stats:

    | campaign_name | view | platform |
    | ---------- | ------  | ------ |
    | someapp_ios_j002r | 5 | iOS |
    | android_2app | 3 | Android |
    | coolcmpgn_IOS_777 | 10 | iOS |
    | andr_pickme-cmp | 10 | Android |

## 2. Copying with the **Value Mapper**

Here's how you can copy non-`date` type `entities` groups with this component:

```json
{ 
   "targetField" : "targetFieldKey",
   "field" : "fieldKey",
   "default" : null
}
```

This way the component will simply copy all the `fieldKey` data into the newly created `targetFieldKey`.

`originalId` doesn't get copied (same as for the [**New Column by Original Values**](comp_newcolumnbyoriginalvalues.html){: .demolink}).
{: .notice--warning}

Running preview of the config, you will be notified: <br>

```
Invalid component configuration `componentTitle` (transform/mapper): property map errors: The map field is required."
```