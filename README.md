---
revision    : Wed Feb 07, 2018 14:34:22
title       : KAML ain't markup language
subtitle    : The specifications
author      : Jean-Michel Marcastel
---

## KAML ain't markup language
<!-- @{ toc -->

<small>

Sub-sections
:   [Overview](#overview) |
    [Version](#version) |
    [Examples](#examples)

Next sections
:   [Specifications](#specifications) |
    [About](#about)

</small>

<!-- @} -->
<!-- @{ h3: overview -->
### [Overview](#kaml-aint-markup-language)

[KAML] aims to be a minimal configuration file format that is easy to read by programs and humans alike. [KAML] is the formal
specification of Korn shell _compound variables_ (renamed here _dictionaries_) which have been around since the mid 1980s -- we
have, with `ksh93`, a reference implementation and linter, and with `libast` a reference C implementation. With this heritage,
[KAML] could be said to be [POSIX] compliant -- though obviously this is an [Open Group] prerogative.

[KAML] stands for _KAML ain't markup language_... it's Korn shell (with GNU lineage). Pronounced _camel_
(/ˈkæməl/), the acronym was chosen to sound like [YAML], for which [KAML] is intended to be a more flexible and extensible
alternative. Like [YAML], [KAML] is a superset of [JSON] offering many extended features that are practical for configuration
files, and less important to data exchange. [KAML] is a superset of [YAML] too; providing much of the functionality of [ASN-1] or
[XSLT] transformations in the robust and simple syntax of [POSIX] shells.

<!-- @} -->
<!-- @{ h3: version -->
### [Version](#kaml-aint-markup-language)

The [KAML] reference implementation (i.e. Korn shell compound variables) has been stable over three decades. The [KAML]
specification is still work-in-progress as many of the more powerful features of [KAML] have not yet been documented.

| KAML Version    | Korn shell version  | Version notes                                                                          |
| :-------------: | :-----------------: | :------------------------------------------------------------------------------------- |
|             n/a | `ksh88`             | Korn shell (1988 incarnation). First _official_ appearance of compound variables.      |
|             n/a | `ksh93`             | Korn shell (1993 incarnation). Reference implementation for KAML 0.1.0.                |
|     [0.1.0-wip] | AJM 93u+ 2012-08-01 | First formal definition. Still in the workings. Implementation very stable.            |

[0.1.0-wip]: https://github.com/ISLEcode/[KAML]

-   [KAML] versioning follows [semantic versioning](https://semver.org) principles.
-   Each version of [KAML] is bound to a release of the Korn shell which serves as the reference implementation of the
    specification.
-   [KAML] is maintained on GitHub (<https://github.com/ISLEcode/KAMP>)


<!-- @} -->
<!-- @{ h3: examples -->
### [Examples](#kaml-aint-markup-language)

Topics
:   [Plain scalars](#plain-scalars) |
    [Scalars with type attributes](#scalars-with-type-attributes) |
    [Indexed and associative arrays, compound properties](#indexed-and-associative-arrays-compound-properties) |
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
<!-- @{ indexed and associative arrays, compound properties-->
#### [Indexed and associative arrays, compound properties](#examples)
```
upper       see_also=(                  # Indexed array with uppercased items
    asn-1 ini json kaml sgml yaml xml
)

coordinates=(                           # Array of arrays
    ( a b c )                           #
    ( i j k )                           # Indexed arrays, associative arrays and compound properties
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

compound record=(                       # Compound property
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
path=$PATH                              # Property expansion
system=$(uname -s)                      # Embed output of exec(3)
```

<!-- @} -->
<!-- @{ korn shell extensions -->
#### [Korn shell extensions](#examples)
```
top_bin=${PATH%%:*}                     # Property manipulation and conversions
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
## Specifications
<!-- @{ toc -->

<small>

Sub-sections
:   [Overview](#overview) |
    [Identifiers](#identifiers) |
    [Properties](#properties) |
    [Scalars](#scalars) |
    [Numbers](#numbers) |
    [Arrays](#arrays) |
    [Dictionaries](#dictionaries) |
    [Custom types](#custom-types) |
    [Comments](#comments)

Previous section
:   [Top](#kaml-aint-markup-language)

Next section
:   [About](#about)

</small>

<!-- @} -->
<!-- @{ h3: overview -->
### [Overview](#specifications)

-   KAML is Korn shell syntax
    -   character encoding is either ANSI ASCII or UTF-8
    -   whitespace matches [POSIX] regexp class `[[:space:]]`
    -   `ksh -n` is the KAML linter
-   KAML files should use the extension `.kml`.
-   KAML files should follow UNIX conventions for newlines

<!-- @} -->
<!-- @{ h3: identifiers -->
### [Identifiers](#specifications)

```{.ebnf}
identifier          = identifier-first, { identifier-next } ;
identifier-first    = ? [[:alpha:]] or "_" ? ;
identifier-next     = ? [[:alnum:]] or "_" ? ;
```
Identifiers are used to construct the name of properties. An identifier is a sequence of characters consisting of one or more
characters in the [POSIX] _alnum_ character class (`A-Z`, `a-z` and `0-9`.) or an underscore (`_`). The first character cannot be
a digit. There is no limit on how many characters an identifier may consist of. Identifiers are case-sensitive.

<!-- @} -->
<!-- @{ h3: properties -->
### [Properties](#specifications)

```{.ebnf}
kaml-stream         = { property-assignment | comment } ;
property-assignment = [ typedef ], name, "=", value, [ comment ] ;
```

Properties are the primary building block of a KAML documents. The KAML syntax is primarily about assigning values to properties,
identified by their name. KAML primarily supports character strings and numbers. [Custom types](#custom-types) can be defined with
the `typedef` syntax.

_Note_: No unquoted white space are allowed before or after the assignment operator (`=`).

```{.ebnf}
name                = simple-name | compound-name ;
simple-name         = identifier ;
compound-name       = ( ".",  simplename
                      | [ "." ],  simple-name, { ".", simple-name } ;
```

Property names are either simple or compound. A simple variable name is an identifier. A compound property name is either:

-   an identifier preceded by a dot (`.`)
-   more than one identifier each separated by a dot (`.`) and optionally preceded by a dot.

_Recommendation_: naming conventions vary widely in flavour and type; consider providing utilities to normalise imported and/or
exported property names such that users can continue using the naming conventions to which they are accustomed. For instance
`myPropertyName`, `my-property-name`, `My property name` all map to a _canonical form_ used in KAML: `my_property_name`.

```{.ebnf}
value               = [ scalar | array | dictionary | custom ] ;
```

These are discussed hereafter.

<!-- @} -->
<!-- @{ h3: scalars -->
### [Scalars](#specifications)

Some characters have a special meaning KAML files or the environment in which they are used -- the dollar (`$`) sign for instance.
To remove that meaning, you must quote the character. Single characters can be _escaped_ -- that is they can be preceded with the
backslash character (`\`) which _escapes_ their default meaning. You can quote a string of characters by enclosing them in:

-   literal (single) quotes (`'...'`) to remove the special meaning of all characters except the single quote itself (`'`).

-   grouping (double) quotes (`"..."`) to remove the special meaning of all characters except the dollar sign (`$`), the backslash
    (`\`) and the backtick (````). If the dollar sign (`$`) is not escaped, then property substitution is done inside the double
    quotes.

-   message grouping (double) quotes ('$"..."), the same as grouping quotes except that the string will be looked up in
    a locale-specific message dictionary and replaced if found. The dollar sign (`$`) is always deleted.

    ```{.sh}
    LANG=fr-FR
    greeting=$"Welcome"         # := Bienvenu
    ```

-   ANSI C strings (`$'...'`) to remove the special meaning of all characters except the ANSI C escape sequences:

    | Escape sequence   | Character                                                                     |
    | :---------------- | :---------------------------------------------------------------------------- |
    | `\a`              | Bell character                                                                |
    | `\b`              | Backspace                                                                     |
    | `\f`              | Formfeed                                                                      |
    | `\n`              | Newline                                                                       |
    | `\r`              | Return                                                                        |
    | `\t`              | Tab                                                                           |
    | `\v`              | Vertical tab                                                                  |
    | `\\`              | Backslash                                                                     |
    | `\E`              | Escape character                                                              |
    | `\0x`             | The 8-bit character whose ASCI code is the 1-, 2-, or 3-digit octal number `x`|

<!-- @} -->
<!-- @{ h3: numbers -->
### [Numbers](#specifications)

```
number          := integer | float | boolean ;
integer         := whole-number | arithmetic-expression ;
float           := real-number | arithmentic-expression ;
boolean         := (? truthness expressed as 0 or 1 ?) ;
```

[KAML] provides extensive features to handle scalar values which represent numbers, be they integers or floating point numbers.
#### [Integers](#numbers) <!-- @{ -->

```{.ebnf}
integer             = base10-integer | altbase-integer | arithmetic expression ;
base10-integer      = [ "+" | "-" ], whole-number ;
altbase-integer     = base "#" whole-number ;

whole-number        = (? any non-negative whole number ?) ;
base                = (? a decimal integer between 2 and 64 ?) ;
```

Integers are decimal (i.e. base 10) whole numbers. Positive numbers may be prefixed with a plus operator (`+`). Negative numbers
are prefixed with a minus operator (`-`). KAML allows to assign an integer using an arithmetic base between 2 and 64. A number in
a base greater than 10 uses upper-case and lower-case letters of the alphabet to represent a digit. For instance `16#b` or `16#B`
represents the value 11 in base 16. For bases greater than 36, upper-case and lower-case letters are distinct. The characers `@`
and `_` are the two highest digits. For example `40#b` represents 11, whereas `40#B` represents 37, both in base 40. Anything
after a decimal point is truncated. Leading zeros are dropped.

<!-- @} -->
#### [Floating point numbers](#numbers) <!-- @{ -->

```{.ebnf}
float               = base10-integer, [ decimal-number ], [ exponent ] ;
decimal-number      = decimal-separator, whole-number ;
exponent            = [ "E" | "e" ], whole-number ;

decimal-separator   = (? "." -- the decimal separator is comma in some locales ?) ;
```

Floats should be implemented as IEEE 754 binary64 values. A float consists of an integer part (which follows the same rules as
integer values) optionally followed by a fractional part and/or an exponent part. If both a fractional part and exponent part are
present, the fractional part must precede the exponent part.

Some examples:

```
# fractional
float1=+1.0 float2=3.1415 float3=-0.01

# exponent
float4=5e+22 float5=1e6 float6=-2E-2

# both
float7=6.626e-34
```

Float values `-0.0` and `+0.0` are valid and should map according to IEEE 754 (i.e. the unary minus is remembered.)

_Note_: though desirable, there is currently no support for special float values such as _infinity_, _pi_ or _not a number_.

<!-- @} -->
#### [Booleans](#numbers) <!-- @{ -->

KAML does not provide per se a boolean data type. Nonetheless boolean values and toggles can be easily implemented in several
ways. We describe such implementation here in Korn shell syntax, as this is KAML's reference syntax.

Below are some easy implementation examples. Many others can be imagined. The master recommendation when catering with boolean
values, when these are to be used in arithmetic expressions, is how to you want to match truthness to digital values.

1.  Boolean values expressed as _true_ or _false_ which can be used in arithmetic expressions. This is the Korn-shell notion of
    `TRUE` which is equivalent to decimal 0, anything other is false, and evaluates to 1.

    ```
    enum bool_e=( true false )
    ```
    We can then use the following in [KAML] streams:
    ```
    bool_e shell_boolean=true   # Evaluates to 0
    ```

2.  Boolean value expressed as _true_ or _false_, which can be used in arithmetic expressions, and where `TRUE` is truthness as
    expressed in the C language; that is the reverse logic compared to the previous example.

    ```
    enum cbool_e=( false true )
    ```
    We can then use the following in [KAML] streams:
    ```
    cbool_e clang_boolean=true  # Evaluates to 1
    ```

3.  Boolean values expressed as _true_ or _false_ in a given locale. We use here C language truthness.

    ```
    LANG=fr-FR
    enum togge_e=( $"false" $"true" )
    ```
    We can then use the following in [KAML] streams:
    ```
    toggle_e toggle=faux        # Evaluates to 0
    ```

<!-- @} -->
#### [Epoch time](#numbers) <!-- @{ -->

<span style="color:red">

**This section is work-in-progress. It was ripped from [TOML] with the intent to adapt it for [KAML] using the UNIX _Epoch_
reference point in time.**

</span>

To unambiguously represent a specific instant in time, you may use an [RFC 3339](http://tools.ietf.org/html/rfc3339) formatted date-time with offset.

```{.sh}
odt1=1979-05-27T07:32:00Z
odt2=1979-05-27T00:32:00-07:00
odt3=1979-05-27T00:32:00.999999-07:00
```

The precision of fractional seconds is implementation specific, but at least millisecond precision is expected. If the value
contains greater precision than the implementation can support, the additional precision must be truncated, not rounded.

If you omit the offset from an [RFC 3339](http://tools.ietf.org/html/rfc3339) formatted date-time, it will represent the given
date-time without any relation to an offset or timezone. It cannot be converted to an instant in time without additional
information. Conversion to an instant, if required, is implementation specific.

```{.sh}
ldt1=1979-05-27T07:32:00
ldt2=1979-05-27T00:32:00.999999
```

The precision of fractional seconds is implementation specific, but at least millisecond precision is expected. If the value
contains greater precision than the implementation can support, the additional precision must be truncated, not rounded.

If you include only the date portion of an [RFC 3339](http://tools.ietf.org/html/rfc3339) formatted date-time, it will represent
that entire day without any relation to an offset or timezone.

```{.sh}
ld1=1979-05-27
```

If you include only the time portion of an [RFC 3339](http://tools.ietf.org/html/rfc3339) formatted date-time, it will represent
that time of day without any relation to a specific day or any offset or timezone.

```{.sh}
lt1=07:32:00
lt2=00:32:00.999999
```

The precision of fractional seconds is implementation specific, but at least millisecond precision is expected. If the value
contains greater precision than the implementation can support, the additional precision must be truncated, not rounded.

<!-- @} -->
#### [Arithmetic expressions](#numbers) <!-- @{ -->

When a scalar is explicitly typed as an integer or a float, the right hand side value can be an arithmetic expression, hereafter
simply called _expression_. An expression is a constant, a property, an environment variable, or is constructed with one of the
following operator(s) -- listed here from highest to lowest precedence.

| #.    | Operator                          | Purpose                                                   |
| :---: | :-------------------------------- | :-------------------------------------------------------- |
| (a)   | `( expression )`                  | Overrides precedence rules                                |
| (b)   | `"++" name \| name "++"`          | Prefix/postfix increment of property _name_'s value       |
|       | `"--" name \| name "--"`          | Prefix/postfix decrement of property _name_'s value       |
|       | `"+" expression`                  | Unary plus                                                |
|       | `"-" expression`                  | Unary minus                                               |
|       | `"!" expression`                  | Logical negation                                          |
|       | `"~" expression`                  | Bitwise negation                                          |
| (c)   | `expression "*" expression`       | Multiplication                                            |
|       | `expression "/" expression`       | Division                                                  |
|       | `expression "%" expression`       | Modulo                                                    |
| (d)   | `expression "+" expression`       | Addition                                                  |
|       | `expression "-" expression`       | Subtraction                                               |
| (e)   | `expression "<<" expression`      | Left shift                                                |
|       | `expression ">>" expression`      | Right shift                                               |
| (f)   | `expression "<=" expression`      | Less than or equal to                                     |
|       | `expression ">=" expression`      | Greater than or equal                                     |
|       | `expression "==" expression`      | Equal to                                                  |
|       | `expression "!=" expression`      | Not equal to                                              |
| (g)   | `expression "&" expression`       | Bitwise _AND_                                             |
|       | `expression "^" expression`       | Bitwise _XOR_ (exclusive _OR_)                            |
|       | `expression "\|" expression`      | Bitwise _OR_                                              |
| (h)   | `expression "&&" expression`      | Logical _AND_                                             |
| (i)   | `expression "\|\|" expression`    | Logical _OR_                                              |
| (j)   | `expr. "?" expr. ":" expr.`       | Conditional operator.                                     |
| (k)   | `name "=" expression`             | Assignment.                                               |
| (l)   | `name op "=" expression`          | Compound assignment (`op`: `[*/%^|+-]`,  `<<`, or `>>`)   |
| (m)   | `expression "," expression`       | Comman operator (both expressions are evaluated)          |

Simple expressions can be type as-is -- but without spaces:

```
integer sum=10+11+12
```

More complex expressions should use arithmetic expansion (`$(( ... ))`). Each `$(( ... ))` is replaced by the value of the
arithmetic expression within the double parenthesis.

```
integer     a=$(( RANDOM % 5 ))
integer     b=$(( a * 10 + 256 ))
```
<!-- @} -->
#### [Arithmetic functions](#numbers) <!-- @{ -->

```{.ebnf}
arithmetic-function     = "function(", expression, ")" ;
```

Arithmetic expressions can use arithmetic functions. The following functions are available:

| Name          | Implements                                                    |
| :------------ | :-------------------------------------------------------------|
| `abs`         | Absolute value                                                |
| `acos`        | Arc cosine of angle in radians                                |
| `asin`        | Arc sine                                                      |
| `atan`        | Arc tangent                                                   |
| `cos`         | Cosine                                                        |
| `cosh`        | Hyperbolic cosine                                             |
| `exp`         | Exponential with base `e` where `e ~ 2.178`                   |
| `int`         | Greatest integer less than or equal to value of `expression`  |
| `log`         | Logarithm                                                     |
| `sin`         | Sine                                                          |
| `sinh`        | Hyperbolic sine                                               |
| `sqrt`        | Square root                                                   |
| `tan`         | Tangent                                                       |
| `tanh`        | Hyperbolic tangent                                            |

<!-- @} -->

<!-- @} -->
<!-- @{ h3: arrays --->
### [Arrays](#specifications)

An array is a property that can store multiple values, where each value is associated with a subscript.

There are two types of arrays -- indexed arrays and associative arrays. The subscript for indexed arrays is an arithmetic
expression; the subscript for an associative array is an arbitrary string. You can specify a subscript with any property using the
array syntax notation: `name[subscript]`. The property for an indexed array can be any [arithmetic
expression](#arithmetic-expressions) that evaluates between 0 and some implementation-defined value that is at least 4095. The
subscript of an associative array can be any string.

You can assign values to array elements individually with property assignment commands. You can assign values to indexed array
elements sequentially, starting at 0, using the compound assignment `name=( value ... )`. You can assign values to an indexed
array using the compound assignment `hash name=( [subscript]=value ... )`.

Alternatively you can assign a list of values to an array sequentially: `name[subscript]=value`. You also the subscript-less
syntax  for indexed arrays `name+=( value)`; the equivalent form for associative arrays requires the subscript:
`name+=( [subscript]=value )`.


```
digits=( one two three four )
digits[4]=five
digits+=( six seven eight nine ten)

alphabet=( [a]=alpha [b]=bravo [c]=charlie )
alphabet[d]=delta
alphabet+=( [e]=echo [f]=foxtrot ... )
```

_Note_: using _Perlish_ naming conventions, we interchangeably use the term _hash_ for associative arrays, and the bare word
_array_ for indexed arrays. For greater legibility of KAML files, the singular form of these alternate names can be used to
specify the type of a property.

```
array digits=( one two three ... )
hash alphabet=( [a]=alpha [b]=bravo [c]=charlie ...)
```

You can refer to previously defined properties (or environment variables) in right hand side values using the conventional UNIX
brace syntax:

```
colour=([apple]=red [grape]=purple [banana]=yellow)
prefered_colour=${colour[banana]}
```

_Note_: Omitting the braces is not a syntax error, but yield a different result as expansion will be applied to the first
identifier in the name, here `$colour`; which, if it doesn't exist, will be silently replaced with an empty string. In Korn shell
environments you can force the shell to complain using the `set -u` option whenever it encounters a variable (or property) that
has not been set.

When you reference an array without specifying a subscript, then the subscript of the first element in the array is assumed. The
special subscripts `@` and `*` refer to all the elements in the array. As for regular shell variables, the `!` operand can be used
to expand the list of subscripts in an array. The size operator `#` can be used in place of `!` to obtain the number of elements
in an array. Using our previous example, this can be summarised as:

```
${colour[apple]}    # := red
${colour[]}         # := red
${!colour[@]}       # := apple banana grape
${colour[@]}        # := red yellow purple
${#colour[@]}       # := 3
$colour[apple]      # := [apple] (if colour is undefined)
```
_Note_: The associative array is automatically sorted alphabetically.




69-70 132 136 144 179 183 188 189 190 215 323 

to assign multiple elements to an associative array.

Arrays are square brackets with values inside. Whitespace is ignored. Elements
are separated by commas. Data types may not be mixed (different ways to define
strings should be considered the same type, and so should arrays with different
element types).

```{.sh}
arr1=( 1 2 3 )
arr2=( red yellow green )
arr3=( ( 1 2 ) (3 4 5) )
arr4=( all strings are the same type)
arr5=( ( 1 2 ) (a b c) )
```

<!-- @} -->
<!-- @{ h3: dictionaries -->
### [Dictionaries](#specifications)

A dictionary is a property whose name consists of more than one identifier. A compound assignment is an assignment of the
form:

```{.sh}
name=( word ... )
```

which is used for array assignment as described earlier, or

```{.sh}
name=( assignment ... )
```

where `assignment` can be a _simple assignment_ or a _compound assignment_. For each `assignment` in the list, the property
`name.assignment` is assigned to. In addition, the value of `name`, `$name`, consists of a list of assignments enclosed in
parantheses that is equivalent to an assignment for all compound properties whose name begins with `name`.

Once the compound property `name` has been created, you can operate on each member independently. Properties of the form `name`,
created or deleted, will be created or deleted from the compound property `name`.

```{.sh}
picture=(
    bitmap=$PICTDIR/fruit
    colour=([apple]=red [grape]=purple [banana]=yellow)
    size=( typeset -E x=8.5 y=11.0)
)
```

In JSON land, that would give you the following structure.

```{.json}
{
    "picture": {
        "bitmap": "/path/to/pict/dir/fruit",
        "colour": {
            "apple": "red",
            "grape": "purple",
            "banana": "yellow"
        },
        "size": {
            "x": 8.5,
            "y": 11.0
        }
    }
}
```

<!-- @} -->
<!-- @{ h3: custom types -->
### [Custom types](#specifications)

[KAML] allows for the definition of custom data types. Since the official linter for [KAML] is the Korn shell, we represent the
definition of custom data types in this section based on Korn shell capabilities, in particular the `typeset` and `enum` commands.

#### Data types <!-- @{ -->

The `typeset` command is the primary Korn shell interface to define custom data types. Being a UNIX shell command, data type are
declare through command line interface options. We use the same syntax in [KAML] files. Commonly used data types have an
associated alias name (e.g. `integer` or `float`).

###### Uppercase (`-u`)

Change lower-case characters to upper-case when the property is expanded.

```
typeset -u x=abc    # := ABC
```

###### Lowercase (`-l`)

Change upper-case characters to lower-case when the property is expanded.

###### Floating point, scientific notation (`-E` or `-En`)

Evaluate the property's value as an arithmetic floating point expression. Output should match the `%g` format of the C language
_printf(3)_ function. The `n` in `En` is the number of significant digits; the default is 10.

You can use the predefined `float` alias to declear floating point variables.

###### Floating point, fixed precision (`-F` or `-Fn`)

Evaluate the property's value as an arithmetic floating point expression. Output should match the `%f` format of the C language
_printf(3)_ function. The `n` in `En` is the number of significant digits; the default is 10.

###### Integer (`-i` or `-ibase`)

Evaluate the property's value as an arithmetic integer expression. The `base` is the integer's arithmetic base, and can be
a decimal integer between 2 and 64.

You can use the predefined `integer` to declare integer variables.

```
integer x=6
typeset -i8 y=x+x # := 8#14
```

###### Associative array (`-A`)

Define an associative array, as opposed to an indexed array. The subscript for an associative array element is an arbitrary
string.

###### Left-justified (`-L` or `-Lwidth`)

Left justify the character's of the property's value to fit `width` and put trailing spaces, tf needed. The `width` is any
positive number. If unspecified, use the number of characters of the first value assigned to the property.

If you assign a value that is too big to fit `width`, the value will be truncated to match the specified width.

###### Strip leading zeros (`-LZ` or `-LZwidth`)

This is similar to the left justification attribute (above), except that upon expansion leading zeros at the left are stripped.

```
typeset -LZ3 x=abcd         # Expands to 'abc'
typeset -LZ3 y=03           # Expands to '3  '
typeset -LZ3 z=00abcd       # Expands to 'abc'
```

###### Right justified (`-R` or `-Rwidth`)

Right justify the characters to fit `width`, putting leading spaces at the left, if needed, to fill `width`. The `width` is any
positive number. If unspecified, use the number of characters of the first value assigned to the property.

If you assign a value that is too big to fit `width`, the value will be truncated to match the specified width.

```
typeset -R3 x=abcd          # Expands to 'bcd'
typeset -R3 y=3             # Expands to '  3'
```

###### Zero-filled (`-RZ` or `-RZwidth`, alternatively `-Z` or `-Zwidth`)

This is similar to the right justification attribute (above). However up expansion leading zeros are prepended at the left.

```
typeset -Z3 x=abcd          # Expands to 'bcd'
typeset -Z3 y=3             # Expands to '003'
```

###### Read-only (`-r`)

When a property has the read-only attribute set, any attempt to change the property's value in subsequent processing should raise
a (fatal) exception. Once set, the read-only attribute cannot be unset.

You can set use the `readonly` or `typeset -r` to set this attribute.

```
readonly foo=bar
foo=nobar                   # Raises exception 'foo: is read only'
```

<!-- @} -->
#### Enumerations <!-- @{ -->

The Korn shell `enum` command allows to create enumeration types that can be used in [KAML] streams.

```
enum [ options ] typename=( value ... )
```

`enum` is a declaration command that creates an enumeration type *typename* that can only store any one of the values in the
indexed array variable *typename*. See the discussion on [booleans](#booleans) for examples.

<!-- @} -->

<!-- @} -->
<!-- @{ h3: comments -->
### [Comments](#specifications)

```{.ebnf}
comment                 = plain-comment | special-comment ;
plain-comment           = "#",  comment-string, newline ;
special-comment         = "#!", comment-string, newline ;
comment-string          = (? any character except newline ?)
```

KAML streams can include comments. Comments are not preserved. A comment is introduced by the hash symbol (`#`) which marks the
rest of a line as a comment. If the hash symbol is immediately followed by an exclamation mark (`!`), the comment targets
literate programming and embedded documentation.

```
# This is a full-line comment
name="value" # This is a comment at the end of a line
```

Plain comments are dropped upon processing a KAML stream. Special comments can be extracted separately to dynamically build the
_man(1)_ page or documentation for the KAML stream. Embedded documentation is written in [Markdown] and can contain [Doxygen] like
commands to structure the documentation content.

```
#! @param colour
#! @brief a list of colours for demonstration purposes
#! The _colour_ property is an **associative array**.

colour=([apple]=red [grape]=purple [banana]=yellow)
```

_Recommendation_: There are many [Markdown] flavours, despite the recent [CommonMark] initiative to provide some standardisation.
We recommend standardising on [Pandoc] flavoured Markdown syntax which is rich and extensible. [Pandoc] exposes the abstract
syntax tree of the parsed content allowing easy handling of embedded custom [Doxygen]-like commands.

When the first 16 bits of a [KAML] stream (i.e. the UNIX _magic_ number) are the special comment prefix (`#!`), the comment is
handled differently. The comment can either be a version string or a [shebang]. If the magic number is immediately followed by the
upper-case token `KAML`, then the comment describes the version of the subsequent [KAML] stream.

```
#! KAML1.0
```

Otherwise the special comment is assumed to be a UNIX [shebang]. A minimal example might be:

```
#!/bin/cat
output="Hello world"
```

By supporting shebangs, [KAML] allows _inside out_ integration rather than the traditional _outside in_ model. Akin to _object
orientation_ in programming, this model allows to create a context aware middleman that interacts between multiple programs,
pre-processing the [KAML] data such that each participating program collects the needed information in the format supported by
that program, this could be [JSON], [YAML], [XML] or other standard or proprietary formats.

```
#! /usr/bin/awk '/^#!/,/^---/'
```

A common use case is the practice to embed metadata and character data in a same file. Consider the `<HEAD>` section of HTML
documents or the [YAML] header that is commonly embedded in Markdown documents. The Markdown document potentially being the
source document from which the HTML document is produced. Both documents will then share common metadata which will be used by
various programs to enact the life cycles of these documents.

```
#! /usr/df/bin/blog-manager
```

By using inside out integration, the middle manager becomes the _single point of contact_ to access and transform the [KAML] data.
No central store, or configuration database, is required, and data can be translated into multiple formats, combined, split, or
merged with other data.

<!-- @} -->
## About
<!-- @{ toc -->

<small>

Sub-sections
:   [Comparison with other formats](#comparison-with-other-formats) |
    [Get involved](#get-involved)

Previous sections
:   [Specifications](#specifications), [Top](#kaml-aint-markup-language)

</small>

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
variables_ syntax available in the Korn shell since the mid 1980s. [KAML] came to life in Korn shell pretty much for the same reasons
as JSON appeared in Javascript; to allow easy interchange of structured data sets. Indeed an often overlooked feature of Korn
shell is that it natively supports classes, type definitions, enumerations and the so-called compound variables, called
_dictionaries_ in this specification and which compare to C language `struct` declarations.

[KAML] is easier to read by humans than [JSON] and tagged markups inherited form the [SGML] syntax. It does not reach the
readibility of [YAML] which was a design consideration. The slightly more verbose syntax of [KAML] will probably remain unchanged
as long as the pre-requisite for [KAML] to be natively understood by the Korn shell remains. Korn shell (and the associated
`libast` C language library) are the reference implementation for [KAML]. Should we one day decide to write a parser for the
shell, then extra readability would be a high priority. This is not however on the road map.

[KAML] is immediately available to most, if not all, programming language without writing a single line of parsing code in the
target programming language, just a bit of shell scripting wizardry. Samples will be added to this specification as both proof of
concept and getting started examples.

<!-- @} -->
<!-- @{ get involved -->
#### [Get Involved](#about)

Documentation, bug reports, pull requests, and all other contributions are welcome!

<!-- @} -->
<!-- @{ bookmarks -->

[ASN-1]:        https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One
[Doxygen]:      https://en.wikipedia.org/wiki/Doxygen
[EBNF]:         https://en.wikipedia.org/wiki/Extended_Backus–Naur_form
[INI]:          https://en.wikipedia.org/wiki/INI_file
[JSON]:         https://en.wikipedia.org/wiki/JSON
[KAML]:         https://github.com/ISLEcode/KAML
[Markdown]:     https://en.wikipedia.org/wiki/Markdown
[CommonMark]:   https://en.wikipedia.org/wiki/Markdown#CommonMark
[Open Group]:   http://www.opengroup.org
[POSIX]:        https://en.wikipedia.org/wiki/POSIX
[Pandoc]:       https://en.wikipedia.org/wiki/Pandoc
[SGML]:         https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language
[SheBang]:      https://en.wikipedia.org/wiki/Shebang_(Unix)
[TOML]:         https://en.wikipedia.org/wiki/TOML
[XML]:          https://en.wikipedia.org/wiki/XML
[XSLT]:         https://en.wikipedia.org/wiki/XSLT
[YAML]:         https://en.wikipedia.org/wiki/YAML

<!-- vim: set nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb :-->
