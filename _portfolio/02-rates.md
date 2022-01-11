---
layout: single
title: "Rates"
excerpt: "How to set rates"
header:
  teaser: /assets/images/teasers/rates.png
toc: true
toc_sticky: true
---

<!--
sidebar:
  - title: "Use case"
    text: "New customers and employees intro guide"
-->

>**Use case**<br>
>blah blah blah
{: .notice--danger}

Rates are the factors that are used in calculations, eg: `Spend = Installs * 3`, where 3 - the rate.<br>
As a rule, rates differ by countries, OSs, time frames, etc. For all of that we have tools to make the Spend values always relevant.

## How to edit rates

In this video you will learn how to perform basic actions when dealing with rates: edit them, save those changes and re-collect the stats so that the final numbers would be re-calculated using the new rates.<br>

<iframe width="750" height="422" src="https://www.youtube.com/embed/cn1zgNekrwI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

The video guides you through the following steps:
1. Viewing the original calculation results in a dashboard [Datagrid widget](../visualization/datagrid.html) 
2. Editing the rates in a [macro](../mm/macros/macros.html) with the means of the [Merge Module **Arithmetics** component Visual editor](../ui/arithmetics_visual_editor.html)
3. Re-calculating the numbers by [re-collecting the Integration stats](../collection/collect_data.html)
4. Viewing the new rates calculation results

## Everything you wanted to know about rates

Technically speaking, rates calculations involve more actions to be set up and managed. Some of JustControl.it users might require deeper knowledge of those things and the two in-depth videos below will shed light on it.

### Part 1: How to check and where to edit

Detailed video on how to edit rates using [**Arithmetics**](../mm/comp_arithmetics.html) Merge Module component and check the result.

<iframe width="750" height="422" src="https://www.youtube.com/embed/tqxVQ4bGQ4E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

In the video you have the basics of how different rates are applied to different campaigns explained.<br>

1. The existing metric and newly created breakdowns (using the [**Value Mapper**](../mm/comp_valuemapper.html) Merge Module component) data columns that take part in Spend values calculation are shown on the Integration's [**Browse data**](../ui/integrations/browsedata.html) page.
2. The [**Arithmetics**](../mm/comp_arithmetics.html) Merge Module component that performs the calculations is shown in the [Integration's data transformation flow diagram](../mm/overview_mm.html#interface) 
3. Detailed explanation on how to read the [**Arithmetics**](../mm/comp_arithmetics.html) component's JSON-code are given (also available as a separate [How to read the Arithmetics code](#how-to-read-the-arithmetics-code-fragment) video)
4. Another way of editing the rates - via the [**Arithmetics** Visual editor](../ui/arithmetics_visual_editor.html) is shown both for an Integration and a macro config
5.  With the [**Arithmetics** Visual editor](../ui/arithmetics_visual_editor.html) and [**Browse data**](../ui/integrations/browsedata.html) + [**Tasks**](../ui/integrations/schedule_n_tasks.html#tasks) pages side by side, the rates changes and re-calculation results checking are demonstrated


#### "How to read the Arithmetics code" fragment

Learn which fields help calculating and storing the rates.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tqxVQ4bGQ4E?start=87" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

This is a fragment of the [Part 1: How to check and where to edit](#part-1-how-to-check-and-where-to-edit) video with a detailed explanation on how to read the [**Arithmetics**](../mm/comp_arithmetics.html) Merge Module component JSON-code.<br>
Watching it you'll find out what and where to edit to change the rate or to make them work for different campaigns, etc.

### Part 2: Keeping track of rates history

See how to use config relevances to make sure your rates are relevant for all the time frames.

**Note:** depending on where your rates are kept, can either be the Integration (shown in the video) or macro [config relevances](../ui/relevances.html).
{: .notice--info}

<iframe width="750" height="422" src="https://www.youtube.com/embed/t0IV1roJ_WI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

In this video you will see how to set different rates to be used in the same case (country, OS, etc) but for different dates - create multiple [macro config's date range relevances](../ui/relevances.html).

It is shown using this flow:
1. On the [**Config**](../ui/integrations/config.html) page, edit a date range relevance of the two configs making each of them relevant for its own date range. They will be ordered chronologically [on the list](../ui/relevances.html#list-order)
2. With the [**Arithmetics** Visual editor](../ui/arithmetics_visual_editor.html), change the rates in one of the config relevances
3. On the [**Tasks**](../ui/integrations/schedule_n_tasks.html#tasks) page, re-collect the stats for the new config relevances and rates to be applied
4. On the [**Browse data**](../ui/integrations/browsedata.html), check the calculations result for different dates
