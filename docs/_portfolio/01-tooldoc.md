---
layout: single
title: "Visual editor tool info"
excerpt: "Description, parameters and usage examples for one of the platform's Visual editor tools"
header:
  teaser: /assets/images/teasers/aggregatebyvalues.png
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
  <a href="/assets/images/teasers/aggregatebyvalues.png"><img src="/assets/images/teasers/aggregatebyvalues.png"></a><br>
  &nbsp;

</div>

&#x261D; Tech name: `transform/keepTitle`<br>
&nbsp;&nbsp;&nbsp;&nbsp; [Composable](components_list.html#composable-components){: .demolink}<br>

**MM Visual editor diagram node:**
<figure>
	<a href="/assets/images/tooldoc/aggregatebyvalues.png"><img src="/assets/images/tooldoc/aggregatebyvalues.png"></a>
</figure>

## Description
Allows saving the entities in JC.it database, through the MM integration, by their `title`s instead of `id`s from the data source integration (`title` values get copied into the `originalId` [subcolumn](../base/entities_metrics.html#subcolumns){: .demolink}).

## Parameters
- **`targetField`** [required] - `entities` key

## JSON-code templates

- MM Visual editor
  ```json
  [
    {
      "targetField": "_entitiesKey_"
    }
  ]
```
- Full component code
  ```json
  {
    "name": "transform/keepTitle",
    "params": [
      {
        "targetField": "_entitiesKey_"
      }
    ],
    "comment": "any information"
  }
  ```
<!--END_DOCUSAURUS_CODE_TABS-->

## **- EXAMPLES -**

## 1. General example

There are two data sources: facebook and tiktok. <br>
In the facebook data flow, the `country` entity had been created by using the [**New Entities**](comp_newentities.html){: .demolink} component, whereas the tiktok had the `country` entity available to be collected from source initially. <br>
So both data flows have the same meaning and titles entities before the merge point and thus there will be duplicated statistics after that point.<br>
To avoid that, this component will combine both entities data into one `country` entity after the data flows merge point.


1. The original stats<br>

    By `data_source`:

    | data_source | country | *country.originalId* | view | 
    |  ---------- | ------  | --------  | ------  |
    | facebook | UK | *94975234* | 5 |
    | facebook | AU | *23087089* | 3 |
    | tiktok | UK | *2356083* | 10 |

    By `country`:

    | country | view | 
    |  ---------- | ------  |
    | UK | 5 |
    | AU | 3 |
    | UK | 10 |

    Instead of collapsing into a single row, the UK stats got separated.<br>

2. The component's JSON-code<br>

    To prevent such separation, the **Aggregate by Values** component can be used:
    ```json
    [
      {
        "targetField": "country"
      }
    ]
    ```

3. The resulting stats<br>
    By `data_source`

      | data_source | country | *country.originalId* | view | 
      |  ---------- | ------  | ------  | --- |
      | facebook | UK | UK | 5 |
      | facebook | AU | AU | 3 |
      | tiktok | UK | UK | 10 |

    By `country`

      | country | view | 
      |  ---------- | ------  |
      | UK | 15 |
      | AU | 3 |

## 2. Detailed flow example

### Single data source

Let's take a look at how the single source data is saved in JC.it Core by data source module integration and loaded into the MM integration: 
1. **Original source data** - saved in the Core, `.id`'s are assigned to all the entities in `entities` group (here - `campaign`)

    | *campaign.title* | *campaign.id* | *campaign.originalId* |
    | --- | --- | --- |
    | camp_01 | 10 | **1000** |
    | camp_02 | 20 | **2000** |
2. **In MM without** [**Aggregate by Values**](comp_aggregatebyvalues.html){: .demolink}: *`campaign.id`* gets rewritten creating new entities for this integration; *`campaign.originalId`* copied from source integration's *`campaign.id`*

    | data_source |*campaign.title* | *campaign.id* | *campaign.originalId* |
    | --- | --- | --- | --- |
    | source_01 | camp_01 | 30 | **10** |
    | source_01 | camp_02 | 40 | **20** |
3. **In MM with** [**Aggregate by Values**](comp_aggregatebyvalues.html){: .demolink}: *`campaign.id`* gets rewritten creating new entities for this integration; *`campaign.originalId`* copied from source integration's *`campaign.title`*

    | data_source |*campaign.title* | *campaign.id* | *campaign.originalId* |
    | --- | --- | --- | --- |
    | source_01 | camp_01 | 30 | **camp_01** |
    | source_01 | camp_02 | 40 | **camp_02** |

### Multiple data sources

What about processing two+ data sources stats? Or, for some reports, the `entities` that have been added using the [**New Entities**](comp_newentities.html){: .demolink} component and the `entities` that have being collected from data source, both have same `title`s. In such case, the statistics within the `entities` group will get separated: both entities with **same `title`** will be displayed due to having **different `originalId`s**. This component will merge such same `title`s entities into one by copying their (same) `title`s into their `originalId`s.<br>
1. **Data source 1 integration**

    | *campaign.title* | *campaign.id* | *campaign.originalId* | views |
    | --- | --- | --- | --- |
    | camp_01 | 10 | **1000** | 10 |
    | camp_02 | 20 | **2000** | 10 |
2. **Data source 2 integration**

    | *campaign.title* | *campaign.id* | *campaign.originalId* | views |
    | --- | --- | --- | --- |
    | camp_01 | 30 | **10000** | 5 |
    | camp_02 | 40 | **20000** | 5 |    

3. **In MM without** [**Aggregate by Values**](comp_aggregatebyvalues.html){: .demolink}: *`campaign.id`* gets rewritten creating new entities; *`campaign.originalId`* copied from source integration's *`campaign.id`*<br><br>
    **Viewing by `data_source`**

      | data_source |*campaign.title* | *campaign.id* | *campaign.originalId* | views |
      | --- | --- | --- | --- | --- |
      | source_01 | camp_01 | 50 | **10** | 10 |
      | source_01 | camp_02 | 60 | **20** | 10 |
      | source_02 | camp_01 | 70 | **30** | 5 |
      | source_02 | camp_02 | 80 | **40** | 5 |

      Using source integration's `id`s (`10`-`20` and `30`-`40`) as `originalId`s here and matching the latter to source integrations' `id`s, MM finds the entities one by one and loads their `title`s and metrics. Totally new `id`s (`50`-`80`) are assigned to this MM integration's new entities.<br><br>
    **Viewing by `campaign.title`**

      | *campaign.title* | *campaign.id* | *campaign.originalId* | views |
      | --- | --- | --- | --- |
      | camp_01 | 50 | **10** | 10 |
      | camp_02 | 60 | **20** | 10 |
      | camp_01 | 70 | **30** | 5 |
      | camp_02 | 80 | **40** | 5 |

      All the rows describe completely different entities. Hence both campaigns data got separated and stats is incorrect in all the rows.
4. **In MM with** [**Aggregate by Values**](comp_aggregatebyvalues.html){: .demolink}: *`campaign.id`* gets rewritten creating new entities; *`campaign.originalId`* copied from source integration's *`campaign.title`*<br><br>
    **Viewing by `data_source`**

      | data_source |*campaign.title* | *campaign.id* | *campaign.originalId* | views |
      | --- | --- | --- | --- | --- |
      | source_01 | camp_01 | 50 | **camp_01** | 10 |
      | source_01 | camp_02 | 60 | **camp_02** | 10 |
      | source_02 | camp_01 | 50 | **camp_01** | 5 |
      | source_02 | camp_02 | 60 | **camp_02** | 5 |
 
      Using source integration's `title` (`camp_01` and `camp_02`) as `originalId` here and matching the latter to source integrations' `title`, MM: finds the entity, loads its metrics, assigns totally new `id`s (`50`-`60`) to this MM integration's new entities OR same ones - if such an entity (with same `originalId` and `title`) has already been created within this integration.<br><br>
    **Viewing by `campaign.title`**

      |*campaign.title* | *campaign.id* | *campaign.originalId* | views |
      | --- | --- | --- | --- |
      | camp_01 | 50 | **camp_01** | 15 |
      | camp_02 | 60 | **camp_02** | 15 |
  
      Thanks to this component, rows that contain same campaigns data have become rows of same entities - with same`originalId` and `title` - hence the stats could sum up, becoming correct for both campaigns.