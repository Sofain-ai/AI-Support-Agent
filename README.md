# AI-Support-Agent
KI-Assistent für das Planovo-Handbuch auf Basis von RAG mit n8n, OpenAI-Embeddings und Qdrant.


Das System verwendet n8n Workflows, OpenAI Embeddings und die Qdrant Vektordatenbank, um Fragen zum Planovo-Handbuch zu beantworten.
Der Assistent durchsucht relevante Inhalte aus dem Handbuch und nutzt diese als Kontext, um eine passende Antwort zu generieren.

rchitektur

Das System arbeitet mit einer Retrieval-Augmented-Generation Pipeline.

Benutzerfrage
      ↓
Embedding (OpenAI)
      ↓
Vektorsuche (Qdrant)
      ↓
Relevanter Kontext
      ↓
AI Agent (GPT-4)
      ↓
Generierte Antwort

Workflows

Das Projekt besteht aus zwei Workflows.

1. Datenverarbeitung Workflow

Dieser Workflow bereitet das Handbuch für die semantische Suche vor.

Schritte:

Einlesen der Textdatei

Extraktion des Textinhalts

Aufteilung in kleinere Textabschnitte (Chunks)

Erstellung von Embeddings mit OpenAI

Speicherung der Embeddings in Qdrant


Pipeline

Read File → Extract Text → Chunking → Embedding → Qdrant

Dieser Workflow wird einmal ausgeführt, um die Wissensbasis zu erstellen.



2. Chat Workflow

Dieser Workflow beantwortet Benutzerfragen.

Schritte:

Benutzer stellt eine Frage

Erstellung eines Embeddings für die Frage

Vektorsuche in Qdrant

Abrufen relevanter Textabschnitte

Erstellung eines Kontextes

Übergabe an den AI Agent

Generierung der Antwort

Pipeline:
Chat Message → Embedding → Qdrant Search → Kontext → AI Agent → Antwort




Verwendete Technologien

n8n

OpenAI API

Qdrant

Docker

JavaScript (n8n Nodes)



Qdrant starten

Qdrant wird lokal über Docker gestartet.



docker run -p 6333:6333 qdrant/qdrant


Danach ist Qdrant erreichbar unter:
http://localhost:6333

Verwendete Collection:
planovo_handbook


Vektorkonfiguration:
Dimension: 1536
Distance: Cosine


AI-Support-Agent
│
├── workflows
│   ├── chat-workflow.json
│   └── data-ingestion-workflow.json
│
├── screenshots
│   ├── workflow-chat.png
│   └── workflow-ingestion.png
│
└── README.md
