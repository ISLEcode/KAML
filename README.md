---
revision    : Mon Oct 01, 2018 19:47:17
title       : KAML ain't markup language
subtitle    : The specifications
author      : Jean-Michel Marcastel
---

KAML ain't markup language
--------------------------

This is the repository of the KAML specifications.

### Abstract

[KAML] aims to be a minimal configuration file format that is easy to read by programs and humans alike. [KAML] is the formal
specification of Korn shell *compound variables* (renamed here *dictionaries*) which have been around since the mid 1980s -- we
have, with `ksh93`, a reference implementation and linter, and with `libast` a reference C implementation. With this heritage,
[KAML] could be said to be [POSIX] compliant -- though obviously this is an [Open Group] prerogative.

[KAML] stands for *KAML ain't markup language*... it's Korn shell (with GNU lineage). Pronounced *camel* (/ˈkæməl/), the acronym
was chosen to sound like [YAML], for which [KAML] is intended to be a more flexible and extensible alternative. Like [YAML],
[KAML] is a superset of [JSON] offering many extended features that are practical for configuration files, and less important to
data exchange. [KAML] is a superset of [YAML] too; providing much of the functionality of [ASN-1] or [XSLT] transformations in
the robust and simple syntax of [POSIX] shells.

  [KAML]: https://github.com/ISLEcode/KAML
  [POSIX]: https://en.wikipedia.org/wiki/POSIX
  [Open Group]: http://www.opengroup.org
  [YAML]: https://en.wikipedia.org/wiki/YAML
  [JSON]: https://en.wikipedia.org/wiki/JSON
  [ASN-1]: https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One
  [XSLT]: https://en.wikipedia.org/wiki/XSLT

<!-- vim: set nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb :-->
