### Performance

Unless there's a valid reason for loading your scripts before your content, don't block the
rendering of your page. If your style sheet is heavy, isolate the styles that are absolutely
required initially and defer the loading of the secondary declarations in a separate style sheet.
Two HTTP requests is significantly slower than one, but the perception of speed is the most
important factor.

```html
<!-- bad -->
<!doctype html>
<meta charset=utf-8>
<script src=analytics.js></script>
<title>Hello, world.</title>
<p>...</p>

<!-- good -->
<!doctype html>
<meta charset=utf-8>
<title>Hello, world.</title>
<p>...</p>
<script src=analytics.js></script>
```