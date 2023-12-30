### Selectors

Minimize selectors tightly coupled to the DOM. Consider adding a class to the elements
you want to match when your selector exceeds 3 structural pseudo-classes, descendant or
sibling combinators.

```css
/* bad */
div:first-of-type :last-child > p ~ *

/* good */
div:first-of-type .info
```

Avoid overloading your selectors when you don't need to.

```css
/* bad */
img[src$=svg], ul > li:first-child {
  opacity: 0;
}

/* good */
[src$=svg], ul > :first-child {
  opacity: 0;
}
```