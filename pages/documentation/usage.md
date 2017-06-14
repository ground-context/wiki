---
title: Using Ground
keywords: usage
sidebar: ground_sidebar
permalink: usage.html
folder: documentation
---

There are two primary modes of interactions that users will have with Ground.
The first is generating data context, and the second is interacting with or consuming data context.
There are two different sets of APIs that faciliate each of these modes of interaction.

## Generating Data Context

Generating data context is simple.
For each type of object in the Ground [metamodel](metamodel.html), there are a set of `POST` endpoints that enable users to create those objects.
At the moment, we do not have any bulk insertion APIs, but we plan to add them soon.

As per our data model, every logical object is versioned.
Before creating any version for an object, that object must first be explicltly created in Ground.
Here's an example interaction using a client library:

```java
GroundClient client = new GroundClient(host, port);

int managerId = client.createNode("manager");
int engineerId = client.createNode("engineer");

int managerVersionId = client.createNodeVersion("manager", managerTags); 
/* managerTags: {
      "name": {
          "key": "name", 
          "value": "a-manager", 
          "type": "string"
      },
      "age": {
          "key": "age", 
          "value": 30, 
          "type": "integer"
      }, 
      "department": {
          "key": "department", 
          "value": "engineering", 
          "type": "string"
      }
  }
*/

int engineerVersionId = client.createNodeVersion("engineer", engineerTags); 
/* engineerTags: {
      "name": {
          "key": "name", 
          "value": "an-engineer", 
          "type": "string"
      },
      "age": {
          "key": "age", 
          "value": 25, 
          "type": "integer"
      }, 
      "department": {
          "key": "department", 
          "value": "engineering", 
          "type": "string"
      }
  }
*/

client.createEdge("managerManagerEngineer", managerId, engineerId);
clinet.createEdgeVersion("managerManagesEngineer", managerVersionId, engineerVersionId);
```

**Note**: Our client library is still under development. 
The above is intended as an illustrative example and doesn't use JSON for readability and simplicity.

## Consuming Data Context

As of now, we do not have any complex query APIs.
Users are expected to retrieve individual context objects by querying for them explicitly.
There is a corresponding set of `GET` APIs similar to the `POST` APIs used to create context objects.
