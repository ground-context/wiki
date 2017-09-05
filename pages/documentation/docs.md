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
  * Optional Fields: `name`, `tags`
  * Client API method: `createEdge(sourceKey, name, fromNodeId, toNodeId, tags)`

`POST /versions/edges`: Creates a new Edge Version in the edge provided by `edgeId`.

  * Required Fields: `edgeId`, `toNodeVersionStartId`, `fromNodeVersionStartId`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`, `fromNodeVersionEndId`, `toNodeVersionEndId`, `parentIds`
  * Client API method: `createEdgeVersion(edgeId, toNodeVersionStartId, fromNodeVersionStartId, toNodeVersionEndId, fromNodeVersionEndId, reference, referenceParameters, tags, structureVersionId, parentIds)`

`GET /edges/{sourceKey}`: Retrieve an Edge.
  
  * Client API method: `getEdge(sourceKey)`

`GET /edges/{sourceKey}/latest`: Retrieve the most recent versions (i.e., any version without a child) of this edge.
  
  * Client API method: `getEdgeLatestVersions(sourceKey)`

`GET /edges/{sourceKey}/history`: Retrieve all the parent-child relationships of this edge.
  
  * Client API method: `getEdgeHistory(sourceKey)`

`GET /versions/edges/{id}`: Retrieve an Edge Version.
  
  * Client API method: `getEdgeVersio(id)`

### Graphs

`POST /graphs`: Creates a new Graph.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`, `tags`
  * Client API method: `createGraph(sourceKey, name, tags)`

`POST /versions/graphs`: Creates a new Graph Version in the graph provided by `graphId`.

  * Required Fields: `graphId`, `edgeVersionIds`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`, `parentIds`
  * Client API method: `createGraphVersion(graphId, edgeVersionIds, reference, referenceParameters, tags, structureVersionId, parentIds)`

`GET /graphs/{sourceKey}`: Retrieve a Graph.
  
  * Client API method: `getGraph(sourceKey)`

`GET /graphs/{sourceKey}/latest`: Retrieve the most recent versions (i.e., any version without a child) of this graph.
  
  * Client API method: `getGraphLatestVersions(sourceKey)`

`GET /graphs/{sourceKey}/history`: Retrieve all the parent-child relationships of this graph.
  
  * Client API method: `getGraphHistory(sourceKey)`

`GET /versions/graphs/{id}`: Retrieve a Graph Version.
  
  * Client API method: `getGraphVersion(id)`

### Nodes

`POST /nodes`: Creates a new Node.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`, `tags`
  * Client API method: `createNode(sourceKey, name, tags)`

`POST /versions/nodes`: Creates a new Node Version in the node provided by `nodeId`.

  * Required Fields: `nodeId`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`, `parentIds`
  * Client API method: `createNodeVersion(nodeId, reference, referenceParameters, tags, structureVersionId, parentIds)`

`GET /nodes/{sourceKey}`: Retrieve a Node.
  
  * Client API method: `getNode(sourceKey)`

`GET /nodes/{sourceKey}/latest`: Retrieve the most recent versions (i.e., any version without a child) of this node.
  
  * Client API method: `getNodeLatestVersion(sourceKey)`

`GET /nodes/{sourceKey}/history`: Retrieve all the parent-child relationships of this node.
  
  * Client API method: `getNodeHistory(sourceKey)`

`GET /versions/nodes/{id}`: Retrieve a Node Version.
  
  * Client API method: `getNodeVersion(id)`

`GET /versions/nodes/adjacent/lineage/{id}`: Retrieve the lineage edges adjacent to this node version.
  
  * Client API method: `getNodeVersionAdjacentLineage(id)`

### Structures

`POST /structures`: Creates a new Structure.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`, `tags`
  * Client API method: `createStructure(sourceKey, name, tags)`

`POST /versions/structures`: Creates a Structure Version in the structure provided by `structureId`.

  * Required Fields: `structureId`, `attributes`
  * Optional Fields: `parentIds`
  * Client API method: `createStructureVersion(structureId, attributes, parentIds)`

`GET /structures/{sourceKey}`: Retrieve a Structure.
  
  * Client API method: `getStructure(sourceKey)`

`GET /structures/{sourceKey}/latest`: Retrieve the most recent versions (i.e., any version without a child) of this structure.
  
  * Client API method: `getStructureLatestVersions(sourceKey)`

`GET /structures/{sourceKey}/history`: Retrieve all the parent-child relationships of this structure.
  
  * Client API method: `getStructureHistory(sourceKey)`

`GET /versions/structures/{id}`: Retrieve a Structure Version.
  
  * Client API method: `getStructureVersion(id)`

## Behavior

### Lineage Edges

`POST /lineage_edges`: Creates a new Lineage Edge.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`, `tags`
  * Client API method: `createLineageEdge(sourceKey, name, tags)`

`POST /versions/lineage_edges`: Creates a new Lineage Edge Version in the lineage edge provided by `lineageEdgeId`.

  * Required Fields: `lineageEdgeId`, `fromRichVersionId`, `toRichVersionid`, 
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`, `parentIds`
  * Client API method: `createLineageEdgeVersion(lineageEdgeId, toRichVersionId, fromRichVersionId, reference, referenceParameters, tags, structureVersionId, parentIds)`

`GET /lineage_edges/{sourceKey}`: Retrieve a Lineage Edge.

  * Client API method: `getLineageEdge(sourceKey)`

`GET /lineage_edges/{sourceKey}/latest`: Retrieve the most recent versions (i.e., any version without a child) of this lineage edge.

  * Client API method: `getLineageEdgeLatestVersions(sourceKey)`

`GET /lineage_edges/{sourceKey}/history`: Retrieve all the parent-child relationships of this lineage edge.

  * Client API method: `getLineageEdgeHistory(sourceKey)`

`GET /versions/lineage_edges/{id}`: Retrieve a Lineage Edge Version.

  * Client API method: `getLineageEdgeVersion(id)`

### Lineage Graphs

`POST /lineage_graphs`: Creates a new Lineage Graph.

  * Required Fields: `sourceKey`
  * Optional Fields: `name`, `tags`
  * Client API method: `createLineageGraph(sourceKey, name, tags)`

`POST /versions/lineage_graphs`: Creates a new Lineage Graph Version in the lineage graph provided by `lineageGraphId`.

  * Required Fields: `lineageGraphId`, `lineageEdgeVersionIds`
  * Optional Fields: `tags`, `structureVersionId`, `reference`, `referenceParameters`, `parentIds`
  * Client API method: `createLineageGraphVersion(graphId, lineageEdgeVersionIds, reference, referenceParameters, tags, structureVersionId, parentIds)`

`GET /lineage_graphs/{sourceKey}`: Retrieve a Lineage Graph.

  * Client API method: `getLineageGraph(sourceKey)`

`GET /lineage_graphs/{sourceKey}/latest`: Retrieve the most recent versions (i.e., any version without a child) of this lineage graph.

  * Client API method: `getLineageGraphLatestVersions(sourceKey)`

`GET /lineage_graphs/{sourceKey}/history`: Retrieve all the parent-child relationships of this lineage graph.

  * Client API method: `getLineageGraphHistory(sourceKey)`

`GET /versions/lineage_graphs/{id}`: Retrieve a Lineage Graph Version.

  * Client API method: `getLineageGraphVersion(id)`
