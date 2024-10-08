---
title: CSP source values
slug: Web/HTTP/Headers/Content-Security-Policy/Sources
page-type: http-csp-directive
spec-urls: https://w3c.github.io/webappsec-csp/#framework-directive-source-list
---

{{HTTPSidebar}}

HTTP {{HTTPHeader("Content-Security-Policy")}} (CSP) header directives that specify a `<source>` from which resources may be loaded can use any one of the values listed below.
Relevant directives include the {{Glossary("fetch directive", "fetch directives")}}, along with others [listed below](#relevant_directives).

## Sources

- `<host-source>`

  - : Internet host by name or IP address. The [URL scheme](/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL), port number, and path are optional.
    Wildcards (`'*'`) can be used for subdomains, host address, and port number, indicating that all legal values of each are valid.
    When matching schemes, secure upgrades are allowed (e.g. specifying `http://example.com` will match `https://example.com`).
    Examples:

    - `http://*.example.com`: Matches all attempts to load from any subdomain of example.com. Also matches `https` resources.
    - `mail.example.com:443`: Matches all attempts to load from port 443 on mail.example.com.
    - `https://store.example.com`: Matches all attempts to access store.example.com using `https:`.
    - `*.example.com`: Matches all attempts to load from any subdomain of example.com.
    - `https://*.example.com:12/path/to/file.js`: Matches all attempts to load from any subdomain of example.com using `https:` on port 12, and only if the path is `/path/to/file.js`.
    - `ws://example.com`: Matches all attempts to load from example.com using `ws:`. Also matches `wss` resources.
    - `https://example.com/subdirectory`: Matches all attempts to load the exact path `https://example.com/subdirectory`.
    - `https://example.com/subdirectory/`: Matches all attempts to load files under `subdirectory` directory. For example, `https://example.com/subdirectory/path/to/file.js`. It does not match `https://example.com/path/to/file.js`.

    For more details about how path matching is done refer the [parts matching algorithms](https://w3c.github.io/webappsec-csp/#match-schemes) in the specification.

- `<scheme-source>`

  - : A scheme such as `http:` or `https:`.
    The colon is required.
    Unlike other values below, single quotes shouldn't be used.
    You can also specify data schemes (not recommended).

    - `data:` Allows [`data:` URLs](/en-US/docs/Web/URI/Schemes/data) to be used as a content source.
      _This is insecure; an attacker can also inject arbitrary `data:` URLs. Use this sparingly and definitely not for scripts._
    - `mediastream:` Allows [`mediastream:` URIs](/en-US/docs/Web/API/Media_Capture_and_Streams_API) to be used as a content source.
    - `blob:` Allows [`blob:` URIs](/en-US/docs/Web/API/Blob) to be used as a content source.
    - `filesystem:` Allows [`filesystem:` URIs](/en-US/docs/Web/API/FileSystem) to be used as a content source.

    > [!NOTE]
    > If a scheme source is missing, the document origin's scheme is used.
    > Secure upgrades are allowed, so if the document is loaded using `https:`, then `example.com` will match `https://example.com` but not `http://example.com`.
    > For more information, see [CSP Level 3](https://www.w3.org/TR/CSP3/#match-url-to-source-list).

- `'self'`
  - : Refers to the origin from which the protected document is being served, including the same URL scheme and port number.
    You must include the single quotes. Some browsers specifically exclude `blob` and `filesystem` from source directives.
    Sites needing to allow these content types can specify them using the Data attribute.
- `'unsafe-eval'`
  - : Allows the use of `eval()` and other unsafe methods for creating code from strings.
    You must include the single quotes.
- `'wasm-unsafe-eval'`
  - : Allows the loading and execution of WebAssembly modules without the need to also allow unsafe JavaScript execution via `'unsafe-eval'`.
    The single quotes are required.
- `'unsafe-hashes'`
  - : Allows enabling specific inline [event handlers](/en-US/docs/Web/Events/Event_handlers).
    If you only need to allow inline event handlers and not inline {{HTMLElement("script")}} elements or [`javascript:` URLs](/en-US/docs/Web/URI/Schemes/javascript), this is a safer method than using the `unsafe-inline` expression.
- `'unsafe-inline'`
  - : Allows the use of inline resources, such as inline {{HTMLElement("script")}} elements, [`javascript:` URLs](/en-US/docs/Web/URI/Schemes/javascript), inline event handlers, and inline {{HTMLElement("style")}} elements.
    The single quotes are required.
- `'none'`
  - : Refers to the empty set; that is, no URLs match.
    The single quotes are required.
- `'nonce-<base64-value>'`

  - : An allowlist for specific inline scripts using a cryptographic nonce (number used once).
    The server must generate a unique nonce value each time it transmits a policy.
    It is critical to provide an unguessable nonce, as bypassing a resource's policy is otherwise trivial.
    See [unsafe inline script](/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src#unsafe_inline_script) for an example.
    Specifying nonce makes a modern browser ignore `'unsafe-inline'` which could still be set for older browsers without nonce support.

    > [!NOTE]
    > The CSP `nonce` source can only be applied to _nonceable_ elements (e.g., as the {{HTMLElement("img")}} element has no `nonce` attribute, there is no way to associate it with this CSP source).

- `'<hash-algorithm>-<base64-value>'`
  - : A sha256, sha384 or sha512 hash of scripts or styles.
    This value consists of the algorithm used to create the hash followed by a hyphen and the base64-encoded hash of the script or style.
    When generating the hash, exclude \<script> or \<style> tags and note that capitalization and whitespace matter, including leading or trailing whitespace.
    In CSP 2.0, hash sources can be applied to inline scripts and styles. Hash source expressions are allowed in [CSP 3.0](https://www.w3.org/TR/CSP3/#external-hash) for external scripts in `script-src` directives.
    See the [script-src](/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src#unsafe_inline_script) and [style-src](/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/style-src#unsafe_inline_styles) pages for more information and examples.
- `'strict-dynamic'`
  - : The `strict-dynamic` source expression specifies that the trust explicitly given to a script present in the markup, by accompanying it with a nonce or a hash, shall be propagated to all the scripts loaded by that root script.
    At the same time, any allowlist or source expressions such as `'self'` or `'unsafe-inline'` are ignored.
    See [script-src](/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src#strict-dynamic) for an example.
- `'report-sample'`
  - : Requires a sample of the violating code to be included in the violation report.
- `'inline-speculation-rules'`
  - : Allows the inclusion of [speculation rules](/en-US/docs/Web/API/Speculation_Rules_API) in scripts (see also [`<script type="speculationrules">`](/en-US/docs/Web/HTML/Element/script/type/speculationrules)).

## Specifications

{{Specifications}}

## Relevant directives

Directives for which the above sources apply include:

- {{Glossary("fetch directive", "Fetch directives")}}:

  - {{CSP("default-src")}}
  - {{CSP("child-src")}}
  - {{CSP("connect-src")}}
  - {{CSP("font-src")}}
  - {{CSP("frame-src")}}
  - {{CSP("img-src")}}
  - {{CSP("manifest-src")}}
  - {{CSP("media-src")}}
  - {{CSP("object-src")}}
  - {{CSP("prefetch-src")}}
  - {{CSP("script-src")}}
  - {{CSP("script-src-elem")}}
  - {{CSP("script-src-attr")}}
  - {{CSP("style-src")}}
  - {{CSP("style-src-elem")}}
  - {{CSP("style-src-attr")}}
  - {{CSP("worker-src")}}

- {{Glossary("Document directive", "Document directives")}}:

  - {{CSP("base-uri")}}
  - {{CSP("sandbox")}}

- {{Glossary("Navigation directive", "Navigation directives")}}:

  - {{CSP("form-action")}}
  - {{CSP("frame-ancestors")}}
