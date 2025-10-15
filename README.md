# 🍷 Wine Knowledge Graph & GraphRAG Project

## 📘 Overview
This project demonstrates how to transform a **tabular dataset** into a **semantic Knowledge Graph (RDF format)** and then use it for **Graph Retrieval-Augmented Generation (GraphRAG)**.

Using the popular [Wine Reviews dataset](https://www.kaggle.com/datasets/zynicide/wine-reviews), we model wines, regions, varieties, and reviews as interconnected entities — creating a graph that can be queried, visualized, and later integrated with **Large Language Models (LLMs)** for reasoning and insights.



The repository is divided into two main tutorials:

1. 🧩 **Notebook 1 — From CSV to RDF Knowledge Graph**  
   Learn how to design an RDF schema, generate triples using `rdflib`, and serialize the graph for querying and visualization.

2. 🤖 **Notebook 2 — GraphRAG for Wine Insights**  
   Explore how to query the knowledge graph, extract semantic context, and combine it with LLMs to build a simple **GraphRAG reasoning pipeline**.

---

## 🍇 Dataset
The project uses the **Wine Reviews dataset**, containing over 130,000 wine descriptions with metadata such as:
- `country`, `province`, `region`, `variety`, `winery`, `points`, `price`, `description`, and `taster`.

The dataset provides a rich foundation for modeling relationships such as:

```
Wine → hasVariety → Variety  
Wine → producedBy → Winery  
Wine → fromRegion → Region  
Region → inCountry → Country  
Review → aboutWine → Wine  
Review → byTaster → Taster
```

These relationships are represented as RDF triples and stored in a serialized `.ttl` (Turtle) file.

---

## 🧠 Project Goals
- ✅ **Demonstrate RDF graph creation** from structured CSV data  
- ✅ **Visualize relationships** among wines, regions, and reviewers  
- ✅ **Showcase semantic querying** using SPARQL  
- ✅ **Extend the graph for reasoning** via a GraphRAG pipeline using LLMs  

---

## 🏗️ Repository Structure

```
wine-knowledge-graph/
│
├── data/
│   ├── wine_reviews.csv               # Original dataset
│   ├── wine_graph.ttl                 # RDF graph (Turtle format)
│
├── notebooks/
│   ├── 01_wine_rdf_tutorial.ipynb     # CSV → RDF tutorial
│   ├── 02_graphRAG_wine_retrieval.ipynb # GraphRAG tutorial
│
├── scripts/
│   ├── rdf_builder.py                 # Helper functions to create triples
│   ├── sparql_queries.py              # Example SPARQL queries
│
├── README.md
└── requirements.txt
```

---

## 🧩 Methodology

1. **Data Preparation**  
   Clean and normalize the dataset (handle missing values, simplify columns).  

2. **Schema Design**  
   Define ontology classes (`Wine`, `Winery`, `Variety`, `Region`, `Country`, `Review`, `Taster`) and predicates (`hasVariety`, `fromRegion`, etc.).  

3. **RDF Graph Construction**  
   Use `rdflib` to generate RDF triples and export them to `.ttl`.  

4. **SPARQL Querying**  
   Query the graph to retrieve insights, e.g.:
   ```sparql
   SELECT ?wine ?region WHERE {
     ?wine a :Wine ; :fromRegion ?region .
   } LIMIT 10
   ```

5. **Graph Visualization**  
   Use `NetworkX` or `PyVis` for visual exploration.  

6. **GraphRAG Integration (Part 2)**  
   Use SPARQL + Python to extract context and feed it into an LLM for natural language reasoning.

---

## 🧰 Technologies Used
- **Python 3.10+**  
- **rdflib** — RDF graph creation and serialization  
- **SPARQLWrapper** — Query interface  
- **NetworkX / PyVis** — Graph visualization  
- **Pandas / NumPy** — Data manipulation  
- **LangChain / FAISS (later)** — Retrieval-Augmented Generation  

---

## 🧮 Example RDF Triples

```turtle
:Wine_001 a :Wine ;
    :hasVariety :Cabernet_Sauvignon ;
    :producedBy :Silver_Oak_Winery ;
    :fromRegion :Napa_Valley ;
    :price "75"^^xsd:decimal ;
    :points "92"^^xsd:integer .

:Napa_Valley a :Region ;
    :inCountry :USA .

:Review_001 a :Review ;
    :aboutWine :Wine_001 ;
    :byTaster :John_Doe ;
    :description "A bold Cabernet with notes of blackberry and vanilla." .
```

---

## 📈 Future Work
- 🧩 Add **flavor extraction** via NLP from review text (`hasFlavor → FlavorNote`)  
- 🧠 Implement **GraphRAG reasoning** with SPARQL + LLMs  
- 🔍 Explore **graph embeddings** for similarity-based recommendations  
- 🎨 Build an interactive dashboard (Streamlit or Neo4j Bloom) for graph exploration  

---

## 🤝 Contributions
This project is open for educational collaboration.  
If you’re interested in improving the schema, adding data sources, or extending GraphRAG experiments, feel free to fork and contribute.

---

## 🧾 License
MIT License © 2025 [Wafaa EL HUSSEINI](https://github.com/wafaahs)

---

## 🌐 Links
- 📘 [Kaggle Notebook (Part 1)](https://www.kaggle.com/code/wafaaelhusseini/) *(Coming soon)* 
- 🧠 [Kaggle Notebook (Part 2)](https://www.kaggle.com/code/wafaaelhusseini/) *(Coming soon)*
