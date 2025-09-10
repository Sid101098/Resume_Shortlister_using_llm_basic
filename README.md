# Resume_Shortlister_using_llm_basic
A python notebook which lets you shortlist resume based on keywords using LLM models
# Resume Shortlister with LLM & RAG

An intelligent resume shortlisting system that uses Local LLMs (via Ollama) and Retrieval-Augmented Generation (RAG) to find the best candidates based on job requirements.

##  Features

- **Local LLM Integration**: Uses Ollama to run models locally on your machine
- **RAG Pipeline**: Retrieval-Augmented Generation for intelligent candidate matching
- **Vector Database**: FAISS/Chroma for efficient resume storage and retrieval
- **Lightweight**: Optimized for 8GB MacBook Air with memory-efficient models
- **Multiple Models Support**: Works with various Ollama models
- **Fallback Systems**: Graceful degradation when models are unavailable

## Prerequisites

- macOS (optimized for Apple Silicon)
- Python 3.8+
- Ollama installed locally
- 8GB+ RAM recommended

##  Installation

### 1. Install Ollama
```bash
# Install Ollama
brew install ollama

# Start Ollama service
ollama serve
```

### 2. Download Lightweight Models (for 8GB RAM)
```bash
# Recommended models for 8GB MacBook Air
ollama pull phi3:mini    # ~1.8GB - Best choice
ollama pull gemma2:2b    # ~1.6GB - Very lightweight
ollama pull qwen2:0.5b   # ~0.3GB - Smallest option

# Check available models
ollama list
```

### 3. Install Python Dependencies
```bash
pip install langchain-community chromadb sentence-transformers faiss-cpu requests
```

##  Quick Start

### 1. Start Ollama Service
```bash
# Keep this running in a separate terminal
ollama serve
```

### 2. Run the Resume Shortlister
```python
# Run the complete pipeline
python resume_shortlister.py
```

### 3. Test Your Setup
```python
# Test if LLM is working
from llm_test import test_llm_connection
test_llm_connection()
```

##  Project Structure

```
resume-shortlister/
├── main.py                 # Main application
├── llm_test.py            # LLM connection testing
├── resume_data.py         # Sample resume data
├── vector_store.py        # Vector database management
├── requirements.txt       # Python dependencies
└── README.md             # This file
```

##  Usage Examples

### Basic Shortlisting
```python
from main import shortlist_candidates

# Find ML engineers with Python experience
results = shortlist_candidates(
    "Find candidates with machine learning and Python experience"
)
print(results)
```

### Cloud Experts Search
```python
# Find candidates with cloud experience
results = shortlist_candidates(
    "Looking for candidates with AWS or Google Cloud experience"
)
```

### Senior Developers
```python
# Find senior developers with leadership experience
results = shortlist_candidates(
    "Need senior developers with team leadership and architecture experience"
)
```

##  Configuration

### Model Selection
The system automatically detects available Ollama models and chooses the best one. You can manually specify a model:

```python
# Manual model selection
llm = LightweightOllama(model_name="phi3:mini")
```

### Memory Optimization
For 8GB MacBook Air, the system is pre-configured with:
- Lightweight embedding model (`all-MiniLM-L6-v2`)
- FAISS vector store (memory-efficient)
- Response length limiting
- Batch processing optimization

##  Troubleshooting

### Common Issues

1. **"Connection refused" error**
   ```bash
   # Make sure Ollama is running
   ollama serve
   ```

2. **Model not found**
   ```bash
   # Download the model
   ollama pull phi3:mini
   ```

3. **Memory issues**
   ```bash
   # Use lighter models
   ollama pull qwen2:0.5b
   ```

4. **Special characters in responses (@@@@@)**
   ```bash
   # Reinstall corrupted model
   ollama rm phi
   ollama pull phi
   ```

### Testing Your Setup

```python
# Run comprehensive tests
from llm_test import comprehensive_llm_test, check_ollama_status

# Check Ollama status
check_ollama_status()

# Test LLM responses
comprehensive_llm_test()
```

## Sample Resume Data

The system includes sample resumes for testing:
- Sarah Chen: Data Scientist with NLP experience
- Michael Rodriguez: ML Engineer with computer vision background
- Emily Thompson: Data Engineer with cloud expertise

## Customization

### Adding Your Own Resumes
```python
# Add custom resumes
custom_resumes = [
    {
        "id": 101,
        "name": "John Smith",
        "email": "john.smith@email.com",
        "experience": "Senior Developer with 5+ years experience...",
        "education": "BS Computer Science, MIT",
        "skills": "Python, JavaScript, React, Node.js",
        "certifications": "AWS Certified Developer"
    }
    # Add more resumes...
]
```

### Modifying Search Parameters
```python
# Adjust retrieval settings
retriever = vectorstore.as_retriever(
    search_kwargs={
        "k": 3,          # Number of candidates to retrieve
        "score_threshold": 0.7  # Similarity threshold
    }
)
```

## Performance Tips

1. **Use lighter models** for better performance on 8GB RAM
2. **Close other applications** when running intensive queries
3. **Restart Ollama** periodically if you experience memory issues
4. **Use specific queries** for better results instead of broad searches

##  Contributing

Feel free to submit issues and enhancement requests!

##  License

This project is open source and available under the MIT License.

##  Support

If you encounter any problems:
1. Check that Ollama is running: `ollama serve`
2. Verify models are downloaded: `ollama list`
3. Test the connection: `python llm_test.py`

For persistent issues, try using the smallest model:
```bash
ollama pull qwen2:0.5b
```

---
