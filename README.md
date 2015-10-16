# TIL (today I learned): etags in nginx

## static files
For static files (e.g. `try_files` or `root`) etag creation is enabled by default (no need to `etags on;`). They will respond with a header `ETag: "5620b4ae-367640"`.

### when using with gzip

Prior to 1.7.3 no etags were delivered when using gzip. Since 1.7.3 nginx will change "strong" to "weak" ones. The header will look like this: `ETag: "W/5620b4ae-367640"`. Nginx still used the hash of the original file (and *not* the gzipped on) and prefix it with a "W/".

## `proxy_pass`
Nginx does not create etags for proxied servers. You need to take care of this.

### when using with gzip
When the proxied server responds with a `"ETag"` header, nginx will transform it to a weak etag (read above).
