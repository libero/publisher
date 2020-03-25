# 1. Use micro frontends

Date: 2020-03-25

## Status

Accepted

## Context

We designed the API layer (known as the backend) to be a custom set of services. This allows the user to tailor it to
their own requirements, and introduce custom code as needed.

The original plan was to make the presentation layer (known as the frontend) a monolith. That is, a single service that
generates all the HTML pages.

As a monolith, it is hard, if not impossible, to change or replace parts without having to replace the whole. This would
mean a lot of configuration options to support differing requirements. It would also limit adoption of the platform
as it can't meet them.

We investigated the use of micro frontends in [#371][Spike].

## Decision

We will create separate services for individual, and groups of, pages. The user will use a proxy to make them appear as
a single service. The frontends are independent of each other, and are always optional.

## Consequences

- The frontends will need to share knowledge of authentication.
- Each frontend will have its own assets.
- The user will need to configure each frontend so it knows how to generate links to other frontends.
- The user can choose which frontends to use.
- The user can add their own frontends as needed.

[Spike]: https://github.com/libero/publisher/issues/371 "Spike for micro frontends architecture"
