### Language & character encoding

While defining the language is optional, it's recommended to always declare
it on the root element.

The HTML standard requires that pages use the UTF-8 character encoding.
It has to be declared, and although it can be declared in the Content-Type HTTP header,
it is recommended to always declare it at the document level.

```html
<!-- bad -->
<!doctype html>
<title>Hello, world.</title>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Hello, world.</title>
</html>
```