# 2. Use component-level micro frontends

Date: 2020-03-25

## Status

Proposed

## Context

Having [separate micro frontends for pages](0001-use-micro-frontends.md) requires duplication of the header and footer.

We expect users will want to change the content of both, as well as their styling and behaviour.

## Decision

We will use [Edge Side Includes (ESIs)](https://www.w3.org/TR/esi-lang), limited to `<esi:include>`.

Each component will have 2 ESIs: 1 for the `<head>` and 1 for the `<body>`.

Each page-level micro frontend will process the ESIs if it is not behind a trusted proxy that can do so. They will
detect this through the `Surrogate-Capabilities` request header.

## Consequences

- It is compatible with popular ESI processors (e.g. Varnish, Fastly).
- Not all popular CDNs are ESI processors (e.g. AWS CloudFront).
- Components can add their own CSS and JavaScript in the `<head>` ESI.
- As the page transcludes the component, the user has to take care to avoid clashes in styling and behaviour.
