### [https://cors.x7.workers.dev](https://cors.x7.workers.dev)


```js
addEventListener("fetch", event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  try {
    const url = new URL(request.url);

    if (url.pathname === "/")
      return new Response(`
        Usage:\n
          ${url.origin}/<url>
      `);

    return await fetch(request.url.slice(url.origin.length + 1), {
        method: request.method,
        headers: request.headers,
        redirect: "follow",
        body: request.body
      });
  } catch (e) {
    return new Response(e.stack || e, {status: 500});
  }
}
```
