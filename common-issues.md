# Common Issues

## Mysterious Double Response

When you're helping a student debug and using the server log, do you see a mysterious double request going out without any redirects?

It's likely because an asset is being loaded:

```
<img src="hi">
```

on a page at `/things/:zebra` will cause a request to `/things/hi` for the image asset.