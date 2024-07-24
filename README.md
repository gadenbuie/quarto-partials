# Partial content templates for Quarto


## Installing

``` bash
quarto add gadenbuie/quarto-partials
```

This will install the extension under the `_extensions` subdirectory. If
you’re using version control, you will want to check in this directory.

Once you’ve install the extension, you can use the
`{{< partial file ... >}}` shortcode to include partial content from
`file` in your [Quarto document](https://quarto.org)!

## Example

Use the `{{< partial file ... >}}` shortcode to include partial content
from `file` in your Quarto document. The partial content can use
[mustache templating syntax](https://mustache.github.io) and you can
provide named key-value pairs in the shortcode to provide the template
data.

For example, `_hello.md` contains the following content

> <div class="code-with-filename">
>
> **\_hello.md**
>
> ``` markdown
> {{< include _hello.md >}}
> ```
>
> </div>

and we can include the partial, providing our own value for
`{{ name }}`:

> ``` markdown
> {{< partial _hello.md name="weary traveler" >}}
> ```
>
> Hello, weary traveler!

You can also include the partial data in the frontmatter of your
document, using the `partial-data` key, e.g. 

> ``` yaml
> partial-data:
>   name: "friend"
> ```
>
> ``` markdown
> {{< partial _hello.md >}}
>
> Or used inline: To you I say "{{< partial _hello.md >}}"
> ```
>
> Hello, friend!
>
> Or used inline: To you I say “Hello, friend!”

Alternatively, the second argument of the shortcode can point to a
custom key in your YAML frontmatter, e.g.

> ``` yaml
> my-data:
>   friends:
>     name: amigo
> ```
>
> ``` markdown
> {{< partial _hello.md my-data.friends >}}
> ```
>
> Hello, amigo!

Another, possibly less convenient, option is to provide JSON in the
shortcode data. Any key-value pair that starts with `{` or `[` will be
parsed into a JSON object or array.

Note that the file type affects the output. The next example, in
addition to using JSON data, uses a `.qmd` file to render the output as
Quarto-processed markdown.

> <div class="code-with-filename">
>
> **\_hello_first_last.qmd**
>
> ``` markdown
> ::: {.callout-tip title="Hi there!"}
> {{#person}}
> Hello, {{ honorific }} {{ name.first }} {{ name.last }}!
> {{/person}}
> :::
> ```
>
> </div>
>
> ``` markdown
> {{< partial _hello_first_last.qmd person='{"honorific": "Mr.", "name": {"first": "Garrick", "last": "Aden-Buie"}}' >}}
> ```
>
> > [!TIP]
> >
> > ### Hi there!
> >
> > Hello, Mr. Garrick Aden-Buie!

Finally, remember that you can use the full power of [mustache
templating](https://mustache.github.io)! The next example creates a
markdown list from an array of my favorite fruits.

> <div class="code-with-filename">
>
> **\_favorite_fruits.md**
>
> ``` markdown
> These are a few of my favorite fruits:
>
> {{#fruits}}
> - {{.}}
> {{/fruits}}
> ```
>
> </div>
>
> ``` markdown
> {{< partial _favorite_fruits.md fruits='["apple", "banana", "coconut", "mango"]' >}}
> ```
>
> These are a few of my favorite fruits:
>
> - apple
> - banana
> - coconut
> - mango

## Thanks!

`partials` embeds [lustache](https://github.com/Olivine-Labs/lustache),
a pure-Lua implementation of [mustache](https://mustache.github.io).
Thanks to the authors and contributors of these projects!

Thanks, as always, to the developers of [Quarto](https://quarto.org)!
