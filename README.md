Resume Shortlister with Multimodal LLM & RAG
An intelligent resume shortlisting system that uses Local Multimodal LLMs (via Ollama) and Retrieval-Augmented Generation (RAG) to find the best candidates based on job requirements. Now with image processing capabilities for analyzing resume images!

Features
Multimodal LLM Integration: Uses Ollama to run multimodal models that can process both text and images

Resume Image Processing: Extracts text from resume images using computer vision capabilities

RAG Pipeline: Retrieval-Augmented Generation for intelligent candidate matching

Vector Database: FAISS for efficient resume storage and retrieval

Lightweight: Optimized for 8GB+ MacBook Air with memory-efficient models

Multiple Models Support: Works with various Ollama models (text-only and multimodal)

Automatic Text Extraction: Converts resume images to searchable text content

Fallback Systems: Graceful degradation when models are unavailable

Prerequisites
macOS (optimized for Apple Silicon)

Python 3.8+

Ollama installed locally

8GB+ RAM recommended (16GB+ for multimodal models)

Installation
1. Install Ollama
bash
# Install Ollama
brew install ollama

# Start Ollama service
ollama serve
2. Download Models
For Text-Only Processing (8GB RAM):
bash
# Recommended models for 8GB MacBook Air
ollama pull phi3:mini    # ~1.8GB - Best choice
ollama pull gemma2:2b    # ~1.6GB - Very lightweight
ollama pull qwen2:0.5b   # ~0.3GB - Smallest option
For Multimodal Processing (16GB+ RAM):
bash
# Multimodal models for image processing
ollama pull llava:latest      # ~4.7GB - Best multimodal
ollama pull bakllava:latest   # ~4.7GB - Alternative multimodal
ollama pull moondream:latest  # ~1.8GB - Lightweight multimodal

# Check available models
ollama list
3. Install Python Dependencies
bash
pip install langchain-community chromadb sentence-transformers faiss-cpu requests pillow python-multipart opencv-python matplotlib
Quick Start
1. Start Ollama Service
bash
# Keep this running in a separate terminal
ollama serve
2. Prepare Resume Images
Place your resume images in the resume_images folder:

Supported formats: JPG, JPEG, PNG, BMP, TIFF, WEBP

Naming convention: candidate_name_resume.jpg (e.g., sarah_chen_resume.jpg)

3. Run the Multimodal Resume Shortlister
python
# Run the complete pipeline
from multimodal_shortlister import shortlist_candidates, extract_text_from_resume

# The system will automatically detect and process resume images
results = shortlist_candidates("Find candidates with Python experience")
print(results)
4. Test Your Setup
python
# Test if multimodal LLM is working
from multimodal_shortlister import test_multimodal_connection

test_multimodal_connection()
Project Structure
text
resume-shortlister-multimodal/
├── multimodal_shortlister.py    # Main multimodal application
├── image_processor.py           # Resume image processing utilities
├── text_extractor.py            # Text extraction from images
├── resume_images/               # Folder for resume images
│   ├── sarah_chen_resume.jpg
│   ├── michael_rodriguez_resume.png
│   └── emily_thompson_resume.jpeg
├── requirements.txt             # Python dependencies
└── README.md                   # This file
Usage Examples
Basic Shortlisting with Text Resumes
python
from multimodal_shortlister import shortlist_candidates

# Find ML engineers with Python experience
results = shortlist_candidates(
    "Find candidates with machine learning and Python experience"
)
print(results)
Shortlisting with Resume Images
python
# The system automatically processes images in resume_images folder
results = shortlist_candidates(
    "Looking for candidates with AWS or Google Cloud experience"
)
Extract Text from Specific Resume Image
python
from multimodal_shortlister import extract_text_from_resume

# Extract text from a specific resume image
extracted_text = extract_text_from_resume("resume_images/john_doe_resume.jpg")
print(extracted_text)
Evaluate Specific Candidate with Image Analysis
python
from multimodal_shortlister import evaluate_candidate_fit

# Detailed evaluation of a specific candidate with image analysis
evaluation = evaluate_candidate_fit(
    "Senior Data Scientist with cloud experience",
    "Sarah Chen"
)
print(evaluation)
How It Works
Image Processing: The system scans the resume_images folder for resume images

Text Extraction: Uses multimodal LLMs to extract text from resume images

Text Parsing: Structures the extracted text into standardized resume format

Vector Storage: Stores processed text in FAISS vector database for efficient retrieval

