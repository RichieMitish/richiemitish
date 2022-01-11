---
layout: single
title: "Ver 1.26: a fresh new look and handy tools for our lists, new source modules and more Merge Module improvements"
excerpt: "One of the regular changelog updates"
header:
  teaser: /assets/images/teasers/changelog2.png
toc: true
toc_sticky: true
---

<!--
sidebar:
  - title: "Use case"
    text: "New customers and employees intro guide"
-->

>**Use case**<br>
>New customers and employees intro guide
{: .notice--danger}

## Summary 

Hello! 

It’s been a while since we last updated you on our new features, so here we are with a couple of very pretty updates.<br>

You will surely find the <a href="">Integrations</a>, <a href="">Auth Connectors</a>, <a href="">Schedules</a> and <a href="">Macros</a> pages looking much nicer now that they have useful filters and list sorting options. For some of those pages, list items are also grouped by the relevant Integrations which makes it easier to get a whole picture of that section for your account. The <a href="">Macros</a> page now has an automated filter that basically does the job of categorizing your macros for you. See other key points via the link
below.<br>

Creating a new Integration flow was redesigned, too.<br>

Aside from our interface, we have new **Voluum** and **Apple Search Ads** source modules. We also keep improving our Merge Module and this time we got rid of a couple of memory and data amount related issues.<br>

See further details below.

<hr>

## Highlights

1. **UI. Lists.** On the <a href="">Integrations</a>, <a href="">Auth Connectors</a>, <a href="">Schedules</a> and <a href="">Macros</a>  pages, the lists were redesigned and enhanced significantly with filters.

    Key points:
      - In general, all those pages now have the list managing options on their left and viewing options like search, sort and refresh at their top.
        <img src="../../assets/images/changelog2/01.png">
      - Each item of those lists contains both its info (on the left: name, ID, etc) and managing tools (on the right: settings, links, descriptions, etc).
        <img src="../../assets/images/changelog2/02.png">
      - On the <a href="">Integrations</a>, <a href="">Auth Connectors</a> and <a href="">Schedules</a> pages, list items are now also grouped by the relevant Integrations.
        <img src="../../assets/images/changelog2/03.png">
      - The filter on <a href="">Macros</a> page basically does the job for you creating a separate filtered list for each word that’s been used in 3+ macro titles.
        <img src="../../assets/images/changelog2/04.png">

2. **UI. Integrations.** New Integration menu was redesigned into a nice and handy list with a search field. Next step of this flow allows you to set the Integration name and visibility.

    <img src="../../assets/images/changelog2/05.png">

3. **Modules.** **Voluum** and **Apple Search Ads** modules are now available to connect.

## Other updates

1. **Modules. Merge Module.**
  - The stability of processing bigger amounts of data was increased.
  - The issue of multiple Arithmetics components affecting the module performance was fixed.
2. **Modules. Google Ads.** A new option of collecting stats for all the available client accounts
is now the default one.
3. **Modules. Facebook.** API v12.0 is supported.