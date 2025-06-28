# OllamaDesk

## 1. Description

OllamaDesk is a Windows desktop application developed in C# and WPF, designed to function as a client for the Ollama service. The primary function of the software is to provide a user interface for chat-based interaction with local Large Language Models (LLMs).

A principal component of this application is a Retrieval-Augmented Generation (RAG) system. This system enables the LLM to use user-provided documents as a context source for generating responses. All document processing, indexing, and storage operations are performed on the local machine.

## 2. System Components and Features

### 2.1. Core Functionality

- **LLM Chat Interface**: Provides a graphical user interface for sending prompts to and receiving responses from a local Ollama-hosted LLM.
    
- **Model Selection**: Allows the user to switch between different LLMs made available through the Ollama service.
    

### 2.2. Retrieval-Augmented Generation (RAG) System

- **Document Ingestion**: The system accepts documents in the following formats for processing: `.pdf`, `.docx`, `.md`, and `.txt`.
    
- **Document Processing and Chunking**: Documents are parsed and divided into smaller text segments ("chunks"). The chunking process utilizes strategies based on the document's structure, including headings, code blocks, or paragraph delimiters.
    
- **Vector Embedding and Storage**: Text chunks are converted into vector embeddings using a specified Ollama embedding model. The embeddings and associated text are stored in a local SQLite database file.
    
- **Contextual Retrieval**: User queries are vectorized and compared against the stored document vectors using cosine similarity to retrieve relevant chunks.
    
- **Prompt Augmentation**: The content of the retrieved chunks is appended to the user's query to form an augmented prompt, which is then sent to the LLM.
    

### 2.3. Technical Features

- **API Client**: HTTP requests to the Ollama API are managed by a client that incorporates Polly library policies for request retries and circuit-breaker functionality.
    
- **Diagnostics**: A separate diagnostics window is available to display real-time application logs and performance metrics related to the RAG pipeline.
    

## 3. Technical Specifications

- **Framework**: .NET 8
    
- **User Interface**: Windows Presentation Foundation (WPF)
    
- **Design Pattern**: Model-View-ViewModel (MVVM)
    
- **Primary Dependency**: Ollama
    
- **Local Database**: SQLite
    
- **Libraries**:
    
    - `Microsoft.Extensions.DependencyInjection` for dependency management.
        
    - `iText 7` / `BouncyCastle` for PDF processing.
        
    - `DocumentFormat.OpenXml` for DOCX processing.
        
    - `Markdig` for Markdown processing.
        
    - `Polly` for HTTP client resiliency policies.
        

## 4. Prerequisites and Installation

### 4.1. System Requirements

- An operating system capable of running .NET 8 desktop applications (i.e., Windows).
    
- An installed and running instance of the [Ollama service](https://ollama.com/ "null").
    
- At least one chat model and one embedding model must be downloaded via Ollama (e.g., `ollama pull llama3`, `ollama pull nomic-embed-text`).
    

### 4.2. Setup Procedure

1. Clone the repository: `git clone https://github.com/cartigli/Ellelem.git`
    
2. Navigate to the repository directory: `cd Ellelem`
    
3. Open the `ollamidesk.sln` file in a compatible version of Visual Studio (2022 recommended) with the ".NET desktop development" workload installed.
    
4. Build the solution. NuGet packages will be restored automatically.
    
5. Execute the application from Visual Studio.
    

## 5. Configuration

Application settings are defined in the `appsettings.json` file, which is located in the project's output directory after building.

Key configuration parameters include:

- `Ollama:ApiBaseUrl`: The base URL for the Ollama API endpoint.
    
- `Ollama:DefaultModel`: The chat model to be loaded on application startup.
    
- `Ollama:EmbeddingModel`: The model to be used for generating vector embeddings.
    
- `Rag`: Contains parameters for the RAG system, such as `ChunkSize` and `MinSimilarityScore`.
    
- `Storage:BasePath`: The directory for storing application data, including the SQLite database.
    

## 6. Operating Procedure

1. Launch the application executable.
    
2. The default LLM, as specified in `appsettings.json`, will be loaded. To change the model, use the side menu.
    
3. To utilize the RAG system, activate the "Enable RAG" checkbox. This action will display the document library panel.
    
4. Click "Add Document" to select and ingest a local file. The status will indicate when processing is complete.
    
5. Check the box next to one or more documents in the library to include them in the context for the current session.
    
6. Submit a query through the text input box. The system will use the selected documents to generate a response.
    

## 7. License

This software is distributed under the terms of the MIT License. Refer to the `LICENSE` file for details.
