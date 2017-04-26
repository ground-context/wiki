---
title: The Ground Metamodel
keywords: metamodel
sidebar: ground_sidebar
permalink: metamodel.html
folder: overview
---

Ground is designed to manage both the ABCs of data context (defined in the [motivation](motivation.html) section) and the design requirements of data context services. 
The Common Ground metamodel is based on a layered graph structure shown here: one layer for each of the ABCs of data context. 

<img src="images/Metamodel.png" alt="Ground" width="25%" /><br/>

## Version Graphs
We begin with the version graph layer of Common Ground, which captures changes corresponding to the C in the ABCs of data context. 
This layer bootstraps the representation of all information in Ground, by providing the classes upon which all other layers are based. 
These classes and their subclasses are among the only information in Common Ground that is not itself versioned; this is why it forms the base of the metamodel. 
The main atom of our metamodel is the Version, which is simply a globally unique identifier; it represents an immutable version of some object. 
We depict Versions via the small circles in the bottom layer of the model. 
Ground links Versions into VersionHistoryDAGs via VersionSuccessor edges indicating that one version is the descendant of another (the short dark edges in the bottom of the figure.) 

Type parametrization ensures that all of the VersionSuccessors in a given DAG link the same subclass of Versions together. 
This representation of DAGs captures any partial order, and is general enough to reflect multiple different versioning systems. 
RichVersions support customization. 
These variants of Versions can be associated with ad hoc Tags (key-value pairs) upon creation. 
Note that all of the classes introduced above are immutable—new values require the creation of new Versions. 

### External Items and Schrödinger Versioning 
We often wish to track items whose metadata is managed outside of Ground: canonical examples include GitHub repositories and Google Docs. 
Ground cannot automatically track these items as they change; at best it can track observations of those items. 
Observed versions of external items are represented by optional fields in Ground’s RichVersions: the parameters for accessing the reference (e.g., port, protocol, URI, etc.), an externalAccessTimestamp, and an optional cachedValue. 
Whenever a Ground client uses the aboveground API to access a RichVersion with non-empty external parameters, Ground fetches the external object and generates a new ExternalVersion containing a new VersionID, an updated timestamp and possibly an updated cached value. 
We refer to this as a Schrödinger versioning scheme: each time we observe an ExternalVersion it changes. This allows Ground to track the history of an external object as perceived by Ground-enabled applications. 

## Model Graphs
The model graph level of Common Ground provides a model- agnostic representation of application metadata: the A of our ABCs.
We use a graph model for flexibility: graphs can repre- sent metadata entities and relationships from semistructured (JSON, XML) and structured (Relational, Object-Oriented, Matrix) data models.
A simple graph model enables the agility of schema-on-use at the metadata level, allowing diverse metadata to be independently captured as ad hoc model graphs and integrated as needed over time. 
The model graph is based on an internal superclass called Item, which is simply a unique ID that can be associated with a VersionHistoryDAG. 
Note that an Item is intrinsically immutable, but can capture change via its associated VersionHistoryDAG: a fresh Version of the Item is created whenever a Tag is changed. 
Ground’s public API centers around three core object classes derived from Item: Node, Edge, and Graph. 

Each of these subclasses has an associated subclass in the version graph: NodeVersion, EdgeVersion and GraphVersion. 
Nodes and Edges are highlighted in the middle layer of the figure, with the Nodes projected visually onto their associated versions in the other layers. 
The version graph allows for ad hoc Tags, but many applications desire more structure. 
To that end, the model graph includes a subclass of Item called Structure. 
A Structure is like a schema: a set of Tags that must be present. 
Unlike database schemas, the Structure class of Ground is versioned, via a StructureVersion subclass in the version graph. 
If an Item is associated with a Structure, each Version of the Item is associated with a corresponding StructureVersion and must define those Tags (along, optionally, with other ad hoc Tags.) 
Together, Tags, Structures and StructureVersions enable a breadth of metadata representations: from unstructured to semi-structured to structured. 

### Superversions: An Implementation Detail. 
The Common Ground model captures versions of relationships (e.g., Edges) between versioned objects (e.g., Nodes). 
The relationships themselves are first-class objects with identity and tags. 
Implemented naively, the version history of relationships can grow in unintended and undesirable ways. 
We address that problem by underlaying the logical Common Ground model with a physical compression scheme combined with lazy materialization of logical versions. 
Consider updating the current version of a central Node M with n incident Edges to neighbor Nodes. 
Creating a new NodeVersion for M implicitly requires creating n new EdgeVersions, one for each of the n incident edges, to capture the connection between the new version of M and the (unchanged!) versions of the adjacent nodes. 

More generally, the number of EdgeVersions grows as the product of node versioning and node fanout. 
We can mitigate the version factor by using a superversion, an implementation detail that does not change the logical metamodel of Common Ground. 
In essence, superversions capture a compressed set of contiguous NodeVersions and their common adjacencies. 
If we introduce k − 1 changes to version v of node M before we change any adjacent node, there will be k logical EdgeVersions connecting M to each of its neighbor NodeVersions. 
Rather than materializing those EdgeVersions, we can use a superversion capturing the relationship between each neighbor and the range \[v, vk\]. 
The actual logical EdgeVersions can be materialized on demand by the Ground runtime. 
More generally, in a branching version history, a superversion captures a growing rooted subgraph of the Versions of one Item, along with all adjacent Versions. 
A superversion grows monotonically to encompass new Versions with identical adjacencies. Note that the superversion represents both a supernode and the adjacent edges to common nodes; directionality of the adjacent edges is immaterial.

## Lineage Graphs
The goal of the lineage graph layer is to capture usage information composed from the nodes and edges in the model graph.
To facilitate data lineage, Common Ground depends on Principals.
Principals (a subclass of Node) represent the actors that work with data: users, groups, roles, etc. 
Any Data Governance effort requires these classes: as examples, they are key to authorization, auditing and reproducibility. 
In Ground, lineage is captured as a relationship between two Versions. 
This relationship is due to some process, either computational or manual. 

LineageEdges (purple arrows in the top layer of the figure) connect two or more (possibly differently-typed) Versions.
Note that LineageEdge is not a subclass of EdgeVersion; an EdgeVersion can only connect two NodeVersions; a LineageEdge can connect Versions from two different subclasses, including subclasses that are not under NodeVersion.
For example, we might want to record that Sue imported `nltk.py` in her `churn.py` script; this is captured by a LineageEdge between a PrincipalVersion (representing Sue) and an EdgeVersion (representing the dependency between the two files). 
Usage data is often generated by analyzing log files, code, and/or data, and it can become very large.
There are important choices about how and when to materialize lineage that are best left to aboveground applications. 
For example, in a pure SQL environment, the lineage of a specific tuple in a table might be materialized physically on demand as a tree of input tuples, but the lineage for all tuples in the table is more efficiently described logically by the SQL query and its input tables.

The Common Ground metamodel can support both approaches depending on the granularity of Items, Versions and LineageEdges chosen to be registered. 
Ground does not dictate this choice; it is made based on the context information ingested and the way it is used by aboveground applications.
