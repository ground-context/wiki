---
title: API Documentation
keywords: docs
sidebar: ground_sidebar
permalink: docs.html
folder: documentation
---

## Applications

### Edges

`POST /edges`: Creates a new Edge.

  * Required Fields: `sourceKey`, `fromNodeId`, `toNodeId`
  * Optional Fields: `name`

`POST /versions/edges`: Creates a new Edge Version in the edge provided by `edgeId`.

  * Required Fields: `edgeId`, `toNodeVersionStartId`, 
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`, `fromNodeVersionEndId`, `toNodeVersionEndId`

`GET /edges/{sourceKey}`: Retrieve an Edge.

`GET /versions/edges/{id}`: Retrieve an Edge Version.

### Graphs

`POST /graphs`: Creates a new Graph.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`

`POST /versions/graphs`: Creates a new Graph Version in the graph provided by `graphId`.

  * Required Fields: `graphId`, `edgeVersionIds`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`

`GET /graphs/{sourceKey}`: Retrieve a Graph.

`GET /versions/graphs/{id}`: Retrieve a Graph Version.

### Nodes

`POST /nodes`: Creates a new Node.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`

`POST /versions/nodes`: Creates a new Node Version in the node provided by `nodeId`.

  * Required Fields: `nodeId`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`.

`GET /nodes/{sourceKey}`: Retrieve a Node.

`GET /versions/nodes/{id}`: Retrieve a Node Version.

### Structures

`POST /structures`: Creates a new Structure.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`

`POST /versions/structures`: Creates a Structure Version in the structure provided by `structureId`.

  * Required Fields: `structureId`, `attributes`

`GET /structures/{sourceKey}`: Retrieve a Structure.

`GET /versions/structures/{id}`: Retrieve a Structure Version.

## Behavior

### Lineage Edges

`POST /lineage_edges`: Creates a new Lineage Edge.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`

`POST /versions/lineage_edges`: Creates a new Lineage Edge Version in the lineage edge provided by `lineageEdgeId`.

  * Required Fields: `lineageEdgeId`, `fromRichVersionId`, `toRichVersionid`, 
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`

`GET /edges/{sourceKey}`: Retrieve a Lineage Edge.

`GET /versions/edges/{id}`: Retrieve a Lineage Edge Version.

### Lineage Graphs

`POST /lineage_graphs`: Creates a new Lineage Graph.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`

`POST /versions/lineage_graphs`: Creates a new Lineage Graph Version in the lineage graph provided by `lineageGraphId`.

  * Required Fields: `lineageGraphId`, `lineageEdgeVersionIds`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`

`GET /lineage_graphs/{sourceKey}`: Retrieve a Lineage Graph.

`GET /versions/lineage_graphs/{id}`: Retrieve a Lineage Graph Version.
