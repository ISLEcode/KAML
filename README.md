---
revision    : Mon Feb 05, 2018 19:59:27
author      : Jean-Michel Marcastel
title       : KAML ain't markup language
---

## KAML ain't markup language
<!-- @{ toc -->

Sections
:   [Overview](#overview) |
    [Examples](#examples) |
    [Version](#version)

Next
:   [Specifications](#specifications) |
    [About](#about)

<!-- @} -->
<!-- @{ h3: overview -->
### [Overview](#kaml-aint-markup-language)

[KAML] aims to be a minimal configuration file format that is easy to read by programs and humans alike. [KAML] is the formal
specification of Korn shell _compound variables_ which have been around since the mid 1980s -- we have, with `ksh93`, a reference
implementation and linter, and with `libast` a reference C implementation. With this heritage, [KAML] could be said to be _POSIX
compliant_ -- though obviously this is an Open Group prerogative.

[KAML] stands for _KAML ain't markup language_... it is Korn shell -- thank you Richard (Stallman)! Pronounced _camel_
(/ˈkæməl/), the acronym was chosen to sound like [YAML], for which [KAML] is intended to be a more flexible and extensible
alternative. Like [YAML], [KAML] is a superset of [JSON]; [KAML] is a superset of [YAML] too! [KAML] aims to play well with [JSON]
which is a de facto standard for mobile apps, REST interfaces, and the like.

<!-- @} -->
<!-- @{ h3: examples -->
### [Examples](#kaml-aint-markup-language)

Topics
:   [Plain scalars](#plain-scalars) |
    [Scalars with type attributes](#scalars-with-type-attributes) |
    [Indexed and associative arrays, compound variables](#indexed-and-associative-arrays-compound-variables) |
    [Custom types and classes](#custom-types-and-classes) |
    [POSIX shell features](#posix-shell-features) |
    [Korn shell extensions](#korn-shell-extensions) |
    [Custom type definitions ](#custom-type-definitions)

<!-- @{ plain scalars -->
#### [Plain scalars](#examples)
```
title="KAML Example"                    # A simple string
author=Jean-Michel\ Marcastel           # Alternate string representation with escaped whitespaces
number=1234                             # Numeric value handled as a string
```

<!-- @} -->
<!-- @{ scalars with type attributes -->
#### [Scalars with type attributes](#examples)
```
bool_e      flag=true                   # Enumeration type `bool_e` (true, false)

upper       tag=kaml                    # String converted automatically to uppercase
lower       extension=.xml              # String converted automatically to lowercase
nameref     brief=title                 # Name reference. Here brief evaluate to "KAML Example"
binary      image=...                   # Binary data encoded as Base64

readonly    pi=3.1415926                # Declare property as read only
longint     long=1234                   # Numeric value evaluated as a `long int`
longuint    long=1234                   # Numeric value evaluated as an `unsigned long int`
shortint    short=1234                  # Numeric value evaluated as a `short int`
shortuint   short=1234                  # Numeric value evaluated as an `unsigned short int`
hexint      commit=a23ef9               # Numeric value in base 16
octal       mode=0777                   # Numeric value in base 8
bits        flags=010101                # Numeric value in base 2
float       rate=0.1234567              # Float represented in scientific notation with 10 significant figures
hexfloat    rate=0.1234567              # Float represented in hexadecimal notation with 10 significant figures
```

<!-- @} -->
<!-- @{ indexed and associative arrays, compound variables-->
#### [Indexed and associative arrays, compound variables](#examples)
```
upper       see_also=(                  # Indexed array with uppercased items
    asn-1 ini json kaml sgml yaml xml
)

coordinates=(                           # Array of arrays
    ( a b c )                           #
    ( i j k )                           # Indexed arrays, associative arrays and compound variables
    ( x y z )                           # allow recursive nesting.
)

hash bookmarks=(                        # Associative array
    [ASN-1]=https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One
    [INI]=https://en.wikipedia.org/wiki/INI_file
    [JSON]=https://en.wikipedia.org/wiki/JSON
    [KAML]=https://github.com/ISLEcode/KAML
    [SGML]=https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language
    [TOML]=https://en.wikipedia.org/wiki/TOML
    [YAML]=https://en.wikipedia.org/wiki/YAML
)

compound record=(                       # Compound variable
    server=192.168.1.1
    ports=( 8001 8001 8002 )
    connection_max=5000
    bool_e enabled=true
)
```

<!-- @} -->
<!-- @{ custom types and classes -->
#### [Custom types and classes](#examples)
```
BookmarkItem website=(                  # Custom class `BookmarkItem`
    url=https://github.com/ISLEcode/KAML
    label="KAML ain't markup"
)

website.label+=" (github)"              # Appending to a previous declared property
```

<!-- @} -->
<!-- @{ posix shell features -->
#### [POSIX shell features](#examples)
```
files=*                                 # Generate filenames matching a pattern
files=**                                # Alternate syntax for recursive descent
path=$PATH                              # Variable expansion
system=$(uname -s)                      # Embed output of exec(3)
```

<!-- @} -->
<!-- @{ korn shell extensions -->
#### [Korn shell extensions](#examples)
```
top_bin=${PATH%%:*}                     # Variable manipulation and conversions
content=$(< /etc/passwd )               # Slurp in files
```

<!-- @} -->
<!-- @{ custom type definitions -->
#### [Custom type definitions](#examples)
```
typeset -u tag=kaml                     # String converted automatically to uppercase
typeset -l extension=.xml               # String converted automatically to lowercase
typeset -M[mapping] x=...               # Wide character mapping support using wctrans(3)

typeset -m keywords=tag                 # Move. Here keywords evaluates to "KAML" and tag will be unset

typeset -R 20 label=name                # Right justify, padding with spaces to meet 20 characters.
typeset -RZ 20 label=name               # Right justify, padding with zeros to meet 20 characters.

typeset -L 20 label=name                # Left justify, padding with spaces to meet 20 characters.
typeset -LZ 20 label=name               # Left justify, padding with zeros to meet 20 characters.

integer -l  long=1234                   # Numeric value evaluated as a `long int`
integer -ul long=1234                   # Numeric value evaluated as an `unsigned long int`
integer -s  short=1234                  # Numeric value evaluated as a `short int`
integer -us short=1234                  # Numeric value evaluated as an `unsigned short int`
integer -i8 mode=0777                   # Numeric value in base 8 -- arithmetic bases 2 to 64 are supported

float       rate=0.1234567              # Float represented in scientific notation with 10 significant figures
float -E2   rate=0.1234567              # Float represented in scientific notation with 2 significant figures
typeset -F2 rate=0.1234567              # Float with 2 significant figures
typeset -X0 rate=0.1234567              # Float represented in hexadecimal notation with 0 significant figures

typeset -b image=...                    # Binary data encoded as Base64
```

<!-- @} -->

<!-- @} -->
<!-- @{ h3: version -->
### [Version](#kaml-aint-markup-language)

The [KAML] implementation has been stable over three decades. The [KAML] specification is still work-in-progress as many of the more
powerful features of [KAML] have not yet been documented.

| [KAML] Version  | Korn shell version  |
|----------------:|--------------------:|
|     [0.1.0-wip] | AJM 93u+ 2012-08-01 |

[0.1.0-wip]: https://github.com/ISLEcode/[KAML]

Guidelines:

-   [KAML] versioning will follow [semantic versioning](https://semver.org) principles.
-   Each version of [KAML] will be bound to a release of the Korn shell which serves as the reference implementation of the
    specification.
-   The
[github]: https://github.com/ISLEcode/[KAML]
       repository of this repository tracks the very latest development and may contain
    features and changes that do not exist on any released version.


<!-- @} -->
## Specifications
<!-- @{ toc -->

Sections
:   [General considerations](#general-considerations) |
    [Comments](#comments) |
    [Name/value pairs](#namevalue-pairs) |
    [Scalars](#scalars) |
    [Indexed arrays](#indexed-arrays) |
    [Associative arrays](#associative-arrays) |
    [Compound variables](#compound-variables)

Previous
:   [Top](#kaml-aint-markup-language)

Next
:   [About](#about)

<!-- @} -->
<!-- @{ h3: general considerations -->
### [General considerations](#specifications)

-   KAML is Korn shell syntax
    -   it is case sensitive
    -   character encoding is either ANSI ASCII or UTF-8
    -   whitespace matches POSIX regexp class `[[:space:]]`
    -   `ksh -n` is the KAML linter
-   KAML files should use the extension `.kml`.
-   KAML files should follow UNIX conventions for newlines

<!-- @} -->
<!-- @{ h3: comments -->
### [Comments](#specifications)

A hash symbol marks the rest of the line as a comment.

```{.sh}
# This is a full-line comment
name="value" # This is a comment at the end of a line
```

<!-- @} -->
<!-- @{ h3: name/value pairs -->
### [Name/value pairs](#specifications)

The primary building block of a KAML document is the name/value pair.

```{.sh}
name=value
```

1.  Names are on the left of the equals sign and values are on the right.

1.  A name cannot be an empty string.

1.  The equal sign must not be preceded or followed by white space.

1.  The name must be a valid shell identifier (i.e. start with an underscore or an alphabetic character, and be composed of
    zero or more alphanumeric characters or the underscore).

    <!-- TODO: myKeyName, my-key-name should be standardised to my_key_name -->

1.  The dot in names is used to define the path of the property in the compound variable.

    For instance:
    ```
    my.address.zicode=1201
    ```
    would be represented in JSON as:
    ```{.json}
    {
        "my": {
            "address": {
                "zipcode": "1201"
            }
        }
    }
    ```

1.  The name can be preceded by a type specification (see [type specifications](#type-spectifications) below.

1.  The right hand side value can be either a [scalar](#scalars), an [indexed array](#indexed-arrays), an [associative
    array](#associative-array), a [compound variable](#compound-variables), or [custom types](#custom-types).

<!-- @} -->
<!-- @{ h3: scalars -->
### [Scalars](#specifications)

There are four ways to express strings: basic, multi-line basic, literal, and
multi-line literal. All strings must contain only valid UTF-8 characters.

**Basic strings** are surrounded by quotation marks. Any Unicode character may
be used except those that must be escaped: quotation mark, backslash, and the
control characters (U+0000 to U+001F, U+007F).

```{.sh}
str = "I'm a string. \"You can quote me\". Name\tJos\u00E9\nLocation\tSF."
```

For convenience, some popular characters have a compact escape sequence.

```
\b         - backspace       (U+0008)
\t         - tab             (U+0009)
\n         - linefeed        (U+000A)
\f         - form feed       (U+000C)
\r         - carriage return (U+000D)
\"         - quote           (U+0022)
\\         - backslash       (U+005C)
\uXXXX     - unicode         (U+XXXX)
\UXXXXXXXX - unicode         (U+XXXXXXXX)
```

Any Unicode character may be escaped with the `\uXXXX` or `\UXXXXXXXX` forms.
The escape codes must be valid Unicode [scalar values](http://unicode.org/glossary/#unicode_scalar_value).

All other escape sequences not listed above are reserved and, if used, [KAML]
should produce an error.

Sometimes you need to express passages of text (e.g. translation files) or would
like to break up a very long string into multiple lines. [KAML] makes this easy.

**Multi-line basic strings** are surrounded by three quotation marks on each
side and allow newlines. A newline immediately following the opening delimiter
will be trimmed. All other whitespace and newline characters remain intact.

```{.sh}
str1 = """
Roses are red
Violets are blue"""
```

[KAML] parsers should feel free to normalize newline to whatever makes sense for
their platform.

```{.sh}
# On a Unix system, the above multi-line string will most likely be the same as:
str2 = "Roses are red\nViolets are blue"

# On a Windows system, it will most likely be equivalent to:
str3 = "Roses are red\r\nViolets are blue"
```

For writing long strings without introducing extraneous whitespace, use a "line
ending backslash". When the last non-whitespace character on a line is a `\`, it
will be trimmed along with all whitespace (including newlines) up to the next
non-whitespace character or closing delimiter. All of the escape sequences that
are valid for basic strings are also valid for multi-line basic strings.

```{.sh}
# The following strings are byte-for-byte equivalent:
str1 = "The quick brown fox jumps over the lazy dog."

str2 = """
The quick brown \


  fox jumps over \
    the lazy dog."""

str3 = """\
       The quick brown \
       fox jumps over \
       the lazy dog.\
       """
```

Any Unicode character may be used except those that must be escaped: backslash
and the control characters (U+0000 to U+001F). Quotation marks need not be
escaped unless their presence would create a premature closing delimiter.

If you're a frequent specifier of Windows paths or regular expressions, then
having to escape backslashes quickly becomes tedious and error prone. To help,
[KAML] supports literal strings which do not allow escaping at all.

**Literal strings** are surrounded by single quotes. Like basic strings, they
must appear on a single line:

```{.sh}
# What you see is what you get.
winpath  = 'C:\Users\nodejs\templates'
winpath2 = '\\ServerX\admin$\system32\'
quoted   = 'Tom "Dubs" Preston-Werner'
regex    = '<\i\c*\s*>'
```

Since there is no escaping, there is no way to write a single quote inside a
literal string enclosed by single quotes. Luckily, [KAML] supports a multi-line
version of literal strings that solves this problem.

**Multi-line literal strings** are surrounded by three single quotes on each
side and allow newlines. Like literal strings, there is no escaping whatsoever.
A newline immediately following the opening delimiter will be trimmed. All
other content between the delimiters is interpreted as-is without modification.

```{.sh}
regex2 = '''I [dw]on't need \d{2} apples'''
lines  = '''
The first newline is
trimmed in raw strings.
   All other whitespace
   is preserved.
'''
```

Control characters other than tab are not permitted in a literal string. Thus,
for binary data it is recommended that you use Base64 or another suitable ASCII
or UTF-8 encoding. The handling of that encoding will be application specific.

#### Integer

Integers are whole numbers. Positive numbers may be prefixed with a plus sign.
Negative numbers are prefixed with a minus sign.

```{.sh}
int1 = +99
int2 = 42
int3 = 0
int4 = -17
```

For large numbers, you may use underscores between digits to enhance
readability. Each underscore must be surrounded by at least one digit on each
side.

```{.sh}
int5 = 1_000
int6 = 5_349_221
int7 = 1_2_3_4_5     # VALID but discouraged
```

Leading zeros are not allowed. Integer values `-0` and `+0` are valid and
identical to an unprefixed zero.

Non-negative integer values may also be expressed in hexadecimal, octal, or
binary. In these formats, leading zeros are allowed (after the prefix). Hex
values are case insensitive. Underscores are allowed between digits (but not
between the prefix and the value).

```{.sh}
# hexadecimal with prefix `0x`
hex1 = 0xDEADBEEF
hex2 = 0xdeadbeef
hex3 = 0xdead_beef

# octal with prefix `0o`
oct1 = 0o01234567
oct2 = 0o755 # useful for Unix file permissions

# binary with prefix `0b`
bin1 = 0b11010110
```

64 bit (signed long) range expected (−9,223,372,036,854,775,808 to
9,223,372,036,854,775,807).

#### Float

Floats should be implemented as IEEE 754 binary64 values.

A float consists of an integer part (which follows the same rules as integer
values) followed by a fractional part and/or an exponent part. If both a
fractional part and exponent part are present, the fractional part must precede
the exponent part.

```{.sh}
# fractional
flt1 = +1.0
flt2 = 3.1415
flt3 = -0.01

# exponent
flt4 = 5e+22
flt5 = 1e6
flt6 = -2E-2

# both
flt7 = 6.626e-34
```

A fractional part is a decimal point followed by one or more digits.

An exponent part is an E (upper or lower case) followed by an integer part
(which follows the same rules as integer values).

Similar to integers, you may use underscores to enhance readability. Each
underscore must be surrounded by at least one digit.

```{.sh}
flt8 = 9_224_617.445_991_228_313
```

Float values `-0.0` and `+0.0` are valid and should map according to IEEE 754.

Special float values can also be expressed. They are always lowercase.

```{.sh}
# infinity
sf1 = inf  # positive infinity
sf2 = +inf # positive infinity
sf3 = -inf # negative infinity

# not a number
sf4 = nan  # actual sNaN/qNaN encoding is implementation specific
sf5 = +nan # same as `nan`
sf6 = -nan # valid, actual encoding is implementation specific
```

#### Boolean

Booleans are just the tokens you're used to. Always lowercase.

```{.sh}
bool1 = true
bool2 = false
```

#### Offset Date-Time

To unambiguously represent a specific instant in time, you may use an
[RFC 3339](http://tools.ietf.org/html/rfc3339) formatted date-time with offset.

```{.sh}
odt1 = 1979-05-27T07:32:00Z
odt2 = 1979-05-27T00:32:00-07:00
odt3 = 1979-05-27T00:32:00.999999-07:00
```

For the sake of readability, you may replace the T delimiter between date and
time with a space (as permitted by RFC 3339 section 5.6).

```{.sh}
odt4 = 1979-05-27 07:32:00Z
```

The precision of fractional seconds is implementation specific, but at least
millisecond precision is expected. If the value contains greater precision than
the implementation can support, the additional precision must be truncated, not
rounded.

#### Local Date-Time

If you omit the offset from an [RFC 3339](http://tools.ietf.org/html/rfc3339)
formatted date-time, it will represent the given date-time without any relation
to an offset or timezone. It cannot be converted to an instant in time without
additional information. Conversion to an instant, if required, is implementation
specific.

```{.sh}
ldt1 = 1979-05-27T07:32:00
ldt2 = 1979-05-27T00:32:00.999999
```

The precision of fractional seconds is implementation specific, but at least
millisecond precision is expected. If the value contains greater precision than
the implementation can support, the additional precision must be truncated, not
rounded.

#### Local Date

If you include only the date portion of an
[RFC 3339](http://tools.ietf.org/html/rfc3339) formatted date-time, it will
represent that entire day without any relation to an offset or timezone.

```{.sh}
ld1 = 1979-05-27
```

##### Local Time

If you include only the time portion of an [RFC
3339](http://tools.ietf.org/html/rfc3339) formatted date-time, it will represent
that time of day without any relation to a specific day or any offset or
timezone.

```{.sh}
lt1 = 07:32:00
lt2 = 00:32:00.999999
```

The precision of fractional seconds is implementation specific, but at least
millisecond precision is expected. If the value contains greater precision than
the implementation can support, the additional precision must be truncated, not
rounded.

<!-- @} -->
<!-- @{ h3: indexed arrays --->
### [Indexed arrays](#specifications)

Arrays are square brackets with values inside. Whitespace is ignored. Elements
are separated by commas. Data types may not be mixed (different ways to define
strings should be considered the same type, and so should arrays with different
element types).

```{.sh}
arr1 = [ 1, 2, 3 ]
arr2 = [ "red", "yellow", "green" ]
arr3 = [ [ 1, 2 ], [3, 4, 5] ]
arr4 = [ "all", 'strings', """are the same""", '''type''']
arr5 = [ [ 1, 2 ], ["a", "b", "c"] ]

arr6 = [ 1, 2.0 ] # INVALID
```

Arrays can also be multiline. Terminating commas (also called trailing commas)
are ok after the last value of the array. There can be an arbitrary number of
newlines and comments before a value and before the closing bracket.

```{.sh}
arr7 = [
  1, 2, 3
]

arr8 = [
  1,
  2, # this is ok
]
```

<!-- @} -->
<!-- @{ h3: associative arrays -->
### [Associative arrays](#specifications)

Tables (also known as hash tables or dictionaries) are collections of key/value
pairs. They appear in square brackets on a line by themselves. You can tell them
apart from arrays because arrays are only ever values.

```{.sh}
[table]
```

Under that, and until the next table or EOF are the key/values of that table.
Key/value pairs within tables are not guaranteed to be in any specific order.

```{.sh}
[table-1]
key1 = "some string"
key2 = 123

[table-2]
key1 = "another string"
key2 = 456
```

Dots are prohibited in bare keys because dots are used to signify nested tables.
Naming rules for tables are the same as for keys (see definition of Keys above).

```{.sh}
[dog."tater.man"]
type.name = "pug"
```

In JSON land, that would give you the following structure:

```json
{ "dog": { "tater.man": { "type": { "name": "pug" } } } }
```

Whitespace around the key is ignored, however, best practice is to not use any
extraneous whitespace.

```{.sh}
[a.b.c]            # this is best practice
[ d.e.f ]          # same as [d.e.f]
[ g .  h  . i ]    # same as [g.h.i]
[ j . "ʞ" . 'l' ]  # same as [j."ʞ".'l']
```

You don't need to specify all the super-tables if you don't want to. [KAML] knows
how to do it for you.

```{.sh}
# [x] you
# [x.y] don't
# [x.y.z] need these
[x.y.z.w] # for this to work
```

Empty tables are allowed and simply have no key/value pairs within them.

As long as a super-table hasn't been directly defined and hasn't defined a
specific key, you may still write to it.

```{.sh}
[a.b]
c = 1

[a]
d = 2
```

You cannot define any key or table more than once. Doing so is invalid.

```
# DO NOT DO THIS

[a]
b = 1

[a]
c = 2
```

```
# DO NOT DO THIS EITHER

[a]
b = 1

[a.b]
c = 2
```

All table names must be non-empty.

```
[]     # INVALID
[a.]   # INVALID
[a..b] # INVALID
[.b]   # INVALID
[.]    # INVALID
```

#### Inline Table

Inline tables provide a more compact syntax for expressing tables. They are
especially useful for grouped data that can otherwise quickly become verbose.
Inline tables are enclosed in curly braces `{` and `}`. Within the braces, zero
or more comma separated key/value pairs may appear. Key/value pairs take the
same form as key/value pairs in standard tables. All value types are allowed,
including inline tables.

Inline tables are intended to appear on a single line. No newlines are allowed
between the curly braces unless they are valid within a value. Even so, it is
strongly discouraged to break an inline table onto multiples lines. If you find
yourself gripped with this desire, it means you should be using standard tables.

```{.sh}
name = { first = "Tom", last = "Preston-Werner" }
point = { x = 1, y = 2 }
```

The inline tables above are identical to the following standard table
definitions:

```{.sh}
[name]
first = "Tom"
last = "Preston-Werner"

[point]
x = 1
y = 2
```

<!-- @} -->
<!-- @{ h3: compound variables -->
### [Compound variables](#specifications)

The last type that has not yet been expressed is an array of tables. These can
be expressed by using a table name in double brackets. Each table with the same
double bracketed name will be an element in the array. The tables are inserted
in the order encountered. A double bracketed table without any key/value pairs
will be considered an empty table.

```{.sh}
[[products]]
name = "Hammer"
sku = 738594937

[[products]]

[[products]]
name = "Nail"
sku = 284758393
color = "gray"
```

In JSON land, that would give you the following structure.

```json
{
  "products": [
    { "name": "Hammer", "sku": 738594937 },
    { },
    { "name": "Nail", "sku": 284758393, "color": "gray" }
  ]
}
```

You can create nested arrays of tables as well. Just use the same double bracket
syntax on sub-tables. Each double-bracketed sub-table will belong to the most
recently defined table element above it.

```{.sh}
[[fruit]]
  name = "apple"

  [fruit.physical]
    color = "red"
    shape = "round"

  [[fruit.variety]]
    name = "red delicious"

  [[fruit.variety]]
    name = "granny smith"

[[fruit]]
  name = "banana"

  [[fruit.variety]]
    name = "plantain"
```

The above [KAML] maps to the following JSON.

```json
{
  "fruit": [
    {
      "name": "apple",
      "physical": {
        "color": "red",
        "shape": "round"
      },
      "variety": [
        { "name": "red delicious" },
        { "name": "granny smith" }
      ]
    },
    {
      "name": "banana",
      "variety": [
        { "name": "plantain" }
      ]
    }
  ]
}
```

Attempting to append to a statically defined array, even if that array is empty
or of compatible type, must produce an error at parse time.

```{.sh}
# INVALID [KAML] DOC
fruit = []

[[fruit]] # Not allowed
```

Attempting to define a normal table with the same name as an already established
array must produce an error at parse time.

```
# INVALID [KAML] DOC
[[fruit]]
  name = "apple"

  [[fruit.variety]]
    name = "red delicious"

  # This table conflicts with the previous table
  [fruit.variety]
    name = "granny smith"
```

You may also use inline tables where appropriate:

```{.sh}
points = ( ( x=1 y=2 z=3 )
           ( x=7 y=8 z=9 )
           ( x=2 y=4 z=8 ) )
```

<!-- @} -->
## About
<!-- @{ toc -->

Sections
:   [Comparison with other formats](#comparison-with-other-formats) |
    [Get involved](#get-involved)

Previous
:   [Specifications](#specifications), [Top](#kaml-aint-markup-language)

<!-- @} -->
<!-- @{ comparison with other formats -->
#### [Comparison with other formats](#about)

Why yet another configuration exchange markup language? We already have [ASN-1], [JSON], [TOML], [YAML], [XML], and countless
others! The original motivation was to have a simple to read, simple to parse, and simple to implement configuration file format
which could be used across various environments and programming languages.

[ASN-1] and [SGML]/[XML] are robust and very complete, they are horribly verbose for human-based management and update. [JSON] is
a much simplier syntax that is well specified and maps maps easily to ubiquitous data types. JSON is great for serializing and has
become a de facto standard for REST and the like interfaces. JSON however lacks features that help humans maintain the data.
[YAML] brings in such features, but at the expense of being hard to parse. [INI] files, though not standardised, are simple and
easy to maintain; yet they primarily target flat data structures and have no data types. More recently [TOML] appears as an
attempt to make [INI] files overcome the aforementioned limitations, at the cost of extra verbosity.

[KAML] pre-dates all these formats -- except perhaps the INI format. [KAML] is nothing but a formal definition of the _compound
variable_ syntax available in the Korn shell since the mid 1980s. [KAML] came to life in Korn shell pretty much for the same reasons
as JSON appeared in Javascript; to allow easy interchange of structured data sets. Indeed an often overlooked feature of Korn
shell is that it natively supports classes, type definitions, enumerations and the so-called compound variables that can be
compared to `struct` definitions in C.

maps easily to ubiquitous data types. JSON is great for serializing
data that will mostly be read and written by computer programs. Where
[KAML] differs from JSON is its emphasis on being easy for humans to
read and write. Comments are a good example: they serve no purpose
when data is being sent from one program to another, but are very
helpful in a configuration file that may be edited by hand.

The YAML format is oriented towards configuration files just like
[KAML]. For many purposes, however, YAML is an overly complex
solution. [KAML] aims for simplicity, a goal which is not apparent in
the YAML specification:
http://www.yaml.org/spec/1.2/spec.html

<!-- @} -->
<!-- @{ get involved -->
#### [Get Involved](#about)

Documentation, bug reports, pull requests, and all other contributions are welcome!

<!-- @} -->
<!-- @{ bookmarks -->

[ASN-1]:    https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One
[INI]:      https://en.wikipedia.org/wiki/INI_file
[JSON]:     https://en.wikipedia.org/wiki/JSON
[KAML]:     https://github.com/ISLEcode/KAML
[SGML]:     https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language
[TOML]:     https://en.wikipedia.org/wiki/TOML
[YAML]:     https://en.wikipedia.org/wiki/YAML
[XML]:      https://en.wikipedia.org/wiki/XML

<!-- vim: set nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb :-->
