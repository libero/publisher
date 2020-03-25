# 1. Use micro frontends

Date: 2020-03-25

## Status

Proposed

## Context

We designed the API layer (known as the backend) to be a custom set of services. This allows the user to tailor it to
their own requirements, and introduce custom code as needed.

The original plan was to make the presentation layer (known as the frontend) a monolith. That is, a single service that
generates all the HTML pages.

As a monolith, it is hard, if not impossible, to change or replace parts without having to replace the whole. This would
mean a lot of configuration options to support differing requirements. It would also limit adoption of the platform
as it can't meet them.

## Decision

We will create separate services for individual, and groups of, pages, that will be exposed through a proxy to appear as
a single service. The frontends are entirely independent, and can be not used or replaced entirely at will.

## Consequences

- A proxy (e.g. Nginx, Varnish) is required to route between the frontends.
- Authentication knowledge will need to be shared between the frontends.
- Each frontend will have its own assets.
- Each frontend can be configured to know how to generate links to other frontends.
