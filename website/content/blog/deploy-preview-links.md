---
title: Deploy Preview Links in Netlify CMS 2.4.0
author: Shawn Erquhart
description: >-
  Deploy preview links from your GitHub repository are now surfaced in Netlify
  CMS for previewing builds of unpublished content.
date: 2019-01-28T19:30:00.000Z
twitter_image: /img/preview-link-unpublished.png
---

![Deploy preview link for unpublished content](/img/preview-link-unpublished.png)

Content editors need a way to see how content will look in production. The preview pane in Netlify
CMS is a good tool for this, but in the words of Marvin Gaye, "ain't nothing like the real thing!"
As Mr. Gaye bemoaned being unable to interact with a picture of his beloved, so content
creators long for the warm embrace of a deployed build.

Or something like that.

JAMstack platforms provide solutions for this, such as Netlify's Deploy Previews, but there hasn't
been a way to access links to these preview builds from within Netlify CMS.

## Solution: Statuses

![GitHub statuses](/img/github-statuses-deploy-previews.png)

Many static sites already have continuous deployment and deploy previews configured on their repo,
and they often use statuses to provide a link to a deployment directly from a commit or pull
request. To retrieve a commit status that provides a deploy preview URL, we check for a status whose
"context" contains one of a list of keywords commonly associated with deploy previews.

If a status is not found, nothing happens in the UI. If a status is found, but the deploy preview
isn't ready, we provide a "Check for Preview" link, allowing the content editor to manually check
back until the preview is ready:

![Deploy preview link for unpublished content](/img/preview-link-check.png)

When the preview is ready, the "Check for Preview" button is replaced with a link to the content:

![Deploy preview link for unpublished content](/img/preview-link-unpublished.png)

## Deep links

Deploy preview links generally direct to the root of a site, but Netlify CMS provides a method for
deep linking, so deploy preview links navigate straight to the piece of content being edited. By
[providing a string template](/docs/deploy-preview-links) for each collection, you can get links
that go right where editors expect them to.

## Unpublished vs. published
If you're not using the editorial workflow, you may not feel you need this very much. Whenever you
save content, it's immediatlely published, so you can navigate to your live site to see the changes.
That said, it's at least convenient to have a link direct to your content from the CMS, so deploy
preview links can also work for CMS installs that do not use the editorial workflow. Instead of
retrieving a URL from a commit status, this functionality requires setting a `site_url` in your
config, and that URL is used in place of the deploy preview URL.

## Try it out!
Deploy preview links are live in Netlify CMS 2.4.0. Please give them a try and let us know if you
have any problems by [opening an issue](https://github.com/netlify/netlify-cms/issues/new) or
reaching out in our [community chat on Gitter](https://gitter.im/netlify/netlifycms)!