# 2. Use component-level micro frontends for the header and footer

Date: 2020-03-25

## Status

Proposed

## Context

Having [separate micro frontends for pages] requires duplication of the header and footer.

We expect users will want to change the content of both, as well as their styling and behaviour.

## Decision

We will create dedicated services for the header and footer.

We will use [Edge Side Includes (ESIs)], limited to `<esi:include>`, to transclude them into pages. 

Each component will have 2 ESIs: 1 for the `<head>` and 1 for the `<body>`.

## Consequences

- It is compatible with popular ESI processors (e.g. Varnish, Fastly).
- Not all popular CDNs are ESI processors (e.g. AWS CloudFront). If there is no trusted proxy that can do so, each
  page-level micro frontend will need to process the ESIs itself. They can detect this through the
  [`Surrogate-Capability`][Surrogate-Capability] request header.
- Components can add their own CSS and JavaScript in the `<head>` ESI.
- As the page transcludes the component, the user has to take care to avoid clashes in styling and behaviour.
- The header and footer services can be replaced, or not used.

[Edge Side Includes (ESIs)]: https://www.w3.org/TR/esi-lang
[Separate micro frontends for pages]: 0001-use-micro-frontends.md
[Surrogate-Capability]: https://www.rfc-editor.org/rfc/rfc4229.html#section-2.1.101
