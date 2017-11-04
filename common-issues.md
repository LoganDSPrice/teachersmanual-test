# Common Issues

## Mysterious Double Response

When you're helping a student debug and using the server log, do you see a mysterious double request going out without any redirects?

It's likely because an asset is being loaded with a relative path:

```
<img src="hi">
```

without a leading slash (or an absolute URL) as the source on a page at `/things/:zebra` will cause a request to `/things/hi` for the image asset, and `:zebra => "hi"` will mysteriously appear in the `params` hash — for the _second_ request/response.

If that action includes a `.find()`, an exception will be thrown.