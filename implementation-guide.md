# Plage Implementation Guide

Plage is abstract structure for grammar forms. it doesn't matter rules are based on RegExp or any other custom form, it's easier to design them on top of plage and this is a simple guide to doing that :



### 1. _`<name>`_

First specify rules for identifier of the languages.
For example :

- minimum length of the names
- available characters that could be used in the name
- whether it must to be surounded by symbols or not
- prefix or postfix
- etc



### 2. _`<comment>`_

Comments are optional so the form can support it or not. if your going to support it you have to consider you can only define **single-line-comment** without any **comment-end-marker**. (comments will terminated at end of the line or end of the file)



### 3. _`<comment-marker>`_

Define the lexial shape of the comment starter. for example in `javascript` we use `//` as single line comment marker.



### 4. _`<language-declaration>`_

Choose whether the form supports languages that doesn't have `<grammar>`.



### 5. _`<delimiter>`_

Forms can support delimiter between `declaration` and `grammar`. they can also support for multiple delimiters for different type of languages as well. an example of delimiter can be `::=` like in `BNF`.



### 6. _`<MA>`_

Before and after the identifier of the languages, forms can add **modifiers** and **attributes** to that language.

For example, identifier can comes after a modifier keyword that defines the type of the language or like xml tags adding attributes to `language`.



### 7. _`<grammar>`_

For the grammar section, forms can support both `inline` and `multiline` or `both` of them.

Also it can have specific rules over these two, for example you can specify in multiline grammar, only single syntax in each line is supported or any more complex form.



### 8. _`<alt>`_

Alternative marker is not required in forms that only support single `syntax` at a line. but it's an important delimiter to separate syntaxes in single line. as an example you can use `|` character as marker.



### 9. _`<indent>`_

Indent is usully a `<tab>` or few `<space>` but indent can also contains symbol as well, for example you can define indent like bellow:

```xml
<indent> : <space> <space> <space> <space> <alt>
```



## Example

To see plage in action, you can check [Rigid Form]() as an implementaion of plage.
