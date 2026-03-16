*Two-person group project for the [[Knowledge & Language]] class in which we aim to make a chatbot that can answer questions about the Terraria wiki.*

# Terraria Chatbot (Chatty Guide)

**Chatty Guide** is a conversational agent specialized in the indie game *Terraria* developed for the Knowledge & Language course at the University of Coimbra. It utilizes a Retrieval-Augmented Generation (RAG) pipeline combining a structured Knowledge Graph (RDF/OWL) with Large Language Models to answer complex questions about a selection of game knowledge.
## Features
* **Natural Language Understanding:** Ask questions in plain English (e.g., *"How do I craft an Adamantite Pickaxe?"* or *"What drops from the King Slime?"*).
* **Knowledge Graph Population:** Uses a custom ontology and RDF triple knowledge graph, populated through extracting entities and relations from data scraped from Terraria Wiki, using rule-based and LLM methods.
* **User Query Handling:** Translates natural language queries into SPARQL to retrieve structured data from the knowledge graph, then uses an LLM to generate a natural, in-character response (simulating the Guide NPC).
* **Interactive GUI:** Includes a graphical interface with a chat panel and an interactive visualization of the knowledge graph.
## Project Structure

```text
.
├── data/                   # Data storage
│   ├── kg/                 # Knowledge graph files (.ttl)
│   ├── ontologies/         # Ontology definitions (.owl)
│   └── misc.json           # Miscellaneous data
├── docs/                   # Project documentation
├── scripts/                # Source code
│   ├── gui/                # GUI logic
│   ├── utils/              # Helper modules
│   ├── chatbot.py          # CLI chatbot entry point
│   ├── populate_kg.py      # Knowledge graph population logic
│   ├── retrieve.py         # Web scraping script
│   └── sparql_generator.py # LLM-to-SPARQL logic
├── .env                    # Environment variables (create your own)
└── requirements.txt        # Python dependencies
```
