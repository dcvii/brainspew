---
title: "How to bypass Cloudflare bot detection"
source: "https://medium.com/@eduardojld/how-to-bypass-cloudflare-bot-detection-dc2086c7a751"
author:
  - "[[Eduardo Lugo]]"
published: 2025-05-30
created: 2025-06-01
description: "If you have tried adding headers, origins, getting and setting cookies, and mocking regular users with Playwright or Selenium without success, this might work for you, it did for us. We had a…"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

If you have tried adding headers, origins, getting and setting cookies, and mocking regular users with Playwright or Selenium without success, this might work for you, it did for us.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*of428ba64RGmH97DCnQJDA.jpeg)

We had a scraping process that started getting Cloudflare errors all of a sudden, We already mentioned all of the stuff we tried that did not work.

## Enter Brightdata

We already used [BrightData](https://brightdata.com/proxy-types/residential-proxies) for our SERP provider; we were using [SERPAPI](https://serpapi.com/), but changed to BrightData since the pricing model made more sense for our use case.

So we wanted to check what alternatives we had within the same provider, and with a couple of changes, we were able to add the residential proxy to our normal requests, which ended up working

## Without Proxy

*\*Headers and URLs were modified to be generic*

```c
const https = require('https');

const request = https.request('https://example.com/api/graphql', {
  method: 'GET',
  headers: {
    'Accept-Encoding': 'gzip',
    'Content-Type': 'application/json',
    Host: 'example.com',
    'User-Agent': 'CustomClient/1.0',
    Accept: '*/*',
    Connection: 'keep-alive',
    'custom-client-name': 'MyApp (production)',
    'x-custom-session': 'SESSION_TOKEN_PLACEHOLDER'
  },
}, (res) => {
  const cookies = res.headers['set-cookie'];
  if (cookies) {
    const cookieString = cookies.map((cookie) => cookie.split(';')[0]).join('; ');
    makeDataRequest(cookieString, resolve, reject);
  } else {
    reject(new Error('No cookies received from initial request'));
  }
});
```

## With proxy

```c
const request = https.request(
      'https://example.com/api/graphql',
      {
        method: 'GET',
        agent, // 👈 use proxy here
        headers: {
          'Accept-Encoding': 'gzip',
          'Content-Type': 'application/json',
          Host: 'example.com',
          'User-Agent': 'CustomClient/1.0',
          Accept: '*/*',
          Connection: 'keep-alive',
          'custom-client-name': 'MyApp (production)',
          'x-custom-session': 'SESSION_TOKEN_PLACEHOLDER'
        },
      },
      (res) => {
        const cookies = res.headers['set-cookie'];
        if (cookies) {
          const cookieString = cookies.map((cookie) => cookie.split(';')[0]).join('; ');
          makeDataRequest(cookieString, resolve, reject);
        } else {
          reject(new Error('No cookies received from initial request'));
        }
      }
    );
```

The agent is created like this

```c
const { HttpsProxyAgent } = require('https-proxy-agent');
const agent = new HttpsProxyAgent(proxyURL);
```

We used Brightdata, but there are other alternatives such as

- [https://oxylabs.io/](https://oxylabs.io/)
- [https://soax.com/](https://soax.com/)
- [https://decodo.com/](https://decodo.com/)

## Conclusion

This can be costly since the proxy provider will charge you depending on the amount of data you are pulling. We ended up reaching out to our target site to get our IPs allowed on their Cloudflare configuration, but while that was getting resolved, this temporary solution prevented any disruption to our services

Generalist. I write Coding and DevOps articles, that being said I'll write about whatever else helps me deliver value to what I'm doing

## More from Eduardo Lugo

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--dc2086c7a751---------------------------------------)