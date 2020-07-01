---
title: Keeping up to date with scientific publications using RSS feeds
author: ''
date: '2020-04-20'
slug: keeping-up-to-date-with-scientific-publications-using-rss-feeds
categories:
  - Tutorial
tags:
  - Academia
  - Science
  - RSS
  - Research
  - Project Management
subtitle: ''
summary: ''
authors: []
lastmod: ''
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

Keeping up to date with scientific publications is no easy task. There are [millions](https://www.stm-assoc.org/about-the-industry/stm-report-2015-2/) of peer-reviewed scientific papers published each year, along with a [continuously growing](https://elifesciences.org/articles/45133) number of preprints. For most scientists, the vast majority of these publications have no bearing on their work---they're essentially spam---and filtering through them manually is like slaying an Academian Hydra. For every irrelevant paper crossed off, two more irrelevant papers are published in its place! But in the age of computers, technologies exist that can slay the Hydra: Enter [RSS feeds](https://en.wikipedia.org/wiki/RSS).

## What is RSS?

RSS (Really Simple Syndication) is a web feed that can be used to keep track of updates to many different websites and deliver them to you in a standardized format. This post focuses on newly published scientific papers from peer-reviewed journals, but RSS feeds can be used with any website that offers RSS. RSS feeds can also be filtered, blacklisting or whitelisting content based on certain keywords, which is incredibly useful for removing irrelevant papers from a feed.

## Using RSS

In order to use RSS you only need two things: The *RSS links* for the websites you would like to keep track of and an *RSS reader* to read them.

For RSS readers, I like to use [Feedly](https://feedly.com) ([iOS](https://apps.apple.com/ca/app/feedly-classic/id1440918660), [Android](https://play.google.com/store/apps/details?id=com.devhd.feedly.classic&hl=en_CA)) or the RSS app in [Slack](https://slack.com), depending on the purpose of my feed. I use Feedly as a private catch-all for content from news sites, guitar magazines, art publications, *and* scientific journals. And I use the RSS app in Slack to publicly share updates to scientific journals or [my group Zotero collections](/post/integrating-slack-and-zotero-with-rss) with others in my Slack workspace. Separating my personal and professional feeds like this is helpful, as it minimizes clutter and lets me keep my interests and work independent of one another. I recommend you do something like this too if you plan to use RSS feeds for personal and professional purposes.

For RSS links, you can use your RSS reader's built-in search function if it has one (Feedly does, the RSS app in Slack does not). This makes adding RSS links to the reader as simple as searching for a scientific journal in the search bar and clicking the follow button to add it to your feed. If the search function does not garner any results, you can search for an RSS link on the website you want a feed from. Most websites---including this one, [Nature Neuroscience](https://www.nature.com/neuro/), and [Memory](https://www.tandfonline.com/toc/pmem20/current)---will place a clickable RSS icon (<i class='fas fa-rss-square pl-1 pr-1' style='color:rgb(255, 153, 51);'></i>) somewhere on the homepage, whose link you can copy into your preferred RSS reader.

When adding RSS links to your reader, it's good practice to group RSS links of similar topics into the same feed, category, or channel so you can stay organized.

{{% alert note %}}
Some websites may not provide RSS, in which case you will need to use a third-party RSS Generator to convert a web page to an RSS feed. Feedly does this automatically when you use its search function.
{{% /alert %}}

## Filtering an RSS feed

If there are journals you want to follow, but only want to see specific types of articles from them, you can filter their RSS links by a keyword. To do this you will need to use a third-party RSS generator that has a filtering function. [siftrss](https://siftrss.com) is a free option that can blacklist or whitelist journal articles by a keyword in their title or description. If you want to filter the same journal by multiple keywords you will need to generate multiple RSS links using different filtering criteria each time.

{{% alert note %}}
Always make sure the filters are working as intended and that you did not make a typo or select the wrong option while generating them, otherwise your RSS feed will likely be empty for eternity.
{{% /alert %}}

## Troubleshooting an RSS feed

If you stop receiving new content from one of the RSS feeds you've subscribed to, it is likely that the RSS feed's link has been changed or the website has stopped providing RSS. You can easily check this by repeating the steps above and seeing if resubscribing to the feed fixes the problem. Most of the time it should. If it doesn't you can try inputting the RSS link into an [RSS validator](https://validator.w3.org/feed/) to see if it is a valid RSS link.
