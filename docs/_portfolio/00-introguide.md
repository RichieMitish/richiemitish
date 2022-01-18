---
layout: single
title: "Intro guide"
excerpt: "Product intro guide as the platform's basic scenario"
header: 
  teaser: /assets/images/teasers/datatochart.png
toc: true
toc_sticky: true
---

<div class="usecase">

<br>
  <strong>USE CASE</strong> <br><br>

  <strong>Problem</strong><br>
  To ensure a proper onboarding process, an intro guide was required for the platform. It had to provide a better understanding of the main steps of the workflow, platform's tools and options available even for the basic case scenario.<br><br>

  <strong>Solution</strong><br>
  <em>Turning raw data into a useful chart</em> guide.<br>
  After shaping and analyzing a few possible customer journey maps for our platfrom, I chose this particular one for being the most user friendly and profitable. All the necessary parts of the workflow were created both for the guide's screenshots and flow and to be used as demo parts in future. For the new customers and employees that had a dedicated environment (demo or their own account), those demo parts were available to play with, following this guide.<br><br>
  <a href="/assets/images/teasers/datatochart.png"><img src="/assets/images/teasers/datatochart.png"></a><br>
  &nbsp;

</div>

So how do you I use this magic tool of yours, you ask?<br>

This is a brief description of the first steps that you're about to take with our product. Please find a more in-depth description in the **Workflow in details section** in the menu on your left. Full info and all the details on every step are given in the corresponding sections in the same menu you see on your left. All the links here will bring you to those corresponding sections.

In your own account, you will have a few demo source Integrations to recreate all the steps described here and know JustControl.it better.<br><br>
This is a basic example of a scenario that can be built in the product. <br>

&#8505;&nbsp;&nbsp;**Info:**<br>
For the data source Integrations, we are using fake ones with fake data, hence those steps that involve creating an Integration and connecting it to the data source cannot be fully recreated at this point.
{: .notice--info}

Moving to the scenario. Say, you need to see the overall **Spend** metric values for the campaigns that are running on two data sources: Facebook and TikTok. <br>
Let's walk through the product starting from the login-pass welcome email to the dashboard with your data visualized on it.

## 1. Welcome email

In the email you receive your creds and the account link. Click the link, enter your creds. 

<a href="/assets/images/introguide/wemail.png"><img class="align-center dropshadow" src="/assets/images/introguide/wemail.png"></a>

You will be redirected to the [**Integrations**](){: .demolink} page of your account. The page is almost empty as of now, of course, showing only the demo Integrations.<br>

<a href="/assets/images/introguide/00_intstart.png"><img src="/assets/images/introguide/00_intstart.png"></a>

To make the data appear on your [**Dashboards**](../ui/dashboards/dashboards_main.html){: .demolink}, we will have to collect it from the data sources that you use (here, TikTok and Facebook), merge it all together, cooking it the way you need, and then visualize it using our [Dashboard widgets](../ui/dashboards/dashboards_main.html#widgets){: .demolink}.<br>

So let's move on to the next step. For the data to appear in your JC.it account, it must be collected into the account's dedicated Integration.

## 2. Create an Integration

You already have two demo Integrations to work with and they do not have to be connected to any data sources. But for the full workflow demonstration purposes, let's have a look at how the actual data source module Integrations work at these very first steps. 

Obviously, you can create multiple Integrations for those data source we have modules for, see the list [here](../modules/modules_list.html){: .demolink}. Each Integration contains data collected [by certain parameters](../ui/integrations/schedule_n_tasks.html#--task-run-parameters--){: .demolink} on a [certain schedule](../ui/integrations/schedule_n_tasks.html#--schedule-rule-parameters--){: .demolink}, all of it is initially set up at this step.

To create a new Integration, in [**Integrations**](../ui/integrations/integrations_main.html){: .demolink} click **NEW INTEGRATION**, select the data source that you want to collect your data from and enter it's name at the second step of this flow.

<a href="/assets/images/introguide/01_newint.png"><img src="/assets/images/introguide/01_newint.png"></a>

The initialization log screen will appear. Wait for the **Module initialized** message and **STOPPED** status.

<a href="/assets/images/introguide/01_init.png"><img src="/assets/images/introguide/01_init.png"></a>

In our case that would be **TikTok**. Since we are using a fake one, do find it on the [Integrations list](../ui/integrations/integrations_main.html#page-overview){: .demolink} and open it.

## 3. Connect to the data source

In order to collect the data, your TikTok Integration must have an access to your TikTok account. So this step is even simpler: connect your Integration to TikTok using your account's creds (or tokens, or keys - different data sources use different ways of authorization).

It is done in the [Integration settings sidebar](../ui/integrations/integrations_main.html#settings){: .demolink}, click the gear icon near the Integration's title to open it:

<img class="align-center" src="/assets/images/introguide/01_gear.png">

Next, click the **CREATE AUTH CONNECTOR** button and [connect it](../srcconnection/connecttiktok.html){: .demolink}.

<a href="/assets/images/introguide/01_conn.png"><img src="/assets/images/introguide/01_conn.png"></a>

## 4. Collect the data into your Integration

>&#8505;&nbsp;&nbsp;**Note:**<br>
Starting from this step, you can recreate the actions on your demo Integration. We're also using it as an example Integration in screenshots.

Once your TikTok Integration is set up and has access to your TikTok data, you can collect the latter to it.

For you to do that, the Integration [status](../ui/integrations/integrations_main.html#status){: .demolink} must be **Running**, whereas currently its **Initialized**. Let's run the Integration. 

In its [settings sidebar](../ui/integrations/integrations_main.html#settings){: .demolink}, click **RUN** and confirm the action.

<a href="/assets/images/introguide/01_run.png"><img src="/assets/images/introguide/01_run.png"></a>

The running Integration can collect data. To do that, you have to run the corresponding Integration task on it. Click **RUN MANUALLY**, and set the following [task run parameters](../ui/integrations/schedule_n_tasks.html#--task-run-parameters--){: .demolink}:

- **Task:** Statistics Range
- **From - To:** Jan 1 - Jan 31, 2021 

This is what it will look like:

<a href="/assets/images/introguide/01_taskrun.png"><img src="/assets/images/introguide/01_taskrun.png"></a>

After setting them, click **RUN**.

The [task run log screen](../ui/integrations/schedule_n_tasks.html#log-view){: .demolink} will appear. Wait till the status says **STOPPED** and log shows an **Executed successfully** confirmation. 

&#8505;&nbsp;&nbsp;**Info:**<br>
That notification means a completion of any task you can run on an Integration:<br><img class="align-center" src="/assets/images/introguide/01_taskstopped.png">
{: .notice--info}

The Integration has collected your TikTok data. Now you can check the result by browsing it on a corresponding page.

>&#8505;&nbsp;&nbsp;**Note:**<br>
>After running the data collection task once, you will have the *currently relevant data* transferred from data source into your Integration. Surely it will be outdated soon, so in order to always have updated and relevant data, the [data collection schedule](../ui/integrations/schedule_n_tasks.html#schedule){: .demolink} will have to be set. <br>

We'll skip this for now and will look at it closely when giving you an in-depth workflow overview in the **Workflow in details** section here: [**Schedule the data collection**](../workflow/build/schedule_collection.html){: .demolink}.

## 5. Browse the collected data

Now you have a TikTok Integration with your data in it. To check if the collection went fine and the data is correct, you can browse it on the [**Browse data**](../ui/integrations/browsedata.html){: .demolink} page. 

Upon the opening it says **There is no data yet…** because the data browsing parameters are not set yet. 

<img src="/assets/images/introguide/01_browsedata_blank.png">

In the [date range picker](../ui/integrations/browsedata.html#date-range-picker){: .demolink}, select that date range that we have collected the data for: *Jan 1 - Jan 31, 2021*.<br> Next, click **DATE** and tick the other breakdown - **CAMPAIGN** - too. This way you are selecting them to be displayed. Click **APPLY** to apply the breakdowns selection.

<a href="/assets/images/introguide/01_browsedata_parset.png"><img src="/assets/images/introguide/01_browsedata_parset.png"></a>

The graph can also be viewed for different metrics, click **Converts** above it to see the dropdown list.

So this page is a window into the TikTok Integration data. The data here is exactly the same as the data source has, nothing is being changed upon the data collection. 

On this page you can [browse data](../browsing/browse_data.html){: .demolink} for different date ranges, by various breakdowns. You can also filter it using the [query filter](../ui/queryfilters.html){: .demolink} above or simply clicking the values you wish to filter the data by.

>**THE SECOND DATA SOURCE**<br>
To transfer the data from your second data source - Facebook - go through **steps 2-5** once again, but building up a Facebook Integration this time.

Once you're done, you'll have two Integrations with data in them that can and will be transformed and merged into one good report. 

## 6. Merge the collected data into a Merge Report

At this step you have two Integrations with the exact same data as the data sources have. You can browse it on their own [**Browse data**](../ui/integrations/browsedata.html){: .demolink} pages and you can merge it into one good report, transforming it the way you need.

Let's say, you need to have your **Spend** displayed to you and it's calculated as ***Installs * 2***. So you need to have the data on installs from both data sources in one place and apply a calculation formula to those numbers to have your **Spend**. That's exactly the basic thing that can be done in our Merge Report.

Here we will go through a process of building a Merge Module Integration's data transformation flow that will provide us with the desired result. We will not get too much into details though as our main goal now is to show you the basic steps.

&#8505;&nbsp;&nbsp;**Info:**<br>
More in-depth description of this process is given in [**Build a merging data flow**](../workflow/merge/create_mm_integration.html){: .demolink} article.
{: .notice--info}

So, let's start. To create a consolidated report, go to [**Integrations**](../ui/integrations/integrations_main.html){: .demolink} click **NEW INTEGRATION** and select **Merge Module**. 

Next, we'll have to build the data transformation flow.<br>

### 6.1. Data inputs

Drag&drop two [**Input Integration**](../mm/comp_inputintegration.html){: .demolink} components on the workplace. Double click on one of them to open its settings. You might want to rename it to `facebook`. In the integrations selector, find and click the Facebook Integration that you have. Next, select the data that you want to have collected into this new Integration and set the parameters that must be applied to it (timezone, filters, etc) while it's being transferred.<br>
Let's say, we need the dates, campaign names, and the data on clicks and installs to calculate the spend with. <br>

The working area and component's settings will look like this:

<a href="/assets/images/introguide/01_mm_01.png"><img src="/assets/images/introguide/01_mm_01.png"></a>

Now add another [**Input Integration**](../mm/comp_inputintegration.html){: .demolink} component, select the second Integration for it and set it up the same way. We suggest naming it `tiktok`.

When you're done, you will have this in front of you:

<a href="/assets/images/introguide/01_mm_02.png"><img src="/assets/images/introguide/01_mm_02.png"></a>

The two Integrations that you have are now added to the data flow diagram as data inputs. When the Merge Module runs, it will take the Integrations' data and transform it in accordance with the data flow that you will create next.

### 6.2. Merging data

But look at the technical names of those data columns in our data sources:

| Facebook | TikTok |
| --- | --- |
| `date` | `date` |
| `campaign` | `cmp` |
| `installs` | `converts` |
| `clicks` | `clicks` |

&#x261D; **Important!**<br>
The data in matching columns (`clicks` and `clicks`) can be merged, whereas the data stored in the mismatching columns (`campaign` and `cmp`) cannot be merged. <br>
See more info in [the corresponding part](../workflow/merge/create_mm_integration.html#5-merge-the-data-tables){: .demolink} of "Build a merging data flow" article.
{: .notice--warning}

What can we do now? Right, simply rename the columns. To do that, put the [**Rename**](../mm/comp_rename.html){: .demolink} component on the diagram, link it to the inputs and set the renaming rules: column's old name to column's new name. The goal is to put same data into one column. You can use any column name, we suggest setting the component this way:

```json
{
  "map": {
    "cmp": "campaign",
    "converts": "installs"
  }
}
```

This will be the picture:

<a href="/assets/images/introguide/01_mm_03.png"><img src="/assets/images/introguide/01_mm_03.png"></a>

At the end of this step your Merge Module knows how to create one good data table out of the two original ones.

### 6.3. Setting the calculations

Let's get to the Spend metrics that we need to calculate. Place the [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} component on the diagram and link it to the [**Rename**](../mm/comp_rename.html){: .demolink} one. <br>
This component can calculate the data you need (filters available) the way you want (using the expressions). For this basic scenario we just need it to calculate the `installs*2` expression. To do that you can either put this into its code:

```json
{
  "formulaField": "field_to_put_formula_not_required",
  "formulaDefault": "N/A",
  "targetField": "spend",
  "defaultToPort": false,
  "map": [
    {
      "expression": "installs*2"
    }
  ],
  "replace": false,
  "skipIfExists": true
}
```

or set it yourself in the [Arithmetics Visual editor](../ui/arithmetics_visual_editor.html){: .demolink}. Hint: putting the prepared code would be faster at this point :).

&#x261D; **Important!**<br>
Note the `"targetField": "spend",` line in the code above. It means that the component will put the calculations result into the `spend` column that doesn't exist in our data table yet. We are to add it a bit later.
{: .notice--warning}

After setting up your [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} component, you will have this:

<a href="/assets/images/introguide/01_mm_04.png"><img src="/assets/images/introguide/01_mm_04.png"></a>

Your Merge Module knows how to create a data table and calculate the metric for you. 

### 6.4. Data output

Now let your Merge Module give you the results. Just place the [**Output**](../mm/comp_output.html){: .demolink} component on the diagram and link it to the [**Arithmetics**](../mm/comp_arithmetics.html){: .demolink} one.

Here's your finished data flow:

<a href="/assets/images/introguide/01_mm_05.png"><img src="/assets/images/introguide/01_mm_05.png"></a>

Once the Merge Module is run, having this data transformation flow it will collect data from Facebook and TikTok Integrations, transform it (rename the columns) and save into one data table for further visualizing.

### 6.5. List the columns

Before getting to this Merge Module's first run, we have one more thing to set up.<br>
And we'll have to dig a bit deeper into the Merge Module's JSON code. Please click the **JSON** button to access it.

<a href="/assets/images/introguide/01_mm_json.png"><img src="/assets/images/introguide/01_mm_json.png"></a>

You will see the Merge Module's JSON-code. Replace the lines **5-13** with this:

```json
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
      "key": "clicks",
      "title": "Clicks",
      "type": "absolute"
    },
    {
      "key": "installs",
      "title": "Installs",
      "type": "absolute"
    },
    {
      "key": "spend",
      "title": "Spend",
      "type": "absolute"
    }
  ],
  ```

This step is required to let the Merge Module know which columns to display on its [**Browse data**](../ui/integrations/browsedata.html){: .demolink} page and also what attributes those [statistics data fields](../base/entities_metrics.html){: .demolink} have.

Next, click the **SAVE ALL THE TIME** button to save all the changes:

<a href="/assets/images/introguide/01_mm_savejson.png"><img src="/assets/images/introguide/01_mm_savejson.png"></a>

&#8505;&nbsp;&nbsp;**Info:**<br>
The button saying **ALL THE TIME** means that this config is **always relevant**.<br> 
If you need to calculate your **Spend** as ***Installs * 2*** for *Jan 1 - Jan 15* and as ***Installs * 20*** for *Jan 16 - Jan 31*, another basic feature of our Merge Module will help you with this, please find more about it here: [Date range relevances](../ui/relevances.html){: .demolink}.
{: .notice--info}

Now your Merge Module can take, transform and save the data. To do any of that, its [status](../ui/integrations/integrations_main.html#status){: .demolink} must be **Running**, whereas currently its **Initialized**. Let's run the module. 

### 6.6. Run the module

To run your Merge Module, you have to [change its status](../ui/integrations/integrations_main.html#how-to-change-the-integrations-status){: .demolink}. To do that, open its settings by clicking the gear icon and click **RUN** in the [settings sidebar](../ui/integrations/integrations_main.html#settings){: .demolink} and then **YES, RUN** to confirm your action.

<a href="/assets/images/introguide/01_mm_run.png"><img src="/assets/images/introguide/01_mm_run.png"></a>

The module is running now and you can work with data. Let's try collecting it from the source Integrations, transform and save.

## 7. Transform the data

To collect, transform and save the data, you have to run the Integration task on your newly set Merge Module Integration. To do that, go to the [**Tasks**](../ui/integrations/schedule_n_tasks.html#tasks){: .demolink} page:

<a href="/assets/images/introguide/01_mm_tasks.png"><img src="/assets/images/introguide/01_mm_tasks.png"></a>

On this page, click **RUN MANUALLY**, and set the following task parameters:

- **Task:** Statistics Range
- **From - To:** Jan 1 - Jan 31, 2021 

This is what it will look like:

<a href="/assets/images/introguide/01_mm_06.png"><img src="/assets/images/introguide/01_mm_06.png"></a>

After setting them, click **RUN**.

The [task run log screen](../ui/integrations/schedule_n_tasks.html#log-view){: .demolink} will appear. Wait till the status says **STOPPED** and log shows an **Executed successfully** confirmation.

<a href="/assets/images/introguide/01_mm_06-stopped.png"><img src="/assets/images/introguide/01_mm_06-stopped.png"></a>

At this point, the Merge Module has collected, transformed and saved the data. Now you can check the result by browsing the transformed data just the way you browsed the collected one.

## 8. Browse the transformed data

To browse the transformed data, go to [**Browse data**](../ui/integrations/browsedata.html){: .demolink} page and browse the consolidated report's data. All the data browsing features available on the source Integrations [**Browse data**](../ui/integrations/browsedata.html){: .demolink} pages are also available here.

<a href="/assets/images/introguide/01_mm_browsedata.png"><img src="/assets/images/introguide/01_mm_browsedata.png"></a>

Set the [date range](../ui/integrations/browsedata.html#date-range-picker){: .demolink} to *Jan 1 - Jan 31, 2021*, then select the breakdowns: click **DATE**, tick the **CAMPAIGN** breakdown and also the **APPLY** button.<br>
Take a look at the data table. The **Spend** column's values are exactly the **Installs** * 2.<br>

Now that you have the metric calculated, let's move on to visualizing it.
 
## 9. Visualize the Merge Report data on a Dashboard

You can of course leave it like that and always open the [**Browse data**](../ui/integrations/browsedata.html){: .demolink} page itself once you need the info and look at the numbers carefully. But it is much more useful to visualize it via various widgets on your Dashboard.

Let's imagine that you have two goals: 
1. Find out how your Spend is changing with time.
2. See which campaigns have the Spend over 500 and below 700 in Germany.

### How is the Spend changing?

To reach the first goal, go to the [**Dashboards**](../ui/dashboards/dashboards_main.html){: .demolink} section, create a new Dashboards clicking **NEW DASHBOARD** and [rename](../ui/dashboards/dashboards_main.html#--rename-dashboard){: .demolink} it to My Dashboard. On your new Dashboard, click [**ADD WIDGET**](../ui/dashboards/dashboards_main.html#add-new-widget){: .demolink} and select [**Chart**](../visualization/chart.html){: .demolink}.

&#8505;&nbsp;&nbsp;**Info:**<br>
In two words, with the [**Chart**](../visualization/chart.html){: .demolink} widget you can create a pie chat, a bar chart or a line chart to visualize your metrics. With the [**Datagrid**](../visualization/datagrid.html){: .demolink} widget, you can, for example, highlight table cells depending on the values, tracking the changes of your metric.
{: .notice--info}

Once it is added, you will see [its settings](../ui/dashboards/dashboards_main.html#add-new-widget){: .demolink} on the left with only the Integrations selector available for now.<br>
First, [rename](../ui/dashboards/dashboards_main.html#rename-widget){: .demolink} the Chart to **January'21 Spend**. Next, click the selector and choose your Merge Module Integration.<br>
For the widget with selected Integrations, all the other [widget settings](../ui/dashboards/dashboards_main.html#widget-settings){: .demolink} become available.<br>
Say, you wish to see how your **Spend** changes with time during January, 2021.<br>

First, open the [date range picker](../ui/integrations/browsedata.html#date-range-picker){: .demolink} and select the *Jan 1 - Jan 31, 2021* date range.<br>
Then, in the **Breakdowns & Metrics** area with green and blue rectangles, drag&drop the green **Spend** one to the right column, it will appear under **Metrics**. This way you're selecting it for viewing in your widget. 

<img src="/assets/images/introguide/dndmetric.gif">

Next, drag&drop the other metric to the left to remove it from your widget and make sure the selected **Breakdown** is **Date**.

&#8505;&nbsp;&nbsp;**Info:**<br>
Green and blue rectangles represent `entities` and `metrics` data columns, find full info about those here: [Entities & metrics](../base/entities_metrics.html){: .demolink}.
{: .notice--info}

Click **APPLY** to save the changes. This is what you will see at this step:

<a href="/assets/images/introguide/01_mm_07.png"><img src="/assets/images/introguide/01_mm_07.png"></a>

There you go! That's your Spend metric changing with time. <br>

### How are the campaigns doing in China?

The next goal is to check out which campaigns in China have the Spend over 3400 and below 2500. 

Before we start, imagine that the campaign names have `de`, `en` and `cn` tags in them marking the countries.

>&#8505;&nbsp;&nbsp;**Note:**<br>
The tags can be different consisting of any other symbols and meaning something else.

To reach our goal, [add](../ui/dashboards/dashboards_main.html#add-new-widget){: .demolink} the [**Datagrid**](../visualization/datagrid.html){: .demolink} widget to your Dashboard and, just like for the [**Chart**](../visualization/chart.html){: .demolink} widget previously and let's [call this one](../ui/dashboards/dashboards_main.html#rename-widget){: .demolink} **Campaigns**. Click the Integrations selector and choose your Merge Module Integration.<br>
Same goes for the date range: *1 - Jan 31, 2021* in the [date range picker](../ui/integrations/browsedata.html#date-range-picker){: .demolink} . As for the **Breakdowns & Metrics** area, since we want to see the data on spend by campaigns, drag&drop the **Spend** and **Campaign** rectangles to the right column and any other rectangles that might be in that column - to the left one. This in what the settings should look like:

<a href="/assets/images/introguide/01_mm_dgsettings.png"><img src="/assets/images/introguide/01_mm_dgsettings.png"></a>

Click **APPLY**.<br>
The data table will appear in the widget, containing both columns that you selected. 

<a href="/assets/images/introguide/01_mm_08.png"><img src="/assets/images/introguide/01_mm_08.png"></a>

<br><br>
Now let's work with that data. In the widget settings, double click the **Spend** rectangle to open the metric's settings.<br>
In the **Spend** settings window, fins **Conditional format** section and click **ADD RULE**. <br>
For the first rule, select **Less than** and set **2500**. Then add the second rule as **Greater than** and **3400**. Don't forget to assign them distinct colours.

<a href="/assets/images/introguide/01_mm_metrset.png"><img src="/assets/images/introguide/01_mm_metrset.png"></a>

Click **OK** and then click **APPLY** to apply the changes to your widget.

Data table cells with the corresponding values will be highlighted. Now you know which campaigns are spending too much and which ones - too little, just at a glance:

<a href="/assets/images/introguide/01_mm_09.png"><img src="/assets/images/introguide/01_mm_09.png"></a>

And on top of that, let's only keep the campaigns run in China. Query filter and the `cn` and `CN` tags will help us with it: click the **Filter query** field, select **Campaign** from the dropdown list, than select the **middle of the line matches** option and enter `cn`. To take into account the `CN` tag, too, click the field again and select **or**, then repeat the previous actions but for the `CN` tag. Here's what the filter query will be like: `Campaign = *cn* or Campaign = *CN*`. After setting it, click **APPLY**. The data table will change to the following:

<a href="/assets/images/introguide/01_mm_10.png"><img src="/assets/images/introguide/01_mm_10.png"></a>

Feel free to close the widget's settings (cross icon in its upper right corner).

 Now in this widget you have your overall spend from Facebook and TikTok filtered by the amount of money and displayed for a certain country. 

And this is the very basic scenario that JustControl.it covers, we haven't even gotten to the proper use of those naming tags and KPI metric creation etc. See the **Workflow in details** menu section on your left for more info. 

## 10. Something to share

Since we are getting to know the product closer, let's take one more step forward and prepare something for the next round.

Imagine that you need to share that info on how the campaigns are doing in Germany with an employee or a business partner of yours. **Just that info, nothing more.** <br>
In two words, to do that you simply create a Dashboard with that widget only, then add a JC.it user for that person and share the Dashboard with that user.

As a preparation here we'll create that Dashboard and place the widget on it. 

First, copy the [**Datagrid**](../visualization/datagrid.html){: .demolink} widget by clicking **Copy Widget** in the [More actions button](../ui/dashboards/dashboards_main.html#page-overview){: .demolink} menu.

<img src="/assets/images/introguide/01_sh_01.png"></a>

<br>

Next, [create a new dashboard](../ui/dashboards/dashboards_main.html#create-new-dashboard){: .demolink} by clicking the **NEW DASHBOARD** button and [rename](../ui/dashboards/dashboards_main.html#--rename-dashboard){: .demolink} it to **Shared dashboard**. Then click [**ADD WIDGET**](../ui/dashboards/dashboards_main.html#add-new-widget){: .demolink} and [add the **Campaigns** widget you have copied](../ui/dashboards/dashboards_main.html#add-new-widget){: .demolink} to your new dashboard.

Now you have two dashboards:

<a href="/assets/images/introguide/01_sh_02.png"><img src="/assets/images/introguide/01_sh_02.png"></a>

The new one can be shared to another person showing them only the info on campaigns' spend in Germany. We'll get to it in the [Adding users and giving permission](usersroles.html){: .demolink} article.