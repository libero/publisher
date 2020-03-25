# 1. Use micro frontends

Date: 2020-03-25

## Status

Proposed

## Context

Having the entire frontend in a monolith is the opposite of the backend architecture, where services are optional, and
can be modified and replaced as needed. This makes it hard, if not impossible, to change or replace a part of the
presentation layer without having to fork/throw away the whole thing.

## Decision

We will create separate services for individual pages and groups of pages, that will be exposed through a proxy to
appear as a single service. The frontends are entirely independent, and can be not used or replaced entirely at will.

## Consequences

- A proxy (e.g. Nginx, Varnish) is required to route between the frontends.
- Authentication knowledge will need to be shared between the frontends.
- Each frontend will have its own assets.
- Each frontend can be configured to know how to generate links to other frontends.
