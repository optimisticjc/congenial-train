---
layout: page
title: Restore Soft Deleted Pages
description: Resolving Pages issues caused by changes in users plan.
author: optimisticjc
last_updated: 2024-03-04
owner_slack: support-docs
owner_team: support-docs
owner_repo: support-docs-content
redirect_from:
  - /docs/support/content/pages/restore-soft-deleted-pages.md
toc: true
---

## Summary

Troubleshooting procedures when Pages users report they are experiencing a `404` or `File Not Found` error. If the page loads, but is blank, incorrect, or doesn't refresh (stale), see that [troubleshooting guide](./troubleshooting-pages-blank.md) instead.

## Debugging in the browser console

You can identify URL discrepancies and missing files through [the browser console](https://developers.google.com/web/tools/chrome-devtools/debug/console/?hl=en).

To find the full URL of the error, right-click on the file name to the right of the error message and then select **Open link in new tab**. Find the corresponding file in the repository and compare.

## Verify the file and filename

1. The file must exist in the repo.
2. The filename must be spelled correctly.
3. File names and URLs are **case-sensitive**.
   - `Index.html` won't show up on the root domain; it must be `index.html`.
   - This applies to all files: `image.jpg` isn’t the same as `image.JPG` and `camelcase.html` isn’t the same as `camelCase.html`.
   - Posts with mixed-case URLs must use the same case in links on the site. A post titled “A Day in the Life” will have the URL `A-Day-in-the-Life`. A link to that post needs to match the capitalization.

If the file doesn't exist, ask that they send you a link to the file in their repo and make sure they have uploaded all of their files to GitHub.

If the file exists with a different name, location, or capitalization, send them a link to the correct location and explain why it's different from what they were trying.

If they are having trouble with mixed-case URLs or filenames, suggest they consider [setting a permalink](https://jekyllrb.com/docs/permalinks/) in the YAML.

## Check for missing index or readme files

Make sure they have an `index.html`, `index.md`, or `README.md` file at the root of their publishing source.

If they put the `index.html` file in a folder, this will still work as long as the YAML front matter includes the permalink parameter `permalink: /`.

Reply with the [Pages / no index Canned Reply](https://github.com/github/zendesk/blob/master/canned-replies/Technical/pages/index/no%20index.md). Add a link to the existing index/README file if you can find one; if not, link to the root of their Pages source instead.

## Verify the location of the Pages site source

Make sure their site is in the right place in the repo. The site location in their repo should match the source in Stafftools. The site must be either in the root or in the `/docs` directory if they have set that as their source. It cannot be in any other subfolder.

## Verify the site build is complete

It can take up to 20 minutes for the site to appear after the initial build, so sometimes users email us before their site finishes building.

1. Open the site.
2. If the site is there, send the [Pages / site loads](https://github.com/github/zendesk/blob/master/canned-replies/Technical/pages/site%20loads.md) canned reply.
3. In your reply, let them know that you can see it, include the link, suggest they clear the browser's cache, and ask if they're able to see it now.

## Verify the site's URL

The URL they're using may not be the correct URL for their site.

Use the [toggle bookmarklet](http://ben.balter.com/pages-toggle-bookmarklet/) or find it in the **Pages** section of Stafftools.

If it's a User Page, is `username.github.io` spelled correctly? Does it match their username exactly?

Users may misunderstand the naming rules. For example, their username is `blah`. The repo name for user or org sites must match their username, so in this case the site's URL would be `https://blah.github.io`. The user assumes they can get the site to show up at `https://othername.github.io` by renaming the repository to `othername.github.io`. This doesn't work as expected; since the repo's name no longer matches the username, the site's actual URL is now `https://blah.github.io/othername.github.io`.

If they're using the wrong URL, let them know the correct one and explain why it's different than the one they were trying.

## Check for custom domain issues

If the user is seeing their own [custom 404 page](https://docs.github.com/github/working-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site), and you have [confirmed](#Check-the-DNS-records) that their domain points to GitHub, you can rule out a custom domain issue. Troubleshoot as a typical "file-not-found" error.

If the user is seeing some other webhost's 404 page, [check the DNS records](#Check-the-DNS-records). It is likely that the settings are incorrect.

If the user is seeing GitHub's 404 page and using a custom domain, the domain may be associated with the wrong repo or no repo at all.

1. Check for a CNAME file in the repo. Go to **Stafftools** > **Repo** > **Pages** or `https://admin.github.com/stafftools/repositories/{OwnerName}/{RepoName}/pages`
2. If they don't have a CNAME file, ask them to [add the domain to the repo settings](https://docs.github.com/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site).
3. If they have a CNAME file, try rebuilding manually. If that doesn't resolve the issue, ask them to remove the CNAME file and re-add the domain through their repo settings.

## Check the DNS records

Use your preferred method of checking the DNS records.

- Use [whatsmydns.net](https://www.whatsmydns.net/). This is the preferred method because the domain is added to the URL, so you can send the link to the user to help prove / explain that their domain isn't set up correctly.
- Use the `dig` command on the command line: `dig <domain>`
- Use the [Alfred workflow](https://app.box.com/s/xjt5fp9rei8ir5ufv0s31wllo5fr2qzk) uploaded by`@shawnajean`. Type `dig <domain>` right into Alfred.

Their A records for the root domain need to point to:

- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

If they have a CNAME record, it needs to point to `username.github.io`. It can not point to `https://username.github.io` or `username.github.io/repo`.

## Check for excluded files

Some files in the repository are automatically excluded from the Pages site build.

### Excluded by Jekyll

Jekyll excludes certain files by default. If they're trying to access a file in the folder `vendor` or `node_modules`, or a file or folder that starts with `_`, `.`, `#` or ends with `~`, Jekyll likely didn't build the file.

This is a great example of where the `.pages ls <domain>` [chatop](#chatops) comes in handy.

### Excluded by Pages

Pages excludes certain meta files by default. The `README`, `CONTRIBUTING` file, `CODE_OF_CONDUCT`, or `LICENSE` files are not inclued in the build unless they include YAML front matter or are explicitly included in the `_config.yml`.

```yml
include:
  - CONTRIBUTING.md
  - README.md
```
