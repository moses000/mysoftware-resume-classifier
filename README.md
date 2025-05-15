# CV Classifier

Welcome to the **CV Classifier**, an AI-powered solution to streamline hiring by automatically screening CVs. This system uses [Cherry Studio AI](https://www.cherry-ai.com/) for document processing and insightful explanations, and scikit-learn for accurate classification, helping businesses save time, find top talent, and reduce recruitment costs.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Issues](https://img.shields.io/github/issues/your-username/cv-classifier)](https://github.com/your-username/cv-classifier/issues)

## 📋 Overview

The CV Classifier automates CV screening by rating resumes as "Good" or "Bad" based on skills, experience, and qualifications. It provides clear explanations for each rating, enabling HR teams to focus on the best candidates. Built with cutting-edge AI, the system is easy to use for businesses and robust for developers.

- **For Business Owners**: Simplifies hiring, saves time, and improves candidate quality.
- **For Developers**: Offers a scalable, secure API with clear technical workflows.

## 📊 Workflows

### Business Flow (For Business Owners)

This high-level flowchart shows how the CV Classifier helps you hire top candidates faster, without technical complexity.

```mermaid
graph TD
    A[Start: Job Applicants Submit CVs] -->|Upload CVs| B[Web Portal]
    B -->|Automatic Screening| C[Smart CV Analyzer]
    C -->|Review Results| D[Get Results: Good/Bad Rating + Explanation]
    D --> E[Hire Top Candidates Faster]
    
    subgraph Why It Works
        W1[Trained on Thousands of CVs] --> C
        W2[Powered by AI (Cherry Studio AI)] --> C
    end
    
    subgraph Business Benefits
        B1[Save Time] --> E
        B2[Find Better Hires] --> E
        B3[Reduce Costs] --> E
    end
