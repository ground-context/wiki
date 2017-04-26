---
title: Motivation
keywords: motivation
sidebar: ground_sidebar
permalink: motivation.html
folder: overview 
---

Traditional database management systems were built with a centralized interconnect called a catalog.
These catalogs contained traditional forms of *metadata*, such as relational table schemas and summary statistics for each table in the database.

This component is sorely lacking in the big data space.
The *de facto* metadata store today is the Hive Metastore which only allows users to store relational metadata.
While the Hive Metastore is used as a catalog by a number of open source components today, such as Cloudera Impala and Spark SQL, it is very restrictive.
The data management space today is not limited to relational tables anymore; the community has an ever-growing number of data formats that are supported for an ever-growing number of use cases.

We believe that there is a missing component in the big data space that helps users manage their metadata.
However, we believe that the definition of metadata is too restrictive.
Instead, we want to capture something with a much broader scope: *data context*.
*Data context* is all the information surrounding the use of data in an organization.

There are three key components to *data context* (affectionately termed the **ABCs of data context**): application context, behavioral context, and change over time.
The *application context* is what you might traditionally think of as metadata.
It consists of semantic models, statistical models, and other data that enables users to interpret raw bits for usage.
The *behavioral context* captures who in an organization is touching data and what they are doing with that data.
This includes capturing data lineage or provenance, associations between data and code, and the derivations of semantic relationships.
Lastly, the *change over time* aspect of data context helps users understand how the world is changing.
We believe that capturing the current state-of-the-world is not sufficient.
Users do and will need to understand relationships in time as well as in "space".

In addition to the motivation above, there are a few design principles that we believe in:

* **Design for Scale**. Capturing usage and interaction data will entail ingesting large amounts of data from usage logs and similar sources.
  Ground will need to scale accordingly to handle such a volume of data.
* **Model Agnostic**. Given the increasing data sources, formats, and processing tools, prescriptiveness is anathema to our vision.
  Rather, we believe that a good data context system will need to be adaptive and general.
* **Immutable**. In light of the change over time aspect of data context, we believe that data context must be immutable; new context will be generated and added over time.
* **Politically Neutral**. Lastly, we believe that Ground must be politically unopinionated to be productive for a broad variety of constituencies within an organization.
