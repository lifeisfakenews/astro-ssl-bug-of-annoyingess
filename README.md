# Astro SSL Bug

To reproduce:
- Clone the repo
- Open it in codespaces or some other viewer
**IT MUST USE HTTPS SO IT CANT BE LOCALHOST**
- `npm i`
- `npm run build` - cannot run dev, i think becayuse 404 pages dont appear to be returned properly in dev
- `/` works fine
- `/anythiny-else` (404 page) causes the SSL bug:

```
TypeError: fetch failed
    at node:internal/deps/undici/undici:12345:11
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
    at async #renderError (file:///workspaces/astro-ssl-bug-of-annoyingess/dist/server/entry.mjs:881:27)
    at async file:///workspaces/astro-ssl-bug-of-annoyingess/dist/server/entry.mjs:1127:26 {
  cause: [Error: 00885EF8AF7F0000:error:0A00010B:SSL routines:ssl3_get_record:wrong version number:../deps/openssl/openssl/ssl/record/ssl3_record.c:354:
  ] {
    library: 'SSL routines',
    reason: 'wrong version number',
    code: 'ERR_SSL_WRONG_VERSION_NUMBER'
  }
}
```

It appears to be to do with the hybrid output and files being prerendered and not prerendered

The bug only happens when `404.astro` does not export `prerender = false`

This issue also does not occur for `output: server`