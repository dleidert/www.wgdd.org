---
lang: en
title: 'Jekyll and GitHub pages: access the download URL (aka browser_download_url)
  for an asset of your latest release via site.github'
description: >-
  This article describes how to access download URL (aka browser_download_url)
  for an asset of your latest release via site.github'. It can be used to
  create a download to the latest release without having to replace the URL
  when it changes. Instead rebuilding the site will find the correct link.
date: '2019-02-24T17:00:00.002+01:00'
category:
- software
- planet-debian
tags:
- foss
- english
- hosting
- software
- liquid
- planet-debian
- git
- github pages
- jekyll
- github
redirect_from:
- /2019/02/jekyll-and-github-pages-access-download.html
---

## Add the download URL of an asset of your latest release

Often there is the question to get the download URL for an asset (e.g. a setup-file) of the latest release of a project. In my case I provide an executable, which includes the version number in its name together with the source as ZIP- and Tarball-archive. Others provide versioned source tarballs or executables, which are different from the Git repository source tarballs.

```data
project-X.Y.Z-setup.exe
project-X.Y.Z-src.tar.gz
```

Now to get the download URL(s) for the asset(s) using the [GitHub API]
one can get and process this URL (replacing <var>USER</var> and
<var>PROJECT</var> with the GitHub user account and projectname accordingly):

[GitHub API]: https://developer.github.com/v3/

> [https://api.github.com/repos/USER/PROJECT/releases/latest](https://developer.github.com/v3/repos/releases/#get-the-latest-release)

Note, that the assets download URL is provided by the <code>browser\_download\_url</code> object in the <code>assets</code> objects list:

```json
{
  ...
  "assets": [
    {
      ...
      "browser_download_url": "...",
      ...
    }
  ]
}
```
{: title="assets object of the browser_download_url object"}

The content provided by the API is **also** available to [Jekyll sites] hosted
as [GitHub pages] via the [<code>site.github</code>][site.github] namespace. You can easily
check all the content of this namespace using this approach (somewhere in your
code):

[Jekyll sites]: https://jekyllrb.com/
[GitHub pages]: https://pages.github.com/
[site.github]: https://help.github.com/en/articles/repository-metadata-on-github-pages

```markup
{{ "{{" }} site.github | inspect }}
```

You'll find, that you can even access detailed author and project information
this way. Now to get the download URL of my asset I just access the first list
entry using this expression:

```markup
{{ "{{" }} site.github.latest_release.assets[0].browser_download_url }}
```

or this approach (less typing):

```markup
{{ "{%" }} assign release = site.github.latest_release %}
{{ "{{" }} release.assets[0].browser_download_url }}
```

I use this to create structured data in [JSON-LD] for a software application. I
can even access the file size, the creation and publication date of my asset.
The following shows the [JSON-LD snippet] I add to one of my GitHub project
pages (I replaced fixed content with dots):

[JSON-LD]: https://json-ld.org
[JSON-LD snippet]: https://raw.githubusercontent.com/dleidert/bde-lock/master/docs/_includes/json/softwareapplication.json

```json
{% assign release = site.github.latest_release %}
{
  "@context": "http://schema.org/",
  "@type": "SoftwareApplication",
  "name": "...",
  "softwareVersion": "{{ release.tag_name | strip | remove: 'v' }}",
  "alternateName": [
    "...",
    "{{ release.name }}"
  ],
  "description": "...",
  "applicationCategory": "...",
  "inLanguage": ["..", ".."],
  "operatingSystem": [
    "...",
    "..."
  ],
  "downloadUrl": "{{ release.assets[0].browser_download_url }}",
  "fileSize": "{{ release.assets[0].size | divided_by: 1024 }}",
  "releaseNotes": "{{ release.html_url }}",
  "license": "...",
  "url": "{{ site.github.repository_url }}",
  "datePublished": "{{ release.published_at }}",
  "dateCreated": "{{ release.created_at }}",
  "author":    {{ "{%-" }} include json/person.json -%},
  "publisher": {{ "{%-" }} include json/publisher.json -%}
}
```

If there is more than one asset (the GitHub repository source tarball and
zipball are not assets) one probably has to use a more flexibale approach then
accessing the first list entry via <code>asset[0]</code> as shown above. If
there are several assets and the asset file name is created the same way for
every release but includes the version number (see the file name examples from
the beginning of this post), there is another approach, that might be to used.
One can process:

```markup
{{ "{{" }} site.github.latest_release.tag_name }}
```

and create the download URL like this

```markup
{{ "{{" }} site.github.releases_url }}/download/latest/foo-{{ "{{" }} site.github.latest_release.tag_name | strip | remove 'v' }}-setup.exe
{{ "{{" }} site.github.releases_url }}/download/latest/foo-{{ "{{" }} site.github.latest_release.tag_name | strip | remove 'v' }}-src.tar.gz
```

Because it is common to tag the version as <code>vX.Y.Z</code> the leading
<code>v</code> is removed from the version tag in the examples above.

Using the approach above one can even loop over
<code>site.github.releaes</code> and create a changelog/news page automatically
for all releases! Maybe you can share <strong>your ideas</strong> about the
suggested approaches on [my GIST page].

[my GIST page]: https://gist.github.com/dleidert/99a8e6ee3a879a7ed1f160c5dd07c13d

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
