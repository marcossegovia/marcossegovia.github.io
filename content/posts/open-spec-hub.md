+++
date = '2025-11-15T16:30:00+01:00'
draft = false
title = 'Open Spec Hub: One Documentation Hub for All Your APIs'
description = 'Building a unified documentation platform that brings REST, AsyncAPI, and other API protocols together in a single, elegant interface'
tags = ['api', 'documentation', 'open-source', 'nextjs', 'asyncapi', 'openapi']
categories = ['projects']
authors = ['marcossegovia']
+++

I've watched teams struggle with the same problem for years. You have your REST API documented in Swagger UI. Your event-driven architecture lives in some AsyncAPI viewer. Maybe there's a GraphQL playground somewhere. Each protocol has its own tools, its own vocabulary, its own way of showing examples. Developers end up with five browser tabs open just to understand how your platform works.

Last month, I joined a project where the onboarding doc literally said: "Check Confluence for the REST endpoints, the Confluent Kafka host for the event schemas, and ask Sarah about the webhooks." When I asked why there wasn't a single source of truth, the response was: "We've tried, but every protocol needs different documentation tools." That's when I decided **to build Open Spec Hub.**

## What It Is

Open Spec Hub is a unified documentation platform that displays all your API contracts—REST, AsyncAPI events, and more—through a single, consistent interface. Instead of juggling multiple tools and mental models, your entire team sees everything in one place. You drop your OpenAPI and AsyncAPI spec files into a folder, and the platform automatically parses, normalizes, and presents them in a way that makes sense regardless of the underlying protocol.

It's built for engineering teams who work with multiple API paradigms and need one centralized hub where everyone can find what they need without context-switching between different documentation tools.

## The Journey

The core challenge wasn't parsing the specs—libraries like swagger-parser and @asyncapi/parser handle that well. The hard part was creating a conceptual model that made sense across protocols. REST talks about "endpoints" and "HTTP methods." AsyncAPI talks about "channels" and "publish/subscribe." How do you show both without making users learn two different mental models?

I spent a week trying to preserve all the protocol-specific terminology. The result was confusing—buttons that said "GET" next to buttons that said "Subscribe", paths like `/api/users` next to topics like `user.events`. It felt like two different applications forced into one interface. I almost gave up on the unified approach and started building separate tabs for each protocol.

Then I realized the solution wasn't to show everything, but to abstract the right things. Both protocols have operations (something you can do), actions (how you interact with it), locations (where it lives), and data schemas (what goes in and out). I created a normalization layer that translates protocol-specific concepts into these universal terms. Now a REST POST endpoint and an AsyncAPI publish operation both render as "Operation" with clear action badges. Same interface, same mental model, different protocols underneath.

The testing strategy surprised me. I initially wrote unit tests for the parsers and normalizers, but what really mattered was the end-to-end experience. I ended up with 82 Playwright tests that verify the entire flow: load a spec, render the operations, display code examples, search across protocols. Writing E2E tests first would have saved me time.

## Under the Hood

I built this with Next.js 14 because I wanted static site generation—documentation should load instantly and work without JavaScript if needed. The architecture has three layers:

1. **Parsers** - Protocol-specific parsing using swagger-parser for OpenAPI and @asyncapi/parser for AsyncAPI
2. **Normalization** - Translates parsed specs into a unified model with common concepts (Operation, Action, Location, Schema)
3. **Rendering** - Protocol-agnostic UI components that work with the normalized model

The UI uses shadcn/ui components with Tailwind CSS. Code examples are highlighted with highlight.js and generated automatically based on the schemas. The whole thing compiles to static HTML, so hosting is trivial—I'm running the demo on GitHub Pages.

Adding support for new protocols is straightforward: write a parser, write a normalizer, register it in the spec detector. The rendering layer doesn't need to change.

## Try It Out

You can explore the [live demo](https://marcossegovia.me/open-spec-hub/demo/) to see how it handles both REST APIs and event streams. The [landing page](https://marcossegovia.me/open-spec-hub/) explains the concept, and the full [source code is on GitHub](https://github.com/marcossegovia/open-spec-hub) under MIT license.

Getting started is simple: clone the repo, drop your OpenAPI and AsyncAPI specs into the `specs/` directory, and run `npm run dev`. Your unified documentation hub will be running on localhost. If you want to add support for GraphQL, gRPC, or other protocols, contributions are very welcome—the architecture is built for extensibility.

## Reflection

Building this taught me that the best abstractions hide complexity without losing important details. I initially thought I needed to expose every feature of every protocol, but what teams actually need is a consistent way to understand their APIs. Keeping the unified model simple—just four core concepts—made the whole platform more useful.

I'm curious to see if this approach works for other protocol combinations. GraphQL and gRPC are obvious next candidates. If you're dealing with multi-protocol API documentation and want a single source of truth, give it a try and let me know what's missing!
