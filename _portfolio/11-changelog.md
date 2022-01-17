---
layout: single
title: "Changelog post"
excerpt: "One of the regular changelog updates"
header:
  teaser: /assets/images/teasers/changelog.png
toc: true
toc_sticky: true
---

<div class="usecase">

  <br>
  <strong>USE CASE</strong> <br><br>

  <strong>Problem</strong><br>
  The platform needed a changelog that would let the customers know about its recent updates and new features.<br><br>
  
  <strong>Solution</strong><br>
  In cooperation with DevOps engineer and developer teams leads, a changelog channel was launched and kept going. Each post consisted of a summary (that was also posted to the Telegram channel) and a detailed list of updates.<br> 
  The summary was telling about how exactly the updates were changing the current workfow for platform users, and the updates list was just going through them one by one. Both parts had links to the relevant pages of product documentation (updated with the new info prior to the changelog post being out).<br>
  See the <em>Ver 1.26: a fresh new look and handy tools...</em> post text on this page.<br><br>
  <a href="/assets/images/changelogview.png"><img class="align-center dropshadow" src="/assets/images/changelogview.png"></a>
  &nbsp;

</div>

## Summary 

Hello! 

It’s been a while since we last updated you on our new features, so here we are with a couple of very pretty updates.<br>

You will surely find the <a class="demolink" href="">Integrations</a>, <a class="demolink" href="">Auth Connectors</a>, <a class="demolink" href="">Schedules</a> and <a class="demolink" href="">Macros</a> pages looking much nicer now that they have useful filters and list sorting options. For some of those pages, list items are also grouped by the relevant Integrations which makes it easier to get a whole picture of that section for your account. The <a class="demolink" href="">Macros</a> page now has an automated filter that basically does the job of categorizing your macros for you. See other key points via the link
below.<br>

Creating a new Integration flow was redesigned, too.<br>

Aside from our interface, we have new **Voluum** and **Apple Search Ads** source modules. We also keep improving our Merge Module and this time we got rid of a couple of memory and data amount related issues.<br>

See further details below.

<hr>

## Highlights

1.&nbsp;**UI. Lists.** On the <a class="demolink" href="">Integrations</a>, <a class="demolink" href="">Auth Connectors</a>, <a class="demolink" href="">Schedules</a> and <a class="demolink" href="">Macros</a>  pages, the lists were redesigned and enhanced significantly with filters.<br>

Key points:
- In general, all those pages now have the list managing options on their left and viewing options like search, sort and refresh at their top.<br>
    <a href="/assets/images/changelog/01.png"><img src="../../assets/images/changelog/01.png"></a><br>
- Each item of those lists contains both its info (on the left: name, ID, etc) and managing tools (on the right: settings, links, descriptions, etc).<br>
    <a href="/assets/images/changelog/02.png"><img src="../../assets/images/changelog/02.png"></a><br>
- On the <a class="demolink" href="">Integrations</a>, <a class="demolink" href="">Auth Connectors</a> and <a class="demolink" href="">Schedules</a> pages, list items are now also grouped by the relevant Integrations.<br>
    <a href="/assets/images/changelog/03.png"><img src="../../assets/images/changelog/03.png"></a><br>
- The filter on <a class="demolink" href="">Macros</a> page basically does the job for you creating a separate filtered list for each word that’s been used in 3+ macro titles.<br>
    <a href="/assets/images/changelog/04.png"><img src="../../assets/images/changelog/04.png"></a><br>

2.&nbsp;**UI. Integrations.** New Integration menu was redesigned into a nice and handy list with a search field. Next step of this flow allows you to set the Integration name and visibility.

&nbsp;&nbsp;&nbsp;<a href="/assets/images/changelog/05.png"><img src="../../assets/images/changelog/05.png"></a>

3.&nbsp;**Modules.** **Voluum** and **Apple Search Ads** modules are now available to connect.

## Other updates

1.&nbsp;**Modules. Merge Module.**<br>
  - The stability of processing bigger amounts of data was increased.
  - The issue of multiple Arithmetics components affecting the module performance was fixed.<br>
  
2.&nbsp;**Modules. Google Ads.** A new option of collecting stats for all the available client accounts is now the default one.<br>
3.&nbsp;**Modules. Facebook.** API v12.0 is supported.