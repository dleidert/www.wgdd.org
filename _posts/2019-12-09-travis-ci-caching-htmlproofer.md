---
title: Fix travis-ci.org not caching htmlproofer
description: >-
  Tests run in the after_success target of a TRAVIS CI job cannot add cached
  output to the jobs cache, because this one gets updated before the target is
  actually run.
category:
- planet-debian
- software
tags:
- jekyll
- travis-ci
- htmlproofer
- ci
---

I build my site using [Jekyll], [GitHub] and [Travis-CI]. I've recently
noticed that whenever [HTMLProofer] runs, it says:

```console
Found 0 links in the cache...
```

I couldn't figure it out right away, but the reason actually is that my
[original design] was to build the site in the `script` target and run the test
in the `after_success` target. Sounds logical, yes? But the cache is updated
**before** the `after_success` target and not after, so the link cache never
gets added to build cache. This is also documented [in the docs].

So to add and upload HTMLProofer's cache I moved the site test into the
`script` target too.

[Jekyll]: https://jekyllrb.com/
[GitHub]: https://github.com/dleidert/www.wgdd.org
[Travis-CI]: https://travis-ci.com/dleidert/www.wgdd.org
[HTMLProofer]: https://github.com/gjtorikian/html-proofer

[original design]: https://github.com/dleidert/www.wgdd.org/blob/01bed8bfd7181b4b907d01f450ded471eb10e742/.travis.yml#L33-L38
[in the docs]: https://docs.travis-ci.com/user/job-lifecycle/#the-job-lifecycle

# vim: set tw=79 ts=2 sw=2 ai si et:
