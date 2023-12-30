### Accessibility

Accessibility shouldn't be an afterthought. You don't have to be a WCAG expert to improve your
website, you can start immediately by fixing the little things that make a huge difference, such as:

* learning to use the `alt` attribute properly
* making sure your links and buttons are marked as such (no `<div class=button>` atrocities)
* not relying exclusively on colors to communicate information
* explicitly labelling form controls

```html
<!-- bad -->
<h1><img alt=Logo src=logo.png></h1>

<!-- good -->
<h1><img alt=Company src=logo.png></h1>
```