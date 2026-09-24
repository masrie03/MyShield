#  MyShield 2.0 — AI-Powered Scam Detection

MyShield 2.0 is an AI-powered scam detection system designed to help users identify potentially fraudulent messages and understand the risks associated with them.

The project was developed as a hackathon prototype with a focus on scam detection in the Malaysian context. It combines a lightweight local machine-learning model with Google's Gemini model and grounded information retrieval to provide explainable scam-risk assessments.

## Problem

Online scams frequently rely on urgency, misleading offers, suspicious links, impersonation, and other forms of social engineering.

Rather than simply classifying a message as *scam* or *not scam*, MyShield 2.0 aims to provide users with:

* Scam detection
* Risk-level assessment
* An explanation of the detected risk
* Recommended actions
* Grounded scam-related information

## How It Works

MyShield 2.0 uses a hybrid detection architecture.

```text
User Message
     │
     ▼
┌─────────────────────┐
│    MyShield 2.0     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Local ML Detection  │
│     "Sensor"        │
└──────────┬──────────┘
           │
           │ Scam Probability
           ▼
┌─────────────────────────────┐
│ Gemini AI                   │
│     "Brain"                 │
│                             │
│ • Interprets message        │
│ • Considers ML score        │
│ • Identifies red flags      │
│ • Generates explanation    │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Grounded Scam Information   │
│ Vertex AI Search            │
│ BNM / PDRM-related data     │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Risk Assessment             │
│                             │
│ • Scam / Not Scam           │
│ • Risk Level                │
│ • Explanation               │
│ • Recommended Action        │
└─────────────────────────────┘
```

The local machine-learning component acts as a fast initial signal, while the Gemini-based component performs contextual analysis and combines the available evidence into the final assessment.

## Key Features

### Hybrid AI Detection

Combines traditional machine learning with a Large Language Model rather than relying entirely on a single detection technique.

### Contextual Scam Analysis

Gemini analyses the submitted message for linguistic and contextual indicators of fraudulent behaviour.

### Grounded Retrieval

The AI architecture supports retrieval from a Vertex AI Search datastore containing scam-related information, allowing the system to incorporate external evidence into its assessment.

### Explainable Results

Instead of returning only a classification, the API produces structured output containing:

```json
{
  "is_scam": true,
  "risk_level": "high",
  "explanation": "Explanation of the identified scam indicators.",
  "recommended_action": "Recommended action for the user."
}
```

### Fallback Detection

A rule-based fallback mechanism provides basic detection when the primary AI pipeline fails or produces an invalid response.

## Architecture

The project is organised into several components:

```text
Project-2030/
│
├── ai/
│   └── Scam detection and AI orchestration
│
├── data/
│   └── Project data
│
├── myshield_ui/
│   └── User interface
│
├── services/
│   └── Application service layer
│
├── utils/
│   └── Utility functions
│
├── app.py
│   └── FastAPI application
│
├── main.py
│   └── Main API entry point
│
└── .gitignore
```

## 🛠️ Technology Stack

**Backend**

* Python
* FastAPI
* Pydantic

**Artificial Intelligence**

* Google Gemini 2.5 Flash
* Google Gen AI SDK
* Local machine-learning model
* Joblib

**Cloud & Retrieval**

* Google Cloud
* Vertex AI
* Vertex AI Search

**Application**

* REST API
* Environment-based configuration

## 🔌 API

The FastAPI backend exposes an endpoint for scam detection.

### Request

```http
POST /detect_scam
```

Example request body:

```json
{
  "text": "Congratulations! You won RM5,000. Click this link now to claim your prize."
}
```

### Response

```json
{
  "is_scam": true,
  "risk_level": "high",
  "explanation": "The message contains indicators commonly associated with scam attempts.",
  "recommended_action": "Do not click suspicious links or provide personal information."
}
```

## Running the Backend

Clone the repository:

```bash
git clone <repository-url>
cd Project-2030
```

Create and activate a Python virtual environment.

Install the required project dependencies and configure the required environment variables for the Google Cloud services.

Start the FastAPI development server:

```bash
uvicorn main:app --reload
```

The API can then be accessed through the local FastAPI server.

## Environment Configuration

The application uses environment variables for cloud configuration.

Example:

```env
GOOGLE_CLOUD_PROJECT=your-project-id
DATA_STORE_ID=your-data-store-id
```

Credentials and other secrets should **never be committed to the repository**.

## Prototype Disclaimer

MyShield 2.0 was developed as a hackathon prototype and should not be treated as a production-grade fraud detection or financial-security system.

AI-generated assessments may contain errors, and users should verify suspicious messages through official channels before taking action.

## Project Context

MyShield 2.0 was developed as part of a hackathon project focused on applying AI and modern cloud technologies to a real-world problem.

The project explores how traditional machine learning, generative AI, retrieval, and explainable risk assessment can be combined into a practical scam-detection workflow.

## Author

**Masrie Bukhori**

Master's in Artificial Intelligence
Asia Pacific University of Technology & Innovation (APU)

## License

This repository is intended for educational, research, and portfolio purposes.
