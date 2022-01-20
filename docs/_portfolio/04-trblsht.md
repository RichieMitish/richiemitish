---
layout: single
title: "Troubleshooting errors"
excerpt: "Platform module's error messages, causes, solutions"
header:
  teaser: /assets/images/teasers/trblsht.png
toc: true
toc_sticky: true
---

<div class="sampleinfo">

  <br>
  <strong>Request</strong><br>
  The error messages that appeared upon running a certain process in one of the platform's modules weren't consistent, structured, informative enough. Backend team requested reworking of those messages.<br><br>

  <strong>Solution</strong><br>
  <em>Integration task run troubleshooting</em> page.<br>
  Using the list of error cases and messages provided and explained by backend team, I recreated and worked with each case in a sandbox environment in order to see what exactly it looked like for the platform user, what was helpful in solving the issue and how the message should have been displayed.<br>
  As a result of the first iteration:
  <ul>
    <li>error cases were categorized depending on the cause;</li>
    <li>solutions were found for each of the cases;</li>
    <li>a common structure of error messages was recommended;</li>
    <li>error codes were suggested for both module in question and platform wide usage;</li>
    <li>further developments were recommended for the module's backlog.</li>
  </ul>
  <br>     
  
  <strong>Platform and tools used</strong><br>
  Docs site run on a static site generator; Git, VSCode, Markdown.<br><br> 

  <a href="/assets/images/teasers/trblsht.png"><img src="/assets/images/teasers/trblsht.png"></a><br>
  &nbsp;

</div>

# **-- COMPONENT ISSUES --**

## **300010001** - unknown component

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The _componentName_ component _componentLabel_ has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR:
HH:MM:SS ║ 300010001 - The component '_componentName_' is unknown.
HH:MM:SS ║  
```

 

### Problem

Such a component does not exist.

 

### Solution

Do check the docs for the list of Merge Module components: [components list](../mm/components_list.html){: .demolink}. <br>
If you're using the [**Custom**](../mm/overview_mm.html#custom-node){: .demolink} component, please check the spelling of component's name that you're trying to use in **Custom type** field.


## **300010002** - not a composed component

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The _componentName_ component _componentLabel_ has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR:
HH:MM:SS ║ 300010002 - The _componentName_ component _componentLabel_ cannot be used as a composed one.
HH:MM:SS ║  
```

 

### Problem

