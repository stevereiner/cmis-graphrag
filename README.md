# CMIS-GraphRAG

## A Python sample that gets docs from a folder in a CMIS server, builds Knowledge Graphs and vectors in Neoj4, and supports AI queries with RAG and GraphRAG

For CMIS, the cmislib python package was used

For Neo4j KG building and GraphRAG, the Neo4j neo4j-graphrag python package was used

Uses FastAPI, has REST apis. Question and CMIS folder path forn env varibles, answer in terminal output

# Info on CMIS

[CMIS Wikipedia](https://en.wikipedia.org/wiki/Content_Management_Interoperability_Services)

# Info on Libraries supporting KG building, vectors / RAG, Graphs / GraphRAG

[Libraries Supporting KG building and GraphRAG](https://github.com/stevereiner/cmis-graphrag/blob/main/Libraries%20Supporting%20KG%20building%20and%20GraphRAG.md)

# LLMs models supported

- Supports using OpenAI (gpt-4.1 etc.)
- Supports Ollama LLMs (llama3.1 etc.)

# Requirements for cmislib package
- Name: cmislib Version: 0.7.0
- [cmislib 0.7.0 PyPi.org]https://pypi.org/project/cmislib/
- Summary: Apache Chemistry CMIS client library for Python
- Home-page: http://chemistry.apache.org/
- cmislib 0.7.0 has support for Python 3.x, previous were for Python 2.x

## Your CMIS server needs to support CMIS 1.0 or CMIS 1.1
- Alfresco (cmis 1.1)
- Nuxeo (cmis 1.1)
- OpenText Documentum, OpenText Content Management, OpenText eDocs (cmis 1.1)
- SAP Hana, SAP Extended ECM, SAP Mobile (cmis 1.1)
- IBM FileNet Content Manager, IBM Content Manager (full cmis 1.0, partial cmis 1.1)
- Microsoft SharePoint Server (cmis 1.0, on premises only)


# Requirements for neo4j-graphrag package

## Neo4j server versions supported:
- Neo4j >= 2025.01
- Neo4j >= 5.18.1

## You can use:
- Neo4j Enterprise Edition (Self Hosted)
- Neo4j Community Edition (Free, Self hosted)
- Neo4j Desktop (Free, Windows, Mac, Linux)
- Neo4j AuraDB (free, professional, mission critical tiers) + Graph Analytics Serverless
- Neo4j AuraDS

## APOC core is needed:
- In the Neo4j Desktop version, you can install the APOC core plugin (expand out side panel) It does a restart.
- Neo4j Enterprise Edition: you copy APOC core jar from /product to the /plugins dir, restart
- Neo4j Community Edition: Extra step to download APOC core and copy to the /plugins dir, restart
- Neo4j AuraDB and AuraDS tiers have a subset of APOC core. It has the parts that neo4j-graphrag needs.

## GDS is need
- Neo4j Desktop version, can install the GDS plugin (expand out side panel) It does a restart.
- Neo4j Enterprise server: you copy GDS jar from /labs to the /plugins dir, restart
- Neo4j Community server: Extra step to download GDS jar and then copy to the /plugins dir, restart
- Neo4j AuruDB doesn't have GDS. Would have to also use with Neo4j Graph Analytics Serverless or Neo4j AuraDS
- Neo4j AuraDS has it

## Python versions supported by neo4j-graphrag:
- Python 3.12
- Python 3.11
- Python 3.10
- Python 3.9

# Usage

## To Configure
1. Copy dot-env-sample.txt to .env to configure for your CMIS repository, Neo4j server, whether to use openai,
and what models to use for openai and ollama
2. Also configure in .env what folder you have GraphRAG documents (pdf only for now). Start with a folder with just
ome doc (I sed the cmispress.pdf file in this proect ). FOLDER_PATH="/Shared/GraphRAG"  Note paths follow the CMIS standard way of specifying paths. 
3. Also configure in .env the question to ask
4. in neo4j-util.py you can figure to enable schema an configure entities and relationships
(Note LLMs have gotten good at enntity recognition, that is more to  restrict)

## To Build
1. Setup virtual env
python -m venv  .my-venv
2. Activatge venv  (or to reactivate if closed terminal window)
Windows: .my-venv\Scripts\activatate
Linux / Mac: source .my-venv/bin/activate
(note use deactivate when all done not now)
3. pip install -r requirements.txt
4. For ollama pull llm model and embedding model
ollama pull llama3.18b
ollama pull mxbai-embed-large

## Running
1. Have alresco and neo4j running
2. Run or debug in ide supporting python (VSCode, Cursor, PyCharm, Windsurf, etc.)
3. Or run: pythoon cmis-graphrag on the command line
4. Note cmis-graphrag-date-time.log files created
5. Get answer to your configured question
Query: Who started CMIS
Answer: {'answer': 'The Content Management Interoperability Services (CMIS) draft specification was developed and contributed to by a group of leading ECM vendors, including Alfresco, EMC, IBM, Microsoft, OpenText, Oracle, and SAP. Alfresco Software announced the availability of the first CMIS draft implementation and is a contributing member of the draft technical specification.'}
2025-06-10 17:49:30,591 - INFO - Neo4j connection closed

## Note: you can see whats going on in a Neo4j console with:
- MATCH (n) RETURN n limit 25
- MATCH (n) RETURN n
- SHOW INDEXES

## Screen Shot of KG that gets built in Neo4j for cmispress.pdf
[KG graph in console](https://github.com/stevereiner/cmis-graphrag/blob/main/KG%20graph%20in%20console.png)

## You can cleanup with (don't touch other indexes):
- MATCH (n) DETACH DELETE n
- MATCH (n) RETURN n
- DROP INDEX __entity__id IF EXISTS
- DROP INDEX vector_index_openai IF EXISTS
- DROP INDEX vector_index_ollama IF EXISTS
- SHOW INDEXES


