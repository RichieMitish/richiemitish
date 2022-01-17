---
layout: single
title: "Tutorial"
excerpt: "Step-by-step tutorial on a certain option?"
header:
  teaser: /assets/images/teasers/tutorial.png
toc: true
toc_sticky: true
---

<div class="usecase">

  <br>
  <strong>USE CASE</strong> <br><br>

  <strong>Problem</strong><br>
  The ETL platform required a tutorial on adding a new source to a module that was already up and running.
  <br><br>

  <strong>Solution</strong><br>
  <em>Add statistics from another source Integration</em> page.<br>
  Since the platform's UI was rather techno-dependent, the tutorial had to also include examples with JSON-code and screenshots that would show where...<br>     
  <a href="/assets/images/teasers/tutorial.png"><img src="/assets/images/teasers/tutorial.png"></a><br>
  &nbsp;

</div>

**Related:** [Merge Module Visual Editor guide](../../ui/theeditor.html){: .demolink}

## Getting ready

Before connecting a new data source to the consolidated report, do determine which data you have to collect from the source, eg: the data source feeds *date, platform, gender, currency, country* whereas you need all of the above except for the *gender*. You will need that list for the first step of connection process.

**Note:**<br>
Keep in mind that the input integration can either be a raw data integration OR another Merge Module.
{: .notice--info}

Depending on that `entities` and `metrics` list, determine which one of the existing data flows is/are more suitable for the one you're setting (common `entities`, `metrics`, even if named differently, will help).
<br>

**Example**: two data sources of have have data *by installs*, three others - *by inapp events*. The integration you're connecting is collecting data *by inapp events*, so it's better to integrate it into the flow with three corresponding integrations. <br>

## 1. List the new data columns

### 1.1. Pause the integration

