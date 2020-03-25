# 2. Use component-level micro frontends

Date: 2020-03-25

## Status

Proposed

## Context

Having [separate micro frontends for pages](0001-use-micro-frontends.md) requires duplication of the header and footer.
These are likely to be changed by the user, and possibly even replaced entirely.

## Decision

We will use [Edge Side Includes (ESIs)](https://www.w3.org/TR/esi-lang), limited to `<esi:include>` to maintain
compatibility with existing implementations (such as Varnish and Fastly).

Each component will have 2 ESIs, 1 for the `<head>` and 1 for the `<body>`.

## Consequences

- Requires an ESI processor, which has to at least be implemented at the app level to make it usable standalone.
- Not all popular CDNs are ESI processors (e.g. AWS CloudFront), so require another layer.
- Components can add their own CSS and JavaScript in the `<head>` ESI.
- As the component is transcluded into the page, Care needs to be taken to avoid clashes in styling and behaviour.
