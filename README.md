pen [![pub package](https://img.shields.io/pub/v/pen.svg)](https://pub.dartlang.org/packages/pen) [![Build Status](https://travis-ci.org/seaneagan/pen.svg?branch=master)](https://travis-ci.org/seaneagan/pen)
===

A pubspec authoring tool. (forked from den)

##Install

```shell
pub global activate pen
```

##Usage

```shell
# `pen ...` requires Dart >=1.7, on 1.6 use `pub global run pen ...`

# Create a pubspec.  Field value prompts default to your local git info.
pen spec
# Bypass prompts, accept defaults.
pen spec --force

# Bump your pubspec version (and do a tagged version commit if in a git repo)
pen bump patch               # 1.2.3 -> 1.2.4
pen bump minor               # 1.2.3 -> 1.3.0
pen bump major --pre-id beta # 1.2.3 -> 2.0.0-beta.0
pen bump release --pre       # 1.0.0-dev.2 -> 1.0.0-dev.3
pen bump release             # 1.0.0-dev.2 -> 1.0.0
pen bump build               # 1.0.2+1 -> 1.0.2+2
pen bump breaking            # 0.5.1 -> 0.6.0 / 1.2.3 -> 2.0.0
pen bump 1.2.3-dev           # 1.2.2 -> 1.2.3-dev
pen bump minor -m "ver{v}"   # Custom commit message.

# Install dependencies (defaults to '>={latest stable} <{next breaking}')
pen install polymer browser
pen install unittest --dev
pen install polymer#any
pen install git://github.com/owner/repo.git -sgit
pen install git://github.com/owner/repo#ref -sgit
pen install path/to/foo -spath

# Uninstall dependencies
pen uninstall junk kludge

# Keep dependencies up-to-date

# Show outdated (all by deafult)
pen fetch
pen fetch polymer

# Update outdated to '>={latest stable} <{next breaking}' (all by default)
pen pull
pen pull polymer

# Install comprehensive TAB-completion for pen
pen completion install

# Complete commands, options, package names, etc.
pen i[TAB] -> install
pen install unit[TAB] -> unittest
pen uninstall j[TAB] -> junk
pen fetch p[TAB] -> polymer
pen pull p[TAB] -> polymer
```

###Package Authors

Add the following package installation instructions to your README:

```shell
pub global activate pen
pen install <your package name>
```

##^ Constraints

`pen install` and `pen pull` will take advantage of [^ constraints][caret_info]
e.g. `^1.2.3` if either of:

* Your [sdk constraint][sdk_constraint] disallows pre-1.8.0 SDKs when ^ was introduced.
* You pass the `--caret` flag, which updates your sdk constraint for you.

Otherwise, they will use range syntax e.g. `>=1.2.3 <2.0.0`

[caret_info]: https://groups.google.com/a/dartlang.org/forum/#!topic/misc/0t9qQF-rZg4
[sdk_constraint]: https://www.dartlang.org/tools/pub/pubspec.html#sdk-constraints

##Programmatic Usage

The underlying functionality is available as a Dart API through the [pen_api][] package,
which this package is merely a command-line interface for.

[pen_api]: https://github.com/seaneagan/pen_api

##Inspiration

`pen install` was inspired by [`npm install --save`][npm install] and [`bower install --save`][bower install]
`pen fetch` and `pen pull` were inspired by [`david` and `david update`][david].

[npm install]: https://www.npmjs.org/doc/cli/npm-install.html
[bower install]: http://bower.io/docs/api/#install
[david]: https://github.com/alanshaw/david#cli
