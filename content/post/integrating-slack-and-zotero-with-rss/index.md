---
title: Integrating Slack and Zotero with RSS
author: ''
date: '2020-02-11'
slug: integrating-slack-and-zotero-with-rss
categories: [Tutorial]
tags:
  - Slack
  - Zotero
  - RSS
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

Want to keep your collaborators up-to-date with your project's reference collection? Want to know when your collaborators have a new paper you should read? Want to automate this process? If you answered yes to all these questions then you might find the following tutorial helpful. This tutorial assumes you are already using [Slack](https://slack.com) and [Zotero](https://www.zotero.org) within your organization, but does not require any technical expertise beyond that.

## Step 1: Create a private Zotero API key

```html
https://www.zotero.org/settings/keys/edit/[[KEY CODE WILL BE HERE]]
```

First log into Zotero in your browser, then go to [settings](https://www.zotero.org/settings/) and open the [Feeds/API](https://www.zotero.org/settings/keys) tab. From there you should:

- Click the [create a new private key](https://www.zotero.org/settings/keys/new) link.
- Name the key (e.g., Slack RSS).
- Choose the permissions you want to give the key (or stick with the default permissions).
- Save the key.

Copy the key code down somewhere---you’ll need it later to create the URL for your RSS feed. If you click *edit key* and then look at the URL on the edit key page, the key code will be the long character string at the end.

## Step 2: Find your group’s Zotero library identifier number

```html
https://www.zotero.org/groups/[[GROUP LIBRARY IDENTIFIER NUMBER WILL BE HERE]]/group_name/library
```

Staying on the Zotero website, go to the [Groups](https://www.zotero.org/groups/) tab and open your group's *Group Library*. Look at the URL on that page and copy the group identifier number down somewhere.

## Step 3: Find your Zotero collection's identifier code

```html
https://www.zotero.org/groups/group_number/group_name/collections/[[COLLECTION CODE WILL BE HERE]]
```

From your Group Library, click on the collection in the left-hand pane that you want to create a feed for. After clicking on the collection look at the URL on that page and copy the collection's identifier code down somewhere.

## Step 4: Create an RSS URL for your group's Zotero collection

```html
https://api.zotero.org/groups/[[GROUP NUMBER]]/collections/[[COLLECTION CODE]]/items/top?start=0&limit=25&format=atom&content=bib&style=apa&v=3&key=[[API KEY]]
```

Copy the URL above into your favourite text editor, filling the strings you copied in Steps 1-3 into their appropriate place in the URL. Make sure to remove the square brackets; I just put them there so it’s easier to see where you should paste your strings.

{{% alert note %}}
1. The RSS URL you create here will also work in other RSS readers such as [Feedly](https://feedly.com/i/welcome).
2. If you want to create RSS feeds for other collections in your group's Zotero library you only need to change the URL's collection code. The group number and API key can stay the same.
{{% /alert %}}

## Step 5: Add the RSS app to your Slack workspace

Go to your group's Slack workspace and add the RSS app if you have not already. After adding the app, open it by clicking *View app in Directory.* From here you can copy and paste the URL you made in Step 4 into the *Feed URL* and select the channel you want to have new items from your group's Zotero collection posted in. 

{{% alert note %}}
1. New items are fetched periodically so they might not be posted instantly. There is usually a 10-30 minute delay.
2. You can have multiple Zotero collections post to a single Slack channel by creating multiple RSS feeds and having them all post to the same channel. This is useful if, for example, you have collections for Methods and Theory that you wish to keep seperate, but are still using them for the same project.
3. If you do not want the posts to be made in APA style just change the `style=apa` string in your RSS URL to your preferred style. A list of available styles can be found [here](https://www.zotero.org/styles/).
{{% /alert %}}

## Step 6: Sit back and relax

You’re done! When new items are added to the relevant Zotero collection they will be posted to the respective Slack channel in APA format. Simply repeat the process if you want other Zotero collections posting to any of your Slack channels.
