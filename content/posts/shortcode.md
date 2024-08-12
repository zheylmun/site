+++
title = "Shortcode Example"
date = "2024-06-14"

[taxonomies]
tags=["example"]
+++


## Note

Here is an example of the `note` shortcode:

This one is static!
{{ note(header="Note!", body="This blog assumes basic terminal maturity") }}

This one is clickable!
{{ note(clickable=true, hidden = true, header="Quiz!", body="The answer to the quiz!") }}

Syntax:

```markdown
{{/* note(header="Note!", body="This blog assumes basic terminal maturity") */}}
{{/* note(clickable=true, hidden = true, header="Quiz!", body="The answer to the quiz!") */}}
```

You can also use some HTML in the text:
{{ note(header="Note!", body="<h1>This blog assumes basic terminal maturity</h1>") }}

Literal shortcode:

```markdown
{{/* note(header="Note!", body="<h1>This blog assumes basic terminal maturity</h1>") */}}
```

Pretty cool, right?

Finally, we have center
{{ note(center=true, header="Centered Text", body="This is centered text") }}

```markdown
{{/* note(center=true, header="Centered Text", body="This is centered text") */}}
```

It works good enough for me!