The component that cannot be used as a [composed component](../mm/components_list.html#composable-components){: .demolink} was set as one.

 

### Solution

Please check the `_componentName_`'s documentation [on the components list](../mm/components_list.html){: .demolink} for whether it can or cannot be used as a composed one and fix its code if it cannot.

---


# **-- MISMATCHED FIELDS --**

## **300010003** - mismatched fields lists in Output (preview)

>**Note:** This error only occurs when the integration is run in the [**Preview**](../ui/integrations/schedule_n_tasks.html#preview){: .demolink} or [**Preview Range**](../ui/integrations/schedule_n_tasks.html#preview-range){: .demolink} modes.

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The Output component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010003 - Mismatched lists of entities and/or metrics provided in config and received by Output component. 
HH:MM:SS ║  
```

 

### Problem

The list of `entities` and `metrics` that was received by the preview building component **either from all the data flows or just one of them** is different from the [`params.entities` and `params.metrics`](../base/entities_metrics.html#overview){: .demolink} list that was provided in the config.<br>
Two possible cases when this error might had occurred:

1. **Config vs all the component's Inputs** 
    
    The entities and metrics listed in `params.entities` and `params.metrics` of the integration's config are different to those that were received by the [**Output**](../mm/comp_output.html){: .demolink} component on its input. <br>

    The fields given in the error message are either missing on the [`params.entities` or `params.metrics`](../base/entities_metrics.html#overview){: .demolink} of the config or weren't filled with values in the data flow.

2. **Config vs either one of the component's inputs (Input X vs Input Y)**
    
    The field(-s) will be under `"missed"`|"Not received by component" in the error message.<br>
    The lists of fields that come to the component's inputs are somehow different from one another. 

 

### Solution

1. **Config vs all the component's Inputs** 

    If you need the field in your config, make sure you have it listed on [`params.entities` or `params.metrics`](../base/entities_metrics.html#overview){: .demolink} and filled with values in the data flow.
        Otherwise just delete the field.

    **Detailed solution:**<br>
    1. **In JSON.** Ctrl+F/Cmd+F your config for the key that was given in the error message.<br> 
        If you need that field, make sure you have it: 
        - either **listed on the [`params.entities` or `params.metrics`](../base/entities_metrics.html#overview){: .demolink} of your config** - if you need the values to be displayed on **Browse data**/**Dashboards** pages. 
        - or **deleted** after it's served its purpose, using the corresponding [**Remove**](../mm/comp_remove.html){: .demolink} component, - if that's a tech field and you don't need to see its values, etc.  

        If you don't need that field, just delete it from your config.
        
    2. **On diagram.** <br>
        If you need that field:
        - "Not in config" error message: depending on the missing field's kind, add it to [`params.entities` or `params.metrics`](../base/entities_metrics.html#overview){: .demolink} list of your config's JSON-code, defining its parameters.
        - "Not on input" error message: make sure that field is used and filled with values at the proper step of your data flow.

        If you don't need that field:
        - "Not in config" error message: find the component that adds the field to your config and delete the occurrence. The component might be either [**New Entities**](../mm/comp_newentities.html){: .demolink} or [**New Metrics**](../mm/comp_newmetrics.html){: .demolink}, or the one that has `targetField` in its code. 
        - "Not on input" error message: delete the field from [`params.entities` or `params.metrics`](../base/entities_metrics.html#overview){: .demolink} list of your config's JSON-code. 


2. **Config vs either one of the component's inputs (Input X vs Input Y)**

    If you need the field in your config, make sure it gets filled with `N/A` or `0` for all the config input's data flows at one of the final steps of your overall data flow.

    If you don't need the field in your config, just delete it.

---

## **300010004** - mismatched fields lists in Output (collection)

>**Note:** This error only occurs when the integration is run in the [**Statistics**](../ui/integrations/schedule_n_tasks.html#statistics){: .demolink} or [**Statistics Range**](../ui/integrations/schedule_n_tasks.html#statistics-range){: .demolink} modes.

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The Output component "_componentTitle_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010004 Mismatched lists of entities and/or metrics provided in config and received by Output component. 
HH:MM:SS ║  
```

 

### Problem

[Same as for 300010003.](#problem-2)

 

### Solution

[Same as for 300010003.](#solution-2)

---

## **300010005** - mismatched fields lists: matrices cannot be merged

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ Matrices cannot be merged.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010005 - Mismatched lists of entities and/or metrics provided in config and received by Output component. 
HH:MM:SS ║  
```

 

### Problem

This error can occur in the [**Output**](../mm/comp_output.html){: .demolink} component.<br>
Once the component has checked the fields lists, received from all the previous components' outputs and provided in the integration config, for matching each other, it then:
- encounters an error
- proceeds with merging the data tables (as matrices) into one<br>

This error occurs if the merge has failed. It fails due to the same reason of fields lists being mismatched.<br>
The error should not occur as of March 15, 2021, since the component must show the error [**300010004**](#300010004---mismatched-fields-lists-in-output-collection){: .demolink} when checking the lists - prior to attempting the matrices merge.

 

### Solution

[Same as for 300010003.](#solution-2)

---

## **300010006** - mismatched fields lists in uniqueChecker

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The uniqueChecker component "_componentTitle_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010006 - Mismatched lists of entities and/or metrics provide in config and received by uniqueChecker component. 
HH:MM:SS ║  
```

 

### Problem

[Same as for 300010003](#problem-2), but occurred on the [uniqueChecker](../mm/comp_uniquechecker.html){: .demolink} component's inputs.

 

### Solution

[Same as for 300010003.](#solution-2)

---

# **-- SPECIFIC COMPONENTS ISSUES --**


## **300010007** - duplicated fields in uniqueChecker

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The uniqueChecker component "_componentTitle_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010007 - The uniqueChecker component "_componentTitle_" has detected duplicated fields. 
HH:MM:SS ║    
```

 

### Problem

The component `uniqueChecker` received duplicated fields on its input.

 

### Solution

See the list of duplicated fields given in the error message and fix them being duplicated.

---

## **300010008** - date field type is invalid

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The uniqueChecker component "_componentTitle_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010008 - Invalid type _theInvalidType_ of _fieldName_ `firstField` date field in Cohort component _componentLabel_. Required type: 'string'.
HH:MM:SS ║ 
HH:MM:SS ║ COMPONENT:
HH:MM:SS ║ Component's config:
HH:MM:SS ║ 
```

if it's the 2nd one:

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The uniqueChecker component "_componentTitle_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010008 - Invalid type _theInvalidType_ of _fieldName_ `secondField` date field in Cohort component _componentLabel_. Required type: 'string'.
HH:MM:SS ║ 
HH:MM:SS ║ COMPONENT:
HH:MM:SS ║ Component's config:
HH:MM:SS ║ 
```

 

### Problem

The [**Cohort**](../mm/comp_cohort.html){: .demolink} component's date field(-s) was/were set the invalid type.

 

### Solution

Check the [**Cohort**](../mm/comp_cohort.html){: .demolink} component's date fields: [`firstField` or `secondField`](../mm/comp_cohort.html#parameters){: .demolink}. Both of them must be of `string` type, fix the type if any other one is set.

---
## **300010016** - JSON is invalid

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The JSON Extractor component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010016 - The JSON provided by data source is invalid.
HH:MM:SS ║    
```

 

### Problem

This error occurs in the [**JSON Extractor**](../mm/comp_jsonextractor.html){: .demolink} component.<br>
The JSON provided by data source is invalid and has to be fixed.

 

### Solution

Make sure the source provides your integration with a valid JSON.<br>
Do use a JSON validator to check if the JSON is valid, here's a couple of them: [jsonformatter.curiousconcept.com](https://jsonformatter.curiousconcept.com/), [jsonlint.com](https://jsonlint.com/).

---

## **300010010** - type of extracted value is invalid

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The JSON Extractor component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010010 - The extracted value's type is wrong (object or array). Must be a scalar type. 
HH:MM:SS ║ 
HH:MM:SS ║ COMPONENT:
HH:MM:SS ║ Component's config:
HH:MM:SS ║   
```

 

### Problem

This error occurs in the [**JSON Extractor**](../mm/comp_jsonextractor.html){: .demolink} component.<br>
Instead of the value's expected scalar type (extracted values types are `entity`, `metric` or `date`), an array or an object was found and extracted from the JSON by defined `keyPath`.

 

### Solution

In [**JSON Extractor**](../mm/comp_jsonextractor.html){: .demolink} component of your config, check if the JSON and `keyPath` field are correct.

---

## **300010014** - unknown aggregated function

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The _componentName_ component "_componentTitle_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010014 - Unknown aggregate function.
HH:MM:SS ║
```

 

### Problem

The indicated _componentName_ component "_componentTitle_" has encountered an unknown aggregate function.

 

### Solution

Please make sure the functions used in indicated component have no mistakes to them. Do also check the component's documentation. 

---

## **300010024** - requested currencies unavailable

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The Currency Converter component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010024 - Some vendors do not have the requested currencies. 
HH:MM:SS ║
```

 

### Problem

The error occurs in the [**Currency Converter**](../mm/comp_currencyconverter.html){: .demolink} component.<br>
Vendors do not have the requested currencies available to use.

 

### Solution

Please reach out to our Support team at <a href="mailto:support@justcontrol.it">support@justcontrol.it</a> informing them about the issue. Do provide them with the name of integration you're trying to run.

---

# **-- FIELDS ISSUES --**

## **300010012** - field does not exist

**Error message**
 
```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The _componentName_ component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010012 - The column _fieldName_ does not exist.  
HH:MM:SS ║ 
```

 

### Problem

The indicated field is missing in the integration config.

 

### Solution

Depending on the field's contents, define the field in the config's [`entities` or `metrics`](../base/entities_metrics.html#overview){: .demolink}.

---

## **300010013** - field exists already

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The _componentName_ component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010013 - The component is trying to add the _fieldName_ field that exists already.  
HH:MM:SS ║ 
```

 

### Problem

The component indicated in the error message is set to add and fill with values a field that has already been added and filled earlier in the data flow.

 

### Solution

Find the component that's adding the field in question and fix it.

These components can add fields, do check them in your config:
- [**Integration as Dictionary**](../mm/comp_integrationasdictionary.html){: .demolink}
- [**Normalize Geo**](../mm/comp_normalizegeo.html){: .demolink}
- [**New Entities**](../mm/comp_newentities.html){: .demolink}
- [**New Metrics**](../mm/comp_newmetrics.html){: .demolink}
- [**New Entities by Original IDs**](../mm/comp_newentitiesbyoriginalids.html){: .demolink}
- [**New Column by Original Values**](../mm/comp_newcolumnbyoriginalvalues.html){: .demolink}
- [**Cohort**](../mm/comp_cohort.html){: .demolink}
- [**Copy Columns**](../mm/comp_copycolumns.html){: .demolink}
- [**Currency Converter**](../mm/comp_currencyconverter.html){: .demolink}
- [**Value Extractor**](../mm/comp_valueextractor.html){: .demolink}
- [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink}
- [**JSON Extractor**](../mm/comp_jsonextractor.html){: .demolink}
- [**Meta Extractor**](../mm/comp_metaextractor.html){: .demolink}
- [**Metrics to Entities**](../mm/comp_metricstoentities.html){: .demolink}
- [**Time Period Sum up**](../mm/comp_timeperiodsumup.html){: .demolink}
- [**Value Mapper**](../mm/comp_valuemapper.html){: .demolink}

---

## **300010015** - invalid date

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The _componentName_ component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010015 - The date _invalidDate_ in field _fieldName_ is invalid.  
HH:MM:SS ║ 
```

 

### Problem

The date received in the indicated field is invalid.

 

### Solution

Please check the dates in [date ranges](../ui/integrations/schedule_n_tasks.html#from---to){: .demolink} and [date presets](../ui/integrations/schedule_n_tasks.html#date-preset){: .demolink} used in this integration and fix the wrong one(-s).

---

# **-- GENERAL ISSUES --**

## **300010009** - no stats in the Core

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The Input Integration component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010009 - The component cannot load stats of _moduleName_ module integration _moduleId_ "_integrationName_" from the Core. 
HH:MM:SS ║ 
```

 

### Problem

The Core is not giving out stats of the indicated module.

 

### Solution

Please reach out to our Support team at <a href="mailto:support@justcontrol.it">support@justcontrol.it</a> informing them about the issue. Do provide them with the name of integration you're trying to run.

---

## **300010016** - cannot save entities to the Core

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The Output component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010016 - The component cannot save entities of _moduleName_ module integration _moduleId_ "_integrationName_" to the Core. 
HH:MM:SS ║ 
```

 

### Problem

The [**Output**](../mm/comp_output.html){: .demolink} cannot save entities of the indicated module to the Core.

 

### Solution

Please reach out to our Support team at <a href="mailto:support@justcontrol.it">support@justcontrol.it</a> informing them about the issue. Do provide them with the name of integration you're trying to run.

---

## **300010011** - cannot save stats to the Core

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The Output component "_componentLabel_" has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010011 - The component cannot save stats of _moduleName_ module integration _moduleId_ "_integrationName_" to the Core. 
HH:MM:SS ║ 
```

 

### Problem

The [**Output**](../mm/comp_output.html){: .demolink} cannot save stats of the indicated module to the Core.

 

### Solution

Please reach out to our Support team at <a href="mailto:support@justcontrol.it">support@justcontrol.it</a> informing them about the issue. Do provide them with the name of integration you're trying to run.

---

## **300010018** - config version is unknown

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The integration run has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010018 - Merge Module config version is unknown. 
HH:MM:SS ║ 
```

 

### Problem

The version number in the [integration config's `version` field](../base/structure.html#integration-config){: .demolink} is unknown.

 

### Solution

Please change [the value of `version` field](../base/structure.html#integration-config){: .demolink} to `2` so that it would be:

```json
"version": 2,
```

---

## **300010019** - transaction start failed

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The integration run has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010019 - Cannot start the transaction. 
HH:MM:SS ║ 
```

 

### Problem

The integration could not start the transaction.

 

### Solution

Please reach out to our Support team at <a href="mailto:support@justcontrol.it">support@justcontrol.it</a> informing them about the issue. Do provide them with the name of integration you're trying to run.

---

## **300010020** - transaction failed

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The integration run has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010020 - Cannot commit the transaction. 
HH:MM:SS ║ 
```

 

### Problem

The integration could not commit the transaction.

 

### Solution

Please reach out to our Support team at <a href="mailto:support@justcontrol.it">support@justcontrol.it</a> informing them about the issue. Do provide them with the name of integration you're trying to run.

---

## **300010021** - no relevant config for the date

**Error message**

```json
HH:MM:SS ║ EXECUTION FAILED:
HH:MM:SS ║ The integration run has encountered an error.
HH:MM:SS ║ 
HH:MM:SS ║ ERROR: 
HH:MM:SS ║ 300010021 - The relevant config for selected date(-s) _datesList_ is missing. 
HH:MM:SS ║ 
```

 

### Problem

There is no [relevant integration config](../ui/relevances.html){: .demolink} for the indicated date(-s).

 

### Solution

Please make sure the selected [date range](../ui/integrations/schedule_n_tasks.html#from---to){: .demolink} or [date preset](../ui/integrations/schedule_n_tasks.html#date-preset){: .demolink} is correct or create the missing [config relevance](../ui/relevances.html){: .demolink} for the date in question.
