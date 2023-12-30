### Flow

Don't change the default behavior of an element if you can avoid it. Keep elements in the
natural document flow as much as you can. For example, removing the white-space below an
image shouldn't make you change its default display:

```css
/* bad */
img {
  display: block;
}

/* good */
img {
  vertical-align: middle;
}
```

Similarly, don't take an element off the flow if you can avoid it.

```css
/* bad */
div {
  width: 100px;
  position: absolute;
  right: 0;
}

/* good */
div {
  width: 100px;
  margin-left: auto;
}
```
