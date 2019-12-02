---
title: Test the console lexer
category:
  - tests
  - jekyll
tags:
  - jekyll
  - rouge
  - blog
  - test
  - markdown
---

This is a test

* using `console`

```console
# foo
bar
$ bla
> bli
## blu
% foobar
| loo
```

* using `console?prompt=#`

```console?prompt=#
# foo
bar
$ bla
> bli
## blu
% foobar
| loo
```

* using `console?prompt=%,#,$,>,|`

```console?prompt=%,#,$,>,|
# foo
bar
$ bla
> bli
## blu
% foobar
| loo
```

* using `console?comments`

```console?comments
# foo
bar
```

* using `console?comments=true`

```console?comments=true
# foo
bar
```

* using `console?comments=1`

```console?comments=1
# foo
bar
```

* using `console?comments=false`

```console?comments=false
# foo
bar
```

* using `console?comments=0`

```console?comments=0
# foo
bar
```

<!-- # vim: set tw=79 ts=2 sw=2 ai si et: -->
