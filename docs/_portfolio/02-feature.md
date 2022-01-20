---
layout: single
title: "Feature info and howto's"
excerpt: "Different level tutorials on how to work with a certain feature"
header:
  teaser: /assets/images/teasers/rates.png
toc: true
toc_sticky: true
---

<div class="sampleinfo">

  <br>
  <strong>Request</strong><br>
  The ETL platform had a specific feature that was crucial for many customers. The platform's UI was rather techno-dependent, so a detailed video tutorial on using this feature was requested.<br>
  Since the feature was used by users of different access levels, it needed both shorter and more in-depth descriptions.<br>
  Also, a purely technical side of the platform - JSON-code - took a significant part in this feature and was often needed alone just to tweak this or that, so there had to be a specific fragment of tutorial that only elaborated on this particular part and its UI.<br><br>

  <strong>Solution</strong><br>
  <em>Rates</em> page.<br>
  For this set of tutorial I developed a proper scenario and data set to demonstrate all the sides of this feature. In cooperation with Support team, the key points of its daily usage were highlighted. For the shorter tutorial I created a simple video whereas the more in-depth one became a series of two videos plus an additional third one - with the purely technical part of the feature.<br><br>     
  
  <strong>Platform and tools used</strong><br>
  Docs site run on a static site generator; Git, VSCode, Markdown, iMovie, Movavi Video Editor.<br><br> 

  <a href="/assets/images/teasers/rates.png"><img src="/assets/images/teasers/rates.png"></a><br>
  &nbsp;

</div>

Rates are the factors that are used in calculations, eg: `Spend = Installs * 3`, where 3 - the rate.<br>
As a rule, rates differ by countries, OSs, time frames, etc. For all of that we have tools to make the Spend values always relevant.

## How to edit rates

In this video you will learn how to perform basic actions when dealing with rates: edit them, save those changes and re-collect the stats so that the final numbers would be re-calculated using the new rates.<br>

<iframe width="750" height="422" src="https://www.youtube.com/embed/cn1zgNekrwI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

The video guides you through the following steps:

1. Viewing the original calculation results in a dashboard [Datagrid widget](../visualization/datagrid.html){: .demolink} 
2. Editing the rates in a [macro](../mm/macros/macros.html){: .demolink} with the means of the [Merge Module **Arithmetics** component Visual editor](../ui/arithmetics_visual_editor.html){: .demolink}
3. Re-calculating the numbers by [re-collecting the Integration stats](../collection/collect_data.html){: .demolink}
4. Viewing the new rates calculation results

## Everything you wanted to know about rates

Technically speaking, rates calculations involve more actions to be set up and managed. Some of JustControl.it users might require deeper knowledge of those things and the two in-depth videos below will shed light on it.

### Part 1: How to check and where to edit

Detailed video on how to edit rates using [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} Merge Module component and check the result.

<iframe width="750" height="422" src="https://www.youtube.com/embed/tqxVQ4bGQ4E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

In the video you have the basics of how different rates are applied to different campaigns explained.<br>

1. The existing metric and newly created breakdowns (using the [**Value Mapper**](../mm/comp_valuemapper.html){: .demolink} Merge Module component) data columns that take part in Spend values calculation are shown on the Integration's [**Browse data**](../ui/integrations/browsedata.html){: .demolink} page.
2. The [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} Merge Module component that performs the calculations is shown in the [Integration's data transformation flow diagram](../mm/overview_mm.html#interface){: .demolink} 
3. Detailed explanation on how to read the [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} component's JSON-code are given (also available as a separate [How to read the Arithmetics code](#how-to-read-the-arithmetics-code-fragment){: .demolink} video)
4. Another way of editing the rates - via the [**Arithmetics** Visual editor](../ui/arithmetics_visual_editor.html){: .demolink} is shown both for an Integration and a macro config
5.  With the [**Arithmetics** Visual editor](../ui/arithmetics_visual_editor.html){: .demolink} and [**Browse data**](../ui/integrations/browsedata.html){: .demolink} + [**Tasks**](../ui/integrations/schedule_n_tasks.html#tasks){: .demolink} pages side by side, the rates changes and re-calculation results checking are demonstrated


#### "How to read the Arithmetics code" fragment

Learn which fields help calculating and storing the rates.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tqxVQ4bGQ4E?start=87" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

This is a fragment of the [Part 1: How to check and where to edit](#part-1-how-to-check-and-where-to-edit){: .demolink} video with a detailed explanation on how to read the [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} Merge Module component JSON-code.<br>
Watching it you'll find out what and where to edit to change the rate or to make them work for different campaigns, etc.

### Part 2: Keeping track of rates history

See how to use config relevances to make sure your rates are relevant for all the time frames.

**Note:** depending on where your rates are kept, can either be the Integration (shown in the video) or macro [config relevances](../ui/relevances.html){: .demolink}.
{: .notice--info}

<iframe width="750" height="422" src="https://www.youtube.com/embed/t0IV1roJ_WI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

In this video you will see how to set different rates to be used in the same case (country, OS, etc) but for different dates - create multiple [macro config's date range relevances](../ui/relevances.html){: .demolink}.

It is shown using this flow:
1. On the [**Config**](../ui/integrations/config.html){: .demolink} page, edit a date range relevance of the two configs making each of them relevant for its own date range. They will be ordered chronologically [on the list](../ui/relevances.html#list-order){: .demolink}
2. With the [**Arithmetics** Visual editor](../ui/arithmetics_visual_editor.html){: .demolink}, change the rates in one of the config relevances
3. On the [**Tasks**](../ui/integrations/schedule_n_tasks.html#tasks){: .demolink} page, re-collect the stats for the new config relevances and rates to be applied
4. On the [**Browse data**](../ui/integrations/browsedata.html){: .demolink}, check the calculations result for different dates
