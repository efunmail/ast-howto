## [ast-grep] RENAME Tag Attributes

- Use-case: **Rename** `v-for` to `x-for` - (re: converting *Vue* to **AlpineJS**)

[Playground...](https://ast-grep.github.io/playground.html#eyJtb2RlIjoiQ29uZmlnIiwibGFuZyI6Imh0bWwiLCJxdWVyeSI6IiIsInJld3JpdGUiOiIiLCJjb25maWciOiJpZDogcG4td2lwXG5sYW5ndWFnZTogaHRtbFxuXG5ydWxlOlxuICBraW5kOiBhdHRyaWJ1dGVfbmFtZSAgIyAvLyBmcm9tIFRyZWVTaXR0ZXJcbiAgcGF0dGVybjogJEFcbiAgcmVnZXg6IFwidi0oZm9yfGluaXQpXCIgIyAvLyBUT0RPOiBtb3JlLi4uXG50cmFuc2Zvcm06ICMgLy8gaHR0cHM6Ly9naXRodWIuY29tL2FzdC1ncmVwL2FzdC1ncmVwL2Rpc2N1c3Npb25zLzQ3N1xuICBDSEFOR0VEOlxuICAgIHJlcGxhY2U6XG4gICAgICBzb3VyY2U6ICRBXG4gICAgICByZXBsYWNlOiBcInYtKGZvcnxpbml0KVwiICMgLy8gU0FNRSBhcyBhYm92ZVxuICAgICAgYnk6ICd4LSQxJ1xuZml4OlxuICAkQ0hBTkdFRFxuIiwic291cmNlIjoiPHRlbXBsYXRlPlxuPHVsPlxuICA8bGkgcC1uPVwiaGlcIiB2LWZvcj1cIml0IGluIGl0ZW1zXCIgdi1pbml0PVwiY29uc29sZS5sb2coJ2hpICcpXCI+XG4gICAge3sgaXQuYWdlIH19XG4gIDwvbGk+XG48L3VsPlxuPHA+e3sgZm4oMTIzKSB9fXt7IG1zZyB9fXt7IG5hbWUgfX08L3A+XG48L3RlbXBsYXRlPlxuIn0=)

```yaml
id: pn-wip
language: html

rule:
  kind: attribute_name  # // from TreeSitter
  pattern: $A
  regex: "v-(for|init)" # // TODO: more...
transform: # // https://github.com/ast-grep/ast-grep/discussions/477
  CHANGED:
    replace:
      source: $A
      replace: "v-(for|init)" # // SAME as above
      by: 'x-$1'
fix:
  $CHANGED
```

- Example HTML:

```html
<template>
<ul>
  <li p-n="hi" v-for="it in items" v-init="console.log('hi ')">
    {{ it.age }}
  </li>
</ul>
<p>{{ fn(123) }}{{ msg }}{{ name }}</p>
</template>
```

----

## MULTIPLE Rules (in YAML file)

[Rewrite Code](https://ast-grep.github.io/guide/rewrite-code.html#using-fix-in-yaml-rule)

> You can have multiple rules in one YAML file
> by using the YAML document separator `---`.

----

## RENAME Tags

[Playground...]()

```yaml
id: pn-vue-script
language: html
rule:
  pattern: <script>$$$A</script>
fix: <TODO:SCRIPT>$$$A</TODO:SCRIPT>

---

id: pn-vue-template
language: html
rule:
  pattern: <template lang>$$$A</template>
fix: <TODO:BODY>$$$A</TODO:BODY>
```

- Example HTML:

```html
<script>
var x = 123
function f(n) { return n }
</script>

<template lang="pug">
div
  p Hello
</template>

<template lang="html">
<div>
  <p>Hello</p>
</div>
<template>
  <p>Hiya!</p>
</template>
</template>
```