Change the integration status to **Pause**, see how to do that [here](../../ui/integrations/integrations_main.html#how-to-change-the-integrations-status){: .demolink}.

### 1.2. Add the fields

In the integration config' `entities` and `metrics` , list the new columns you want to add to your MM integration from the new data source. 

**Example:**<br>
We're adding `purchases`.

<a href="/assets/images/tutorial/ninp_01.png"><img class="align-center dropshadow" src="/assets/images/tutorial/ninp_01.png"></a>

## 2. Input Integration node 

Add the [**Input Integration**](../../mm/comp_inputintegration.html){: .demolink} component by dragging the corresponding node from nodes panel onto diagram area (see [the editor UI](../../mm/overview_mm.html#interface){: .demolink}).

1. **Labeling**<br>
    Label it using these templates:<br> 
    - `_mediaSourceName_integrationId_anyNote_`
    - `_dataSourceName_integrationId_mediaSourceName_` - for the Files module<br>
    **Examples:** <br>
    - `appsflyer_999_android_by_installs`
    - `files_998_someSemiAutomatedDataSource`
    
    Every node's label must tell user that component's role accurately and also be handy to copy-paste it into another component's code when needed.
    {: .notice--info}
    
2. **Data to collect**
    1. In the component's settings sidebar, select those **Breakdowns** (`entities`) and **Metrics** (`metrics`) that you want to collect from that data source and put into the data columns of your MM integration.
        <a href="/assets/images/tutorial/ninp_02.png"><img class="align-center dropshadow" src="/assets/images/tutorial/ninp_02.png"></a>
        
        **Example:** we're adding the integration 206 as a new data source and collecting "Date", "Campaign" and "Purchases" from it.<br>
    2. If there are any [filters](../../mm/inputfilters.html){: .demolink} or [macros](../../mm/macros/whyreuse.html){: .demolink} you'd like to apply, switch to the JSON-code view and write them out in `filters`.
    3. If there is some meta data fields that you wish to collect, enter the paths in `meta`.
        <a href="/assets/images/tutorial/ninp_03.png"><img class="align-center dropshadow" src="/assets/images/tutorial/ninp_03.png"></a>
                
        **Example:** we don't have to use macros or filter the stats, or to collect the meta data, so the corresponding fields are empty.

## 3. `data_source`

For debugging purposes, it is recommended to add the `data_source` tech field ("Data Source" column) using the [**New Entities**](../../mm/comp_newentities.html){: .demolink} component:
<a href="/assets/images/tutorial/data_source_imp.png"><img class="align-center dropshadow" src="/assets/images/tutorial/data_source_imp.png"></a>

- `key` - `data_source`
- `value` must be the same as the [**Input Integration**](../../mm/comp_inputintegration.html){: .demolink} node's label, eg: 
    * `_mediaSourceName_integrationId_`
    * `_dataSourceName_integrationId_mediaSourceName_` 
- node label: `data_source_integrationId_`

<a href="/assets/images/tutorial/ninp_04.png"><img class="align-center dropshadow" src="/assets/images/tutorial/ninp_04.png"></a>

**Example:** we don't have to use macros or filter the stats, or to collect the meta data, so the corresponding fields are empty.<br>

## 4. Integrate into the data flow

### 4.1. Fields renaming

The data source you're adding to your MM integration may give out same type data as the existing data sources do, but under different keys, eg: `campaign` and `camp_name`, `spend` and `cost`. In that case, renaming the new data source's column keys using the [**Rename**](../../mm/comp_rename.html){: .demolink} component would help:<br>

```json
{
    "camp_name": "campaign",
    "cost": "spend"
}
```

Same goes for the dates `entities` groups: rename them depending on the existing data flow, for merging purposes.<br>

Thus, when renaming metrics while connecting a new raw data source integration to a few already connected ones, it is better to stay true to data flows and titles of those already being in use as all the fields, [**Conditional Switches**](../../mm/comp_conditionalswitch.html){: .demolink} and [**Value Mappers**](../../mm/comp_valuemapper.html){: .demolink} etc are already set to those names.<br>

<a href="/assets/images/tutorial/ninp_05.png"><img class="align-center dropshadow" src="/assets/images/tutorial/ninp_05.png"></a>

**Example:** the new data source has campaign name in `campaign_name` field whereas in our data flow such data is stored in the `campaign` field, hence the renaming.<br>

#### Config's JSON-code example

Example config of the data flow above.

```json
{
  "name": "mergeModule_205",
  "title": "Merge Module",
  "type": "rewritable",
  "entities": [
    {
      "key": "date",
      "title": "Date",
      "type": "date",
      "primary": true
    },
    {
      "key": "campaign",
      "title": "Campaign"
    }
  ],
  "metrics": [
    {
      "key": "installs",
      "title": "Installs",
      "type": "absolute"
    },
    {
      "key": "clicks",
      "title": "Clicks",
      "type": "absolute"
    },
    {
      "key": "purchases",
      "title": "Purchases",
      "type": "absolute"
    }
  ],
  "params": {
    "macros": {},
    "components": {
      "facebook": {
        "name": "input/core",
        "params": {
          "moduleId": 176,
          "breakdowns": [
            "date",
            "campaign"
          ],
          "metrics": [
            "installs",
            "clicks"
          ],
          "timezone": "Europe/Moscow",
          "dateColumn": "date",
          "filters": {}
        },
        "diagramComponentLocation": "14 14"
      },
      "tiktok": {
        "name": "input/core",
        "params": {
          "moduleId": 177,
          "breakdowns": [
            "date",
            "cmp"
          ],
          "metrics": [
            "clicks",
            "converts"
          ],
          "timezone": "Europe/Moscow",
          "dateColumn": "date",
          "filters": {}
        },
        "diagramComponentLocation": "14 239"
      },
      "rename": {
        "name": "transform/rename",
        "params": {
          "map": {
            "cmp": "campaign",
            "converts": "installs",
            "campaign_name": "campaign"
          }
        },
        "diagramComponentLocation": "511.9951171875 188.99999999999994"
      },
      "output": {
        "name": "output/core",
        "params": {
          "fillMissedColumns": true,
          "ignoreExtraColumns": true
        },
        "diagramComponentLocation": "760.99267578125 188.99999999999994"
      },
      "new_entities": {
        "name": "transform/addConst",
        "params": [
          {
            "targetField": "data_source",
            "value": "facebook_176",
            "replace": false,
            "skipIfExists": true
          }
        ],
        "diagramComponentLocation": "262.99755859375 89"
      },
      "new_entities_copy": {
        "name": "transform/addConst",
        "params": [
          {
            "targetField": "data_source",
            "value": "tiktok_177",
            "replace": false,
            "skipIfExists": true
          }
        ],
        "diagramComponentLocation": "262.99755859375 238.99999999999994"
      },
      "new_entities_copy_copy": {
        "name": "transform/addConst",
        "params": [
          {
            "targetField": "data_source",
            "value": "googleads_206",
            "replace": false,
            "skipIfExists": true
          }
        ],
        "diagramComponentLocation": "268 432"
      },
      "googleads": {
        "name": "input/core",
        "params": {
          "moduleId": 206,
          "breakdowns": [
            "date",
            "campaign_name"
          ],
          "metrics": [
            "purchases"
          ],
          "timezone": "Europe/Moscow",
          "dateColumn": "date",
          "filters": {},
          "meta": {}
        },
        "diagramComponentLocation": "20 432"
      }
    },
    "relations": {
      "output": {
        "IN": [
          [
            "rename",
            "OUT"
          ]
        ]
      },
      "new_entities": {
        "IN": [
          [
            "facebook",
            "OUT"
          ]
        ]
      },
      "new_entities_copy": {
        "IN": [
          [
            "tiktok",
            "OUT"
          ]
        ]
      },
      "rename": {
        "IN": [
          [
            "new_entities_copy",
            "OUT"
          ],
          [
            "new_entities",
            "OUT"
          ],
          [
            "new_entities_copy_copy",
            "OUT"
          ]
        ]
      },
      "new_entities_copy_copy": {
        "IN": [
          [
            "googleads",
            "OUT"
          ]
        ]
      }
    }
  },
  "version": 2
}
```

### 4.2. Data transformations

In accordance with the the goals you want this Merge Module to help you with, add and configure other MM components. Find a full list of them and their descriptions here: [MM Components](../../mm/components_list.html){: .demolink}.