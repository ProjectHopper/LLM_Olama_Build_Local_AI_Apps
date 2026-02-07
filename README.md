# Build_Local_AI_Apps

## 🛠️ Introduction to Olama



"Olama is an open-source tool that simplifies running large language models locally on your personal computer."



## 🧠 What is Olama?




Avoids cloud-based services and paid APIs (e.g., OpenAI ChatGPT).



Features a  Command Line Interface (CLI) to manage installation and execution of models.






Enhances privacy and security by keeping data local.



Reduces costs by eliminating API calls and server usage fees.



Reduces latency by running models on local hardware (no network delay).



Allows customization and fine-tuning of models for specific needs.



## ⚙️ Key Features of Olama



Model Management- 
Easily download, switch, and manage multiple LLMs locally





Unified Interface- 
Interact with different models via consistent CLI commands





Extensibility-
Add custom models and extensions





Performance Optimizations-
Utilize local hardware including GPU acceleration if available



## 💻 System Requirements & Setup





Supported OS: Mac, Linux, Windows



Recommended at least 10 GB free storage (models can be large)



Modern CPU processor required



Python and a code editor (e.g., VS Code) needed for development



## Download and install Olama from the official website (olama.com)



Installation involves downloading a zip file and running the app



After installation, run models like llama 3.2 via CLI using commands such as:

### olama run llama 3.2
in your Command






CLI commands include /show info, /clear, /help, /exit



## 🧩 Understanding Models in Olama

Model Flavors and Parameters



Parameters refer to internal weights and biases learned during training.



More parameters generally mean better performance but require more compute.



Context Length: Max tokens model can ingest at once (e.g., 131,072 tokens for long documents).



Embedding Length: Dimensionality of vector representations for tokens (e.g., 372 dimensions).



Quantization: Technique to reduce model size and improve efficiency by lowering precision (e.g., 4-bit quantization).

## Model Examples





llama 3.2 3B: Default model, balanced performance.



llama 3.2 1B: Smaller model, lighter resource usage.



Larger models (e.g., 8B, 70B, 405B) exist but require significant storage and compute.




## 🖼️ Multi-Modal Models





Some models like Lava support both text and image inputs.



Example: Upload an image to the model, it describes the content (e.g., flowers in a photo).



Useful for vision + language tasks.



## 🔄 Using the REST API





Olama runs a local server (default: localhost:11434).



REST endpoints available for generating text, chatting, model management, etc.



Example curl request to generate text:

    curl -X POST "http://localhost:11434/api/generate" \
     -d '{"model": "llama 3.2", "prompt": "Why is the sky blue?", "stream": false}'






stream: true streams partial responses; stream: false waits for full response.



Chat endpoint accepts messages as:

    {
      "model": "llama 3.2",
      "messages": [{"role": "user", "content": "Tell me a fun fact about Portugal"}]
    }




## 🐍 Python Integration with Olama

Using REST API in Python (Requests)





Create a virtual environment and install requests.



Example to send a prompt and receive streamed response:

    import requests
    import json

    url = "http://localhost:11434/api/generate"
    data = {
      "model": "llama 3.2",
      "prompt": "Tell me a short funny story",
      "stream": True
    }

    response = requests.post(url, json=data, stream=True)
    if response.status_code == 200:
        for line in response.iter_lines():
            if line:
                print(json.loads(line.decode())['text'], end='')


### Using Olama Python SDK





Install the SDK: pip install olama



Example to list models:

    import olama

    response = olama.list()
    print(response)






Example to chat:

    response = olama.chat(
    model="llama 3.2",
    messages=[{"role": "user", "content": "Why is the sky blue?"}]
    )
    print(response['choices'][0]['message']['content'])












## 📚 Retrieval Augmented Generation (RAG) Systems

### What is RAG?





Combines document retrieval with LLM generation.



Documents are split into chunks.



Chunks are converted to embeddings (vector representations).



Embeddings are stored in a vector database.



Queries are embedded and searched in the vector DB to find relevant chunks.



Relevant chunks + query are passed to LLM to generate accurate, context-aware answers.

### Problems Solved by RAG







Problem: 

Limited LLM Knowledge- 
Inject external documents for context



Hallucination- Provide factual data from documents

Scalability- Efficient search in vector DB before generation



## ⚙️ Building a Simple RAG System with Olama and LangChain





Load documents (PDFs, text, URLs) using unstructured or LangChain loaders.



Split documents into chunks (e.g., 1200 tokens with 300 overlap).



Use Olama embeddings model (e.g., nomic embed text) to embed chunks.



Store embeddings in vector DB (e.g., Chroma).



Use LangChain's multi-query retriever to:





Generate multiple query variants.



Search vector DB for relevant chunks.



Pass retrieved chunks and query to Olama LLM (llama 3.2) for response.



Use LangChain's prompt templates and chains to coordinate the process.



## 🔗 Vector Embeddings and Vector Databases Overview







Concept

Embeddings-
Vector representations of text preserving semantic meaning





Vector Database-
Stores embeddings and original text, supports similarity search



Similarity Search- 
Queries converted to embeddings and matched to nearest document embeddings


Use Cases-
Search, recommendation, classification





Example: "cat" and "kitty" have close embeddings in vector space; "cat" and "run" do not.



Embeddings enable semantic search beyond keyword matching.






## 🚀 Final Notes

Olama democratizes AI by allowing local LLM usage without cloud fees or data leakage.



Flexibility to swap models and embeddings easily.



Supports complex AI applications like RAG systems and multi-agent workflows.



Encouraged to explore different models and customize for your use case.



Use provided code templates and starter packs for faster development.



Practice with CLI, REST API, Python SDK, and UI to fully leverage Olama.



## 📌 Essential Commands and Code Snippets

    # List downloaded models
    olama list

    # Pull a model
    olama pull llama 3.2

    # Run a model
    olama run llama 3.2

    # Remove a model
    olama rm llama 3.2


    # Python chat with Olama SDK
    import olama

    response = olama.chat(
    model="llama 3.2",
    messages=[{"role": "user", "content": "Tell me a fun fact about Portugal"}]
    )
    print(response['choices'][0]['message']['content'])


    # cURL example for generate endpoint
    curl -X POST "http://localhost:11434/api/generate" \
      -d '{"model": "llama 3.2", "prompt": "Why is the sky blue?", "stream": false}'




This guide covers the core material, practical commands, and application examples discussed in the lecture segment on Olama, enabling you to master local LLM usage for development and real-world AI solutions.
