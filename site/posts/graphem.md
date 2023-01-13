---
title: Graphem
date: "2022-09-30"
description: "Creating a plugin for NASA's visualization framework"
tags:
  - nasa
  - graphql
  - typescript
---

## Introduction

<a href="https://software.nasa.gov/software/ARC-15256-1D" target="_blank">NASA Open MCT</a> is a web-based mission control framework for visualizing <a href="https://en.wikipedia.org/wiki/Telemetry" target="_blank">telemetry of space missions</a>. It allows <a href="https://nasa.github.io/openmct/plugins/" target="_blank">plugins</a> to be developed to extend its functionality. One of the cases that can be developed is to visualize telemetry data from a source that is different from the default ones. In this case, I developed an experimental plugin that allows you to visualize telemetry data from a <a href="https://graphql.org/" target="_blank">GraphQL</a> endpoint. Introducing **Graphem**.

Graphem, a plugin that allows viewing telemetry data in NASA Open MCT directly from a GraphQL server.

## Design Process

The design of the solution was based on capturing the telemetry data from a GraphQL endpoint and then displaying it in NASA Open MCT. The structure is defined by the <a href="https://nasa.github.io/openmct/plugins-documentation/" target="_blank">NASA Open MCT plugin architecture</a>. The plugin is made up of a part to integrate domain objects with object provider and composition provider. Then require the historical data, to display it on the screen, and finally require the real-time data continuously to link them on the same screen.

GraphQL offers a query language that allows you to request data from a server. The query language is based on the concept of types and fields. And also offers a real-time subscription mechanism to receive data from the server. The data is returned in <a href="https://www.json.org/json-en.html"  target="_blank">JSON format</a>. Graphem applies this concept to the NASA Open MCT plugin architecture.

## Development Process

### Building a basic plugin

The development of Graphem began by generating a prototype of how to build a plugin that obtains basic <a href="https://graphql.org/learn/queries/" target="_blank">GraphQL queries</a>. Although I was able to use the <a href="https://www.apollographql.com/docs/react/" target="_blank">Apollo client</a>, I preferred to use the <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API" target="_blank">fetch API</a> to get more lightness in the plugin.

NASA Open MCT provides documentation on how to develop plugins. The tutorial <a href="https://nasa.github.io/openmct/getting-started/" target="_blank">NASA Spacecraft</a> teaches how to develop a plugin that allows you to visualize telemetry data from a HTTP/<a href="https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API" target="_blank">WebSockets</a> server. This tutorial was used as a basis for the development of Graphem.

After a few tests, I was able to obtain the telemetry data from a GraphQL endpoint and display it in NASA Open MCT. The next step was to integrate real-time data.

### Integrating real-time data

In this part I have to extend the functionality of the server. The server must be able to send telemetry data in real-time. As I mentioned before, GraphQL offers a subscription mechanism to receive data from the server. But at the time multiple solutions came out to implement this mechanism.

### A plugin with Type checking

NASA Open MCT does not support <a href="" target="_blank">TypeScript</a>. But for a better development experience this plugin was built on it. The first step was to create a <a href="" target="_blank">TypeScript configuration file</a>. This file is used to configure the TypeScript compiler. The configuration file is called `tsconfig.json` and is located in the root of the project.

Currently there is an iniative to add Types support for NASA Open MCT. You can follow the progress in [this issue].

### Integrating to NPM package

Once the plugin was ready, it was time to integrate it into a NPM package. For better integration with the Graphem package it uses <a href="https://rollupjs.org/guide/en/" target="_blank">RollUp</a>, a module bundler, in the same style as <a href="" target="_blank">Open MCT YAMCS</a>. Thanks to this same configuration, it will export a file in Universal Module Definition (UMD).

### Publishing the package to NPM

The package is published to NPM. And, it can be installed with `npm i graphem`.

### Publishing the plugin on NASA Open MCT Community Plugins

An email was sent to the NASA Open MCT community to publish the plugin on the [Community Plugins]() section.

Currently the plugin is not published on the NASA Open MCT Community Plugins section. But soon it will be.

## References

- <a href="" target="_blank">NASA Open MCT</a>
- <a href="https://graphql.org/" target="_blank">GraphQL</a>
- <a href="https://www.apollographql.com/docs/react/" target="_blank">Apollo client</a>
- <a href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API" target="_blank">fetch API</a>
- <a href="https://www.typescriptlang.org/" target="_blank">TypeScript</a>
- <a href="https://rollupjs.org/guide/en/" target="_blank">RollUp</a>
- <a href="https://github.com/akhenry/openmct-yamcs" target="_blank">Open MCT YAMCS</a>
- <a href="https://www.oreilly.com/library/view/building-enterprise-javascript/9781788477321/03979156-167c-4598-85e8-0544241e2aed.xhtml" target="_blank">Universal Module Definition</a>