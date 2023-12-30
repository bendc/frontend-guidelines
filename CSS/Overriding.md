### Overriding

Overriding styles makes selectors and debugging harder. Avoid it when possible.

```css
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```