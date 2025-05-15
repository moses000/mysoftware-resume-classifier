# CV Classifier

Welcome to the **CV Classifier**, an AI-powered solution to streamline hiring by automatically screening CVs. This system uses [Cherry Studio AI](https://www.cherry-ai.com/) for document processing and insightful explanations, and scikit-learn for accurate classification, helping businesses save time, find top talent, and reduce recruitment costs.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Issues](https://img.shields.io/github/issues/moses000/mysoftware-resume-classifier)](https://github.com/your-username/cv-classifier/issues)

## 📋 Overview

The CV Classifier automates CV screening by rating resumes as "Good" or "Bad" based on skills, experience, and qualifications. It provides clear explanations for each rating, enabling HR teams to focus on the best candidates. Built with cutting-edge AI, the system is easy to use for businesses and robust for developers.

- **For Business Owners**: Simplifies hiring, saves time, and improves candidate quality.
- **For Developers**: Offers a scalable, secure API with clear technical workflows.

## 📊 Workflows

### Business Flow (For Business Owners)

This high-level flowchart shows how the CV Classifier helps you hire top candidates faster, without technical complexity.

```mermaid
graph TD
    A[Start: Job Applicants<br>Submit CVs] -->|Upload CVs| B[Web Portal]
    B -->|Automatic Screening| C[Smart CV Analyzer]
    C -->|Review Results| D[Get Results:<br>Good/Bad Rating + Explanation]
    D --> E[Hire Top Candidates<br>Faster]
    
    subgraph Why It Works
        W1[Trained on Thousands<br>of CVs] --> C
        W2[Powered by AI<br>(Cherry Studio AI)] --> C
    end
    
    subgraph Business Benefits
        B1[Save Time] --> E
        B2[Find Better Hires] --> E
        B3[Reduce Costs] --> E
    end

How It Works (Business Perspective):

Submit CVs: Applicants upload CVs (PDF, Word, or text) via a user-friendly web portal.
Automatic Screening: The system analyzes CVs instantly, rating them as "Good" (strong candidates) or "Bad" (less suitable).
Clear Results: Each CV gets a rating, a confidence score (e.g., 85%), and an explanation (e.g., "Strong Python skills and relevant experience").
Hire Faster: HR teams prioritize top candidates, saving hours of manual screening.
Why It Works:
Trained on Thousands of CVs: Built using a large dataset to ensure accurate ratings.
Powered by AI: Cherry Studio AI processes CVs and explains results in plain language.


Benefits:
Save Time: Automates screening, reducing HR workload.
Better Hires: Identifies candidates with the right skills.
Lower Costs: Cuts recruitment time and resources.



Technical Flow (For Developers)
This sequence diagram illustrates the arrow flow architecture, detailing the interactions between components.
sequenceDiagram
    participant U as User/UI
    participant F as FastAPI Backend
    participant C as Cherry Studio AI
    participant S as Scikit-learn Model
    participant D as Dataset (Kaggle)

    %% Main Workflow
    U->>F: POST /cv/predict (CV File, API Key)
    F->>F: Validate File (Type, Size, API Key)
    alt Invalid Input
        F->>U: Error (400/403)
    else Valid Input
        F->>C: File Processing API (PDF/DOCX/TXT)
        C->>F: Extracted Text
        alt File Processing Error
            F->>U: Error (500)
        else Success
            F->>S: Predict (Text)
            S->>F: Label (Good/Bad), Score
            F->>C: LLM API (Text, Label)
            C->>F: Explanation
            alt LLM Error
                F->>F: Fallback Explanation
            end
            F->>U: Result (Label, Score, Explanation)
        end
    end

    %% Training Phase (Offline)
    note over D: Offline Training
    D->>D: Preprocess (Clean, Label Good/Bad)
    D->>D: Train Model (TfidfVectorizer + LogisticRegression)
    D->>S: Save Model (cherry_exported_model.pkl)
    note over S: Model Loaded by FastAPI

How It Works (Technical Perspective):

User/UI: Users upload CVs via a web interface (HTML) or 3rd-party system, sending a POST request to the FastAPI endpoint.
FastAPI Backend: Validates inputs (file type: PDF/DOCX/TXT, size <5MB, API key), coordinates processing, and returns results.
Cherry Studio AI:
File Processing: Extracts text from CVs using the file processing API (https://api.cherry-ai.com/v1/file-process).
Explanations: Generates human-readable explanations using the LLM API (https://api.cherry-ai.com/v1/completions).


Scikit-learn Model: A pre-trained model (TfidfVectorizer + LogisticRegression) classifies CVs as "Good" (1) or "Bad" (0) with a confidence score.
Kaggle Dataset: The system is trained on the Updated Resume Dataset, preprocessed to label CVs.
Error Handling:
Invalid inputs return HTTP 400/403 errors.
API failures trigger HTTP 500 or fallback explanations.


Output: JSON response with result ("Good"/"Bad"), score (e.g., 0.85), and explanation (e.g., "Strong Python skills").

🛠️ Setup
Prerequisites

Tools: Python 3.11+, pip, Git
Accounts:
Kaggle for dataset access
Cherry Studio AI for API keys (see docs.cherry-ai.com)


Optional: Docker for deployment

Installation

Clone the repository:
git clone https://github.com/your-username/cv-classifier.git
cd cv-classifier


Create a virtual environment and install dependencies:
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt


Set environment variables:
cp .env.example .env

Edit .env with your API_KEY (for FastAPI) and CHERRY_API_KEY (from Cherry Studio AI).


🚀 Usage

Prepare the Dataset:

Download UpdatedResumeDataSet.csv.
Preprocess it:python preprocess_dataset.py


Output: cv_dataset_clean.csv


Train the Model:
python train_sklearn.py


Output: models/cherry_exported_model.pkl


Run the FastAPI Server:
uvicorn main:app --host 0.0.0.0 --port 8000


Access the API at http://localhost:8000/docs.


Use the Web Portal:
python -m http.server 8001


Open http://localhost:8001 to upload CVs and view results.



🌐 Deployment
Local Deployment

Ensure models/cherry_exported_model.pkl exists.
Run the FastAPI server and web portal as above.

Docker Deployment
docker build -t cv-classifier .
docker run -p 8000:8000 -e API_KEY=your-secret-key -e CHERRY_API_KEY=your-cherry-api-key cv-classifier

Cloud Deployment

Deploy on Render or Railway:
Push to GitHub.
Set requirements.txt and start command: uvicorn main:app --host 0.0.0.0 --port 8000.
Configure API_KEY and CHERRY_API_KEY in the platform’s dashboard.



💼 Business Benefits

Save Time: Automates CV screening, reducing HR workload by hours.
Better Hires: Identifies top candidates based on skills and experience.
Lower Costs: Cuts recruitment time and resources.
Easy to Use: No technical skills needed for HR teams.
Scalable: Handles hundreds of CVs with consistent accuracy.

🛠️ Troubleshooting

Diagram Not Rendering:
Ensure `````mermaid is used in Markdown.
Test in Mermaid Live Editor.
Refresh the page or check for syntax errors.


API Issues:
Verify CHERRY_API_KEY and endpoints at docs.cherry-ai.com.
Check file size (<5MB) and type (PDF/DOCX/TXT).


Model Errors:
Ensure models/cherry_exported_model.pkl exists.
Rerun train_sklearn.py if missing.


CORS Errors:
Add UI domain (e.g., http://localhost:8001) to allow_origins in main.py.



🤝 Contributing
Contributions are welcome! Please:

Fork the repository.
Create a feature branch (git checkout -b feature/xyz).
Commit changes (git commit -m "Add xyz feature").
Push to the branch (git push origin feature/xyz).
Open a pull request.

📜 License
This project is licensed under the MIT License. See LICENSE for details.
📬 Contact
For questions, open an issue or contact your-email@example.com.

Built with ❤️ by [Imoleayo Moses] to revolutionize hiring with AI.```
