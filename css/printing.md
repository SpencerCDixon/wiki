# Print Mode CSS

Very useful tip for adjust print styles is to activate chromes 'print'
media query.  The setting is under 'Rendering' at the bottom:

![Print view](./assets/print-mode.png)

Additionally, it can be useful to surround all div's in a black border to see
where elements are in print mode:

```css
@media print {
  div { border: 1px solid black;}
}
```
