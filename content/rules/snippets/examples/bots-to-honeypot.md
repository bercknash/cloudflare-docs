---
type: example
summary: Use the [bot score field](/workers/runtime-apis/request/#incomingrequestcfproperties) to send bots to a honeypot.
goal:
  - Routing
operation:
  - Redirect
product:
  - Snippets
pcx_content_type: example
title: Send suspect bots to a honeypot
layout: example
---

```js
export default {
  async fetch(request) {
    const response = await fetch(request);

    // Clone the response so that it is no longer immutable
    const newResponse = new Response(response.body, response);

    if (request.cf.botManagement.score < 30) {
      const honeypot = "https://example.com/";
      return await fetch(honeypot, request);
    } else {
      return newResponse;
    }
  },
};
```