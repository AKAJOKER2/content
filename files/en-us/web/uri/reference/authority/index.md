---
title: URI authority
short-title: Authority
slug: Web/URI/Reference/Authority
page-type: uri-component
spec-urls: https://www.rfc-editor.org/rfc/rfc3986.html#section-3.2
sidebar: urlsidebar
---

The **authority** of a URI is the section that comes after the [scheme](/en-US/docs/Web/URI/Reference/Schemes) and before the path. It may have up to three parts: user information, host, and port.

## Syntax

```url
host
host:port
user@host
user@host:port
```

- `host`
  - : The _host_ is usually the domain name or IP address of the server hosting the resource. The domain name is resolved to an IP address using the {{glossary("DNS", "Domain Name System")}}.
- `port` {{optional_inline}}
  - : The _port_ is a number that indicates the port on which the server is listening for requests. It is optional and defaults to 80 for HTTP and 443 for HTTPS. Other schemes may define their own defaults or make it mandatory.
- `user` {{optional_inline}}
  - : The _user_ is optional and is used for authentication purposes. It is not commonly used in web URIs.

    > [!WARNING]
    > Providing user information directly in HTTP URLs is not recommended, as it can expose sensitive information. Use other methods like HTTP authentication or session cookies instead. Sometimes, phishing sites trick users by displaying misleading URLs whose "user" part appears as if it's a domain name, known as [semantic URL attack](https://en.wikipedia.org/wiki/Semantic_URL_attack).

## Description

Consider the following URL:

```url
http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument
```

The authority in this case is `www.example.com:80`, comprised of the host name (specifically a domain name) and a port.

![Domain Name](mdn-url-domain@x2.png)

`www.example.com` is the _host name_ of the URI, indicating which Web server is being requested. Here, we use a domain name, but it's also possible to use an {{Glossary("IP address")}} of the host.
Because IP addresses are less convenient and harder to remember, it's more common to use a domain name unless the server doesn't have one registered.

![Port](mdn-url-port@x2.png)

`:80` is the _port_ of the URL, indicating the technical "gate" used to access the resources on the web server. It is usually omitted if the web server uses the standard ports of the HTTP protocol (80 for HTTP and 443 for HTTPS) to grant access to its resources. Otherwise, it is mandatory.

## Examples

- `https://developer.mozilla.org`
  - : The host is `developer.mozilla.org`. The port is not specified but will default to 443 if accessed via `https:`.
- `http://localhost:8080`
  - : The host is `localhost` and the port is `8080`. `localhost` is a special host name that the browser resolves to the local address `127.0.0.1`.
- `postgresql://postgres:admin123@db:5432`
  - : The host is `db`, and the port is `5432`. It also specifies a user `postgres` and its password `admin123`. This can be used to connect to a PostgreSQL database.
- `https://cnn.example.com&story=breaking_news@10.0.0.1`
  - : A misleading URL that looks like it's pointing to a trusted website. However, the host name is `10.0.0.1`, and the `cnn.example.com&story=breaking_news` part is the "user".

## Specifications

{{Specifications}}

## See also

- [URIs](/en-US/docs/Web/URI)
- [Choosing between www and non-www URLs](/en-US/docs/Web/URI/Guides/Choosing_between_www_and_non-www_URLs)
