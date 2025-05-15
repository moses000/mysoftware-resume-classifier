# CV Classifier

This repository implements a CV classification system using Cherry Studio AI (https://www.cherry-ai.com/) for document processing and explanations, and scikit-learn for text classification.

## 📊 Workflow Diagram

The following sequence diagram illustrates the arrow flow architecture of the CV classification system:

```mermaid
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
