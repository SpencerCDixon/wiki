# CORS

Cross Origin Resource Sharing

Sometimes when debugging CORS issues it can be useful to run Chrome with CORS
disabled just to confirm that it actually is a CORS related bug.  To do that you
can open chrome with:

```sh
$ open -a Google\ Chrome --args --disable-web-security --user-data-dir=~/desktop/some-data
```

Preflight options requests occur when a non trivial request is occuring (not
get/post or non standard headers).  The good news is once the option request
succeeds the browser will cache the response so it won't incur the extra latency
the next time.
