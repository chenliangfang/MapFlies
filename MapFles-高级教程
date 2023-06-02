#### Tags

In order to manage paragraphs, table rows, table columns, runs, special syntax has to be used:

{%p jinja2_tag %} for paragraphs
{%tr jinja2_tag %} for table rows
{%tc jinja2_tag %} for table columns
{%r jinja2_tag %} for runs

By using these tags, python-docx-template will take care to put the real jinja2 tags (without the p, tr, tc or r) at the right place into the document’s xml source code. In addition, these tags also tell python-docx-template to **remove** the paragraph, table row, table column or run where the tags are located.

For example, if you have this kind of template:

{%p if display_paragraph %}
One or many paragraphs
{%p endif %}

The first and last paragraphs (those containing `{%p ... %}` tags) will never appear in generated docx, regardless of the `display_paragraph` value.

Here only:

One or many paragraphs

will appear in generated docx if `display_paragraph` is True, otherwise, no paragraph at all are displayed.

**IMPORTANT :** Always put space after a starting tag delimiter and a space before the ending one :

Avoid:

{%if something%}
{%pif display_paragraph%}

Use instead:

{% if something %}
{%p if display_paragraph %}

**IMPORTANT** : Do not use `{%p`, `{%tr`, `{%tc` or `{%r` twice in the same paragraph, row, column or run. Example :

Do not use this:

{%p if display_paragraph %}Here is my paragraph {%p endif %}

But use this instead in your docx template:

{%p if display_paragraph %}
Here is my paragraph
{%p endif %}

This syntax is possible because MS Word considers each line as a new paragraph (if you do not use SHIFT-RETURN).

#### Display variables

As part of jinja2, one can used double braces:

{{ <var> }}

if `<var>` is a string, `\n`, `\a`, `\t` and `\f` will be translated respectively into newlines, new paragraphs, tabs and page breaks

But if `<var>` is a [RichText](https://docxtpl.readthedocs.io/en/latest/#richtext) object, you must specify that you are changing the actual ‘run’:

{{r <var> }}

Note the `r` right after the opening braces.

**VERY IMPORTANT :** Variables must not contains characters like `<`, `>` and `&` unless using [Escaping](https://docxtpl.readthedocs.io/en/latest/#escaping)

**IMPORTANT :** Always put space after a starting var delimiter and a space before the ending one :

Avoid:

{{myvariable}}
{{rmyrichtext}}

Use instead:

{{ myvariable }}
{{r myrichtext }}

#### Comments

You can add jinja-like comments in your template:

{#p this is a comment as a paragraph #}
{#tr this is a comment as a table row #}
{#tc this is a comment as a table cell #}

See tests/templates/comments_tpl.docx for an example.

#### Split and merge text[

- You can merge a jinja2 tag with previous line by using `{%-`
- You can merge a jinja2 tag with next line by using `-%}`

A text containing Jinja2 tags may be unreadable if too long:

My house is located {% if living_in_town %} in urban area {% else %} in countryside {% endif %} and I love it.

One can use *ENTER* or *SHIFT+ENTER* to split a text like below, then use `{%-` and `-%}` to tell docxtpl to merge the whole thing:

My house is located

{%- if living_in_town -%}

  in urban area

{%- else -%}

  in countryside

{%- endif -%}

  and I love it.

**IMPORTANT :** Use an unbreakable space (*CTRL+SHIFT+SPACE*) when a space is wanted at line beginning or ending.

**IMPORTANT 2 :** `{%- xxx -%}` tags must be alone in a line : do not add some text before or after on the same line.

#### Escaping delimiters[](https://docxtpl.readthedocs.io/en/latest/#escaping-delimiters "Permalink to this headline")

In order to display `{%`, `%}`, `{{` or `}}`, one can use:

{*%, %*}, {*{ or  }*}

#### Tables[](https://docxtpl.readthedocs.io/en/latest/#tables "Permalink to this headline")

#### Spanning[](https://docxtpl.readthedocs.io/en/latest/#spanning "Permalink to this headline")

You can span table cells horizontally in two ways, by using `colspan` tag (see tests/dynamic_table.py):

{% colspan <var> %}

<var> must contain an integer for the number of columns to span. See tests/test_files/dynamic_table.py for an example.

You can also span horizontally within a for loop (see tests/horizontal_merge.py):

{% hm %}

You can also merge cells vertically within a for loop (see tests/vertical_merge.py):

{% vm %}

#### Cell color[](https://docxtpl.readthedocs.io/en/latest/#cell-color "Permalink to this headline")

There is a special case when you want to change the background color of a table cell, you must put the following tag at the very beginning of the cell:

{% cellbg <var> %}

<var> must contain the color’s hexadecimal code *without* the hash sign

## RichText

When you use `{{ <var> }}` tag in your template, it will be replaced by the string contained within var variable. BUT it will keep the current style. If you want to add dynamically changeable style, you have to use both : the `{{r <var> }}` tag AND a `RichText` object within var variable. You can change color, bold, italic, size, font and so on, but the best way is to use Microsoft Word to define your own *character* style ( Home tab -> modify style -> manage style button -> New style, select ‘Character style’ in the form ), see example in tests/richtext.py Instead of using `RichText()`, one can use its shortcut : `R()`

The `RichText()` or `R()` offers newline, new paragraph, and page break features : just use `\n`, `\a`, `\t` or `\f` in the text, they will be converted accordingly.

There is a specific case for font: if your font is not displayed correctly, it may be because it is defined only for a region. To know your region, it requires a little work by analyzing the document.xml inside the docx template (this is a zip file). To specify a region, you have to prefix your font name this that region and a column:

ch = RichText('测试TEST', font='eastAsia:微软雅黑')

**Important** : When you use `{{r }}` it removes the current character styling from your docx template, this means that if you do not specify a style in `RichText()`, the style will go back to a microsoft word default style. This will affect only character styles, not the paragraph styles (MSWord manages this 2 kind of styles).

**IMPORTANT** : Do not use 2 times `{{r` in the same run. Use RichText.add() method to concatenate several strings and styles at python side and only one `{{r` at template side.

**Important** : `RichText` objects are rendered into xml *before* any filter is applied thus `RichText` are not compatible with Jinja2 filters. You cannot write in your template something like `{{r <var>|lower }}`. Only solution is instead to do any filtering into your python code when creating the `RichText` object.

### Hyperlink with RichText

You can add an hyperlink to a text by using a Richtext with this syntax:

context = { 'mylisting':Listing('the listing\nwith\nsome\nlines \a and some paragraph \a and special chars : <>&') }

in your docx template just use `{{ mylisting }}`

With `Listing()`, you will keep the current character styling (except after a `\a` as you start a new paragraph).
