---
lang: en
title: Skipping the CI build job on salsa.debian.org
author: dleidert
description: >-
  To skip CI build jobs on the gitlab-powered platform salsa.debian.org you can
  either use a special commit message note or the git command line push option
  ci.skip.
category:
- debian
- planet-debian
tags:
- gitlab
- salsa.d.o
- packaging
- ci
- git
---

The salsa-ci team offers [pre-written CI jobs][salsa-ci] to build and test your
Debian package with every push. In case you don't want to start the build every
time you push your changes to the server you can skip the build by either using
a special commit message note or a special push option. This might also be
useful, because pushing commits and tags separately might start the job
pipeline twice[^1].

If the commit message contains the string `[ci skip]` or `[skip ci]` in any
capitalization will do the job.

But I prefer to not pollute the log with such non-packaging related content. So
I prefer the second way. Since some time Git offers to advertise strings as
push options. These are then processed by the server in question. To skip the
job just run

```
$ git push -o ci.skip
```

[^1]: To push the tags together with the commits you can run `git config
      push.followTags true` to either set this option locally or globally.

[salsa-ci]: https://salsa.debian.org/salsa-ci-team/pipeline/blob/master/README.md
[ci.skip]: https://docs.gitlab.com/ee/ci/yaml/#skipping-jobs "Gitlab documentation: Skipping jobs"

<!-- vim: set tw=79 ts=2 sw=2 ai si et: -->
