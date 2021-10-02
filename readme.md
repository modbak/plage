# Plage Specification

PLAGE ( **PubLic Abstract Grammar Expression** ) is a low-level interface for custom grammar expression forms.

You need to consider:

- all of the definitions are in scope of this specification. for example the definition of the language in here is refers to language in **plage**, and not definition of the language in **general**

- _`abstract`_ element fully or partially must be defined in implementations

- _`ignore`_ element is idle and would not produce any token

- _`optional`_ element can be ommited by the implementation

<br>

## Source _`<source>`_

**Source** is a string that contains list of one or more `language`.

```xml
<source> : <languages>
```
```xml
<languages> : <language> <languages> | <language>
```

every `language` must starts at the begining of a new line.



<br>

## Blank Line _`<blank>` `ignore`_

`blank` line is a line that is `empty` or only contains `whitespaces` and `comment`.

they can make `source` more readable by spacing between elements.

they can be used between the lines of a **multiline language** as well.

```xml
<blank> : <whitespaces> <comment> | <whitespaces> | <comment> | <empty>
```



<br>

## Whitespaces _`<whitespaces>`_

`Whitespaces` is refers to all the **whitespaces** that **continiusly repeated**.

```xml
<whitespaces> : <whitespace> <whitespaces> | <whitespace>
```

### Whitespace _`<whitespace>`_

`whitespace` can be one of `space` or `tab`.

```xml
<whitespace> : <space> | <tab>
```

### Space _`<space>`_

`space` is refers to space unicode. (`u+0020`)

### Tab _`<tab>`_

`tab` is refers to horizontal tab unicode. (`u+0009`)



<br>

## Comment _`<comment>` `optional` `ignore`_

Comments are optional text and informations.

```xml
<comment> : <comment-marker> <comment-content> | <comment-marker>
```

### Comment Marker _`<comment-marker>` `abstract`_

comment marker is the sign of starting the **comment**.

### Comment Content _`<comment-content>`_

content is string of unicode characters except `control-characters` (`u+0000` to `u+001F`). it continues till meet the first `newline` indicator or end of the source string.



<br>

## Newline _`<newline>`_

`newline` is an indicator at the end of every line.

```xml
<newline> : <CR> <LF> | <CR> | <LF>
```

### Carriage Return _`<CR>`_

`CR` is refers to carriage return unicode. (`u+000D`)

### Line Feed _`<LF>`_

`LF` is refers to line feed unicode. (`u+000A`)



<br>

## Language _`<language>`_

`language` is `grammar` representation of a **language** via `syntaxes`.

```xml
<language> : <language-definition> | <language-declaration>
```

### Language Definition _`<language-definition>`_

```xml
<language-definition> : <declaration> <delimiter> <grammar> | <declaration> <grammar>
```

### Language Declaration _`<language-declaration>` `optional`_

To declare languages that cannot be represented via `grammar`.

```xml
<language-declaration> : <declaration>
```



<br>

## Delimiter _`<delimiter>` `abstract` `optional`_

Delimiter is an optional separator between `declaration` and the `grammar`.



<br>

## Declaration _`<declaration>`_

`declaration` is the name of the `language` and may lead and followed by optional **modifiers** and **attributes**.

```xml
<declaration> : <MA> <name> <MA> | <MA> <name> | <name> <MA> | <name>
```

### Modifier and Attribute _`<MA>` `abstract` `optional`_

Language declarations can have modifiers and attributes.



<br>

## Name _`<name>` `abstract`_

`name` is a pointer to the language. there is no restriction over **naming rules**.



<br>

## Grammar _`<grammar>` `abstract`_

`Grammar` is list of syntaxes of the language.

```xml
<grammar> : <inline-syntaxes> | <multiline-syntaxes>
```

### Inline

To separating different syntaxes in one line we can use **alternative marker** between them :

```xml
<inline-syntaxes> : <syntax> <alt> <inline-syntaxes> | <syntax>
```

### Multiline

Syntaxes can also seperated in multiple lines but they have to have an **indent marker** before each **line** :

```xml
<multiline-syntaxes> : <inline-syntaxes> <syntaxlines> | <syntaxlines>
```
```xml
<syntaxlines> : <syntaxline> <syntaxlines> | <syntaxline>
```
```xml
<syntaxline> : <newline> <indent> <inline-syntaxes>
```

### Alternative Marker _`<alt>` `abstract` `optional`_

The **marker** that indicates that the syntax after it, is an alternative for the syntax of before it.

### Indent _`<indent>` `abstract`_

`Indent` is a leading sign at the start of every **syntaxlines**. it can contains non-whitespace characters as well.



<br>

## Syntax _`<syntax>`_

`Syntax` is refers to **abstract rules** to define the structure of the language.



<br>

## Implementation

To implement a grammar form based on plage you can follow this guide [here](./implementation-guide).
