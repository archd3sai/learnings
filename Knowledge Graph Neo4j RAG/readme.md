# Notes

Course: [Knowledge Graph RAG](https://www.deeplearning.ai/short-courses/knowledge-graphs-rag/)

## Neo4j

open-source NoSQL database that uses graph structures with nodes, edges, and properties to represent and store data. The main strength of Neo4j is its ability to quickly execute complex queries across large datasets.

## Cypher

Cypher is the query language for Neo4j, designed to be intuitive and efficient for working with graph data. 
- Uses an ASCII-art syntax to express patterns in the graph for matching and querying data.
- Allows Create, Read, Update, and Delete operations on both nodes and relationships.
- Supports aggregating data and ordering query results, similar to SQL.
- Provides built-in functions and allows expressions for data manipulation and transformation.
- Designed to efficiently execute complex queries involving deep traversal and pattern matching.

Cypher Cheatsheet: [Link](https://neo4j.com/docs/cypher-cheat-sheet/5/auradb-enterprise/?utm_source=Google&utm_medium=PaidSearch&utm_campaign=Evergreenutm_content=AMS-Search-SEMCE-DSA-None-SEM-SEM-NonABM&utm_term=&utm_adgroup=DSA-use-cases&gad_source=1&gclid=Cj0KCQjwqdqvBhCPARIsANrmZhPnADdJduWJcj8BLHWoQSBM7XaaWBDFYQZ1LltEaTJ2aJ-LwIYw-20aAtwOEALw_wcB)

## Knowledge Graph Example

#### Example

![alt text](https://github.com/archd3sai/learnings/blob/main/Knowledge%20Graph%20Neo4j%20RAG/img/image1.png "Example Graph Relationships")

#### Schema

![alt text](https://github.com/archd3sai/learnings/blob/main/Knowledge%20Graph%20Neo4j%20RAG/img/image.png "Graph Schema")

## Example LLM Prompt

```
CYPHER_GENERATION_TEMPLATE = """Task:Generate Cypher statement to query a graph database.
Instructions:
Use only the provided relationship types and properties in the schema.
Do not use any other relationship types or properties that are not provided.
Schema:
{schema}
Note: Do not include any explanations or apologies in your responses.
Do not respond to any questions that might ask anything else than for you to construct a Cypher statement.
Do not include any text except the generated Cypher statement.
Examples: Here are a few examples of generated Cypher statements for particular questions:

# What investment firms are in San Francisco?
MATCH (mgr:Manager)-[:LOCATED_AT]->(mgrAddress:Address)
    WHERE mgrAddress.city = 'San Francisco'
RETURN mgr.managerName

# What investment firms are near Santa Clara?
  MATCH (address:Address)
    WHERE address.city = "Santa Clara"
  MATCH (mgr:Manager)-[:LOCATED_AT]->(managerAddress:Address)
    WHERE point.distance(address.location, 
        managerAddress.location) < 10000
  RETURN mgr.managerName, mgr.managerAddress

# What does Palo Alto Networks do?
  CALL db.index.fulltext.queryNodes(
         "fullTextCompanyNames", 
         "Palo Alto Networks"
         ) YIELD node, score
  WITH node as com
  MATCH (com)-[:FILED]->(f:Form),
    (f)-[s:SECTION]->(c:Chunk)
  WHERE s.f10kItem = "item1"
RETURN c.text

The question is:
{question}"""
```