Query Processing: Matches job requirements against extracted resume content

Multimodal Analysis: Optionally uses image analysis for additional insights

Configuration
Model Selection
The system automatically detects available Ollama models and chooses the best one:

python
# Manual model selection (if needed)
llm = MultimodalOllama(model_name="llava:latest")
Image Processing Settings
python
# Configure image directory
IMAGE_DIR = "your_custom_resume_folder"

# Supported image formats
IMAGE_EXTENSIONS = ['.jpg', '.jpeg', '.png', '.bmp', '.tiff', '.webp']
Memory Optimization
For 8GB MacBook Air:

Use text-only models (phi3:mini, gemma2:2b)

Process images in batches

Enable fallback to text-only mode

For 16GB+ systems:

Use multimodal models (llava:latest)

Process higher resolution images

Enable full image analysis capabilities

Sample Resume Data
The system includes sample resumes for testing:

Sarah Chen: Data Scientist with NLP experience

Michael Rodriguez: ML Engineer with computer vision background

Emily Thompson: Data Engineer with cloud expertise

David Kim: Frontend Developer with UI/UX design skills

Customization
Adding Your Own Resume Images
Place images in the resume_images folder

Name them using the pattern: firstname_lastname_resume.extension

The system will automatically detect and process them

Custom Resume Fields
python
# Add custom fields to extracted resume data
resume_data = {
    "name": "Extracted Name",
    "email": "Extracted Email",
    "experience": "Extracted Experience",
    "education": "Extracted Education",
    "skills": "Extracted Skills",
    "certifications": "Extracted Certifications",
    "projects": "Extracted Projects",
    "summary": "Extracted Summary",
    "image_path": "path/to/resume/image.jpg"
}
Modifying Search Parameters
python
# Adjust retrieval settings
retriever = vectorstore.as_retriever(
    search_kwargs={
        "k": 3,          # Number of candidates to retrieve
        "score_threshold": 0.7  # Similarity threshold
    }
)
Troubleshooting
Common Issues
"Connection refused" error

bash
# Make sure Ollama is running
ollama serve
Model not found

bash
# Download the required model
ollama pull llava:latest
Memory issues on 8GB RAM

bash
# Use lighter models
ollama pull phi3:mini
Multimodal model not available

The system will automatically fallback to text-only mode

Resume images will still be processed using text extraction

Special characters in responses (@@@@@)

bash
# Reinstall corrupted model
ollama rm llava
ollama pull llava
Testing Your Setup
python
# Run comprehensive tests
from multimodal_shortlister import (
    test_multimodal_connection, 
    check_ollama_status,
    test_image_processing
)

# Check Ollama status
check_ollama_status()

# Test multimodal capabilities
test_multimodal_connection()

# Test image processing
test_image_processing()
Performance Tips
Use appropriate models for your hardware:

8GB RAM: Text-only models (phi3:mini, qwen2:0.5b)

16GB+ RAM: Multimodal models (llava:latest)

Optimize image size:

Resize large images before processing

Use JPEG format for smaller file sizes

Process in batches for large numbers of resumes

Close other applications when running intensive queries

Restart Ollama periodically if you experience memory issues

Use specific queries for better results instead of broad searches

Advanced Features
Batch Processing
python
# Process multiple resumes in batch
from multimodal_shortlister import batch_process_resumes

# Process all images in a folder
results = batch_process_resumes("path/to/resumes/folder")
Custom Text Extraction
python
# Customize text extraction prompts
def custom_extraction_prompt(image_path):
    prompt = """Your custom extraction instructions...
    Extract specifically: [your requirements]"""
    return llm.invoke(prompt, image_path)
Integration with Existing Systems
python
# Integrate with existing HR systems
def integrate_with_ats(candidate_data):
    # Your integration code here
    pass
Contributing
Feel free to submit issues and enhancement requests!

Planned Features
PDF resume support

Batch processing optimization

Advanced image preprocessing

Custom field extraction templates

Integration with popular ATS systems

Performance benchmarking tools

Cloud deployment options

License
This project is open source and available under the MIT License.

Support
If you encounter any problems:

Check that Ollama is running: ollama serve

Verify models are downloaded: ollama list

Test the connection: Run the test functions

Check available memory: Ensure you have enough RAM for multimodal processing

For persistent issues with multimodal models, try using text-only mode:

bash
ollama pull phi3:mini
The system will still extract text from resume images but will use text-only models for analysis.

