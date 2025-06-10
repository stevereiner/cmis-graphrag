# cmis-graphrag

Python sample: CMIS folder content with Neo4j KG build and GraphRAG with neo4j-graphrag

For CMIS the cmislib package was used

For Neo4j KG building and GraphRAG the Neo4j neo4j-graphrag packaged was used

For reference info on neo4j-graphrag and other libraries supporting KG building, 
vector embeddings / RAG, and KG graphs / GraphRAG :

[Libraries Supporting KG building and GraphRAG](https://github.com/stevereiner/cmis-graphrag/blob/main/Libraries%20Supporting%20KG%20building%20and%20GraphRAG.md)

Supports using OpenAI (gpt-4.1 etc.) or Ollama LLMs (llmma3.1 etc.) models

Your doc mgt server needs to support CMIS 1.1 (like Alfresco)


## Requirements for  neo4j-graphrag package

## Your Neo4j server 
Neo4j versions supported:
Neo4j >=5.18.1

You can use:
Self Hosted enerterprise server
Free self hosted community server (requiring enterprise is not documented)
Free Neo4j desktop (has enterprise version in it) (was testing with this)
Neo4j AuraDB cloud service >=5.18.0 (Not free or professional tier since need GDS)
Think need either AuraDS or AuraDB business critical with GDS sessions or with AuraDS integration
Also AuraDB includes a only subset of APOC Core functions and procedures, nor you can config
APOC Full is not available in any AuraDB tier for security reasons

1. APOC and GDS plugins install not needed in AuraDBs (see above for restrictions)
2. Enterprise server: you copy gds jar copy from your /product and apoc jar from /labs to the /plugins dir, restart
3. Community server: Extra step to download apoc and gds jars and copy to the /plugins dir, restart
4. In the Neo4j Desktop version, you can install the plugins in the expand out side panel in the GUI. It does a restart 
whith each plugin you enable

## Python versions supported by neo4j-graphrag:
Python 3.12
Python 3.11
Python 3.10
Python 3.9

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
2. Run or debug in ide supporting python (Visul Studio Code or Cursor)
3. Or run: pythoon cmis-graphrag
4. Note cmis-graphrag-date-time.log files created
5. Get answer to your configured question
Query: Who started CMIS
Answer: {'answer': 'The Content Management Interoperability Services (CMIS) draft specification was developed and contributed to by a group of leading ECM vendors, including Alfresco, EMC, IBM, Microsoft, OpenText, Oracle, and SAP. Alfresco Software announced the availability of the first CMIS draft implementation and is a contributing member of the draft technical specification.'}
2025-06-10 17:49:30,591 - INFO - Neo4j connection closed

## Note can set whats going a neo4j console with
MATCH (n) RETURN n limit 25
MATCH (n) RETURN n
SHOW INDEXES

# KG that gets built in Neo4j for cmispress.pdf
[KG graph in console](https://github.com/stevereiner/cmis-graphrag/blob/main/KG%20graph%20in%20console.png)

## Can cleanup with (don't touch other indexes)
MATCH (n) DETACH DELETE n
MATCH (n) RETURN n
DROP INDEX __entity__id IF EXISTS
DROP INDEX vector_index_openai IF EXISTS
DROP INDEX vector_index_ollama IF EXISTS
SHOW INDEXES


