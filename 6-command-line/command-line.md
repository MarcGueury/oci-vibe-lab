# Customize (Adding new files...)

## Introduction
In this lab, we will use the Cline CLI directly. Several time one after each other for automating a complex task. 

Estimated time: 10 min

### Objectives

- Create a migration plan from app_to_migrate to **app_target** flow using several Coding Agent calls,  

### Prerequisites
- The lab 1 and 2 must have been completed.

    ![Architecture](../0-intro/images/lab-migration.png)

## Task 1: Login to the compute

Login to the compute created in lab 2.
- go to the installation directory

```
<copy>
cd oci-vibe
./starter.sh ssh compute
</copy>
```

Or ssh to the machine directly if you have setup it so in lab 3.

```
<copy>
ssh opc@YOUR_COMPUTE_IP
</copy>
```

## Task 2: Check the migration scripts.

The migration script is using several Cline CLI command in a chain. Look at the migration script 

```
<copy>
cd migration
cat migration_plan.sh
</copy>
```

You will find several commands like this:

````
<copy>
cline -y > /tmp/cline_cli.log << EOF
You are a senior software engineer and technical writer.

Goal:
Analyze the provided source code of an application and generate comprehensive, structured technical documentation suitable for engineers who need to understand, maintain, or migrate the system.

Input:
- Source code. Check the current directory.

Tasks:

1. System Overview
   - Describe the purpose of the application
   - Identify main use cases
   - High-level architecture (monolith, microservices, layers, etc.)

....

Output Files:
- User Manual: USER.md
- Technical Manual: TECH.md

Output format:
- Well-structured documentation with clear sections
- Use diagrams in text form where helpful (e.g., component interactions)
- Be precise and avoid guessing—flag uncertainties explicitly
EOF
</copy>
````

## Task 3: Run the migration script

Back in the terminal. 
1. Run the script
    ```
    <copy>
    ./migration_plan.sh
    </copy>
    ```
    ![Migration](images/cline-cli1.png)  

The result will looks like this:

---

### Executive Summary

The app_to_migrate is a specialized Retrieval-Augmented Generation (RAG) system for HR policies and procedures. It uses Oracle DB for storing PDF policies (as BLOBs), advanced PDF parsing/OCR/chunking, Oracle Vector Store for semantic search, and OCI Cohere models for embeddings and chat completions. It is integrated with Oracle APEX frontend, supports user personalization (based on grade, service years, etc.), mathematical calculations in responses, source attribution with Object Storage links, and on-demand embedding creation. The backend consists of two Python Flask services.

The app_target is a modern full-stack conversational AI agent application using LangGraph (ReAct agent), OCI Generative AI (primarily gpt-oss-120b or alternatives), a Model Context Protocol (MCP) server for dynamic tools, a rich web UI with streaming, voice input, multi-language support, Mermaid diagram generation, and Oracle DB integration for structured data (DEPT table). It emphasizes research tasks, avoids math calculations, supports authentication (IDCS/JWT or simulated), user context propagation to tools, and modern deployment (Nginx, Docker/K8s ready).

**Overall Migration Feasibility**: Medium-High. Target's agent framework and UI can serve as a strong foundation; development needed for RAG pipeline, PDF processing, and HR prompt/logic.

### Feature Comparison Table

| Feature Name | Description | Present in app_to_migrate | Present in app_target | Gap Type |
|--------------|-------------|---------------------------|-----------------------|----------|
| Natural Language HR Querying | Ask questions about policies, leave, benefits, loans; grounded in documents | Yes | Partial (research-focused agent, no HR docs/RAG) | partial |
| RAG Pipeline with Vector Search | Semantic retrieval from chunked HR PDFs using OracleVS or Qdrant | Yes | No | missing |
| Document Ingestion & Embedding | Advanced PDF parsing (text, tables to MD, bold topics, OCR/Tesseract for images), chunking (1500/150), on-demand via API from DB BLOBs | Yes | No | missing |
| User Personalization & Math Calculations | Inject userDetails (grade, years, kids); prompt for tailored responses incl. leave/loan calcs | Yes | No (prompt avoids math; user context for tools only) | missing |
| Source Attribution with Links | Response includes HTML links to Object Storage PDFs with page numbers | Yes | Partial (tool results as tables; no doc sources) | partial |
| Chat History Support | previous_chat_message/reply params for conversation continuity | Yes | Yes (threaded conversations in LangGraph) | equivalent |

---

![Migration](images/cline-cli2.png)  

Congratulation for finishing the lab. We hope that you learned something useful !! 

## Acknowledgements

- **Author**
    - Marc Gueury, Generative AI Specialist
    - Ilayda Temir, Generative AI Specialist
