## Rename HTML attributes

- Use-case: **Rename** `v-for` to `x-for` - (re: converting *Vue* to **AlpineJS**)

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
