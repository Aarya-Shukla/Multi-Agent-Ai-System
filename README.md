🤖 Multi-Agent AI System
A sophisticated multi-agent AI system that intelligently classifies and processes PDF, JSON, and Email inputs with shared context management and agent orchestration.
🎯 Project Overview
This system demonstrates advanced AI agent coordination by:

Automatically classifying input format (PDF/JSON/Email) and intent (Invoice/RFQ/Complaint/etc.)
Routing requests to specialized processing agents
Maintaining shared context across processing chains
Enabling traceability through thread management

🏗️ System Architecture
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   User Input    │───▶│ Classifier Agent │───▶│ Specialized     │
│ (PDF/JSON/Email)│    │                  │    │ Processing      │
└─────────────────┘    │ • Format Detection│    │ Agents          │
                       │ • Intent Analysis │    └─────────────────┘
                       │ • Routing Logic  │             │
                       └──────────────────┘             │
                                │                       │
                                ▼                       ▼
                       ┌──────────────────┐    ┌─────────────────┐
                       │ Shared Memory    │◀───│ Processing      │
                       │                  │    │ Results         │
                       │ • SQLite Storage │    │ • Extracted Data│
                       │ • Thread Tracking│    │ • Anomalies     │
                       │ • Context Mgmt   │    │ • Metadata      │
                       └──────────────────┘    └─────────────────┘
Core Components
1. Classifier Agent 🧠

Input: Raw file/email/JSON content
Functions:

Format classification (PDF/JSON/Email)
Intent detection using LLM (Invoice/RFQ/Complaint/Regulation/General)
Intelligent routing to appropriate agent


Technology: OpenAI GPT integration for intent analysis

2. JSON Agent 📊

Purpose: Structured data processing and validation
Features:

Schema compliance checking
Data extraction and reformatting
Anomaly detection for missing/invalid fields
Type validation and sanitization



3. Email Agent 📧

Purpose: Email content analysis and CRM preparation
Capabilities:

Sender/recipient extraction
Subject line parsing
Urgency level assessment
Sentiment analysis
CRM-ready formatting
Action item identification



4. Shared Memory Module 💾

Technology: SQLite database for lightweight persistence
Stores:

Processing metadata (source, timestamp, format)
Extracted structured data
Thread/conversation tracking
Anomaly reports


Features: Cross-agent accessibility, thread continuity

🚀 Quick Start
Prerequisites
bashpython >= 3.8
OpenAI API key (for intent classification)
Installation
bash# Clone the repository
git clone <your-repo-url>
cd multi-agent-ai-system

# Install dependencies
pip install -r requirements.txt

# Set your OpenAI API key
export OPENAI_API_KEY="your-api-key-here"
Running the System
Option 1: Web Demo Interface
bashpython demo_api.py
Then visit http://localhost:8000 for the interactive demo.
Option 2: Command Line Testing
bash# Run comprehensive tests
python test_system.py

# Generate sample input files
python sample_inputs.py

# Use the system programmatically
python multi_agent_system.py
📁 Project Structure
multi-agent-ai-system/
├── multi_agent_system.py      # Core system implementation
├── FastAPI.py                # FastAPI web interface
├── sample_inputs.py           # Sample data generator
├── requirements.txt           # Python dependencies
├── README.md                  # This documentation
├── sample_inputs/             # Generated sample files
│   ├── invoice.json
│   ├── rfq.json
│   ├── malformed.json
│   ├── complaint_email.txt
│   ├── rfq_email.txt
│   └── general_email.txt


🎬 Demo Examples
Example 1: Invoice Processing
pythonfrom multi_agent_system import MultiAgentSystem

system = MultiAgentSystem("your-api-key")

invoice_data = {
    "id": "INV-2024-001",
    "type": "invoice", 
    "vendor": "TechCorp Solutions",
    "amount": 2500.00,
    "sender": "billing@techcorp.com"
}

result = system.process_input(invoice_data)
print(f"Classified as: {result.intent.value}")
print(f"Extracted: {result.extracted_data}")
Output:
Classified as: INVOICE
Format: JSON
Extracted: {'id': 'INV-2024-001', 'type': 'invoice', 'vendor': 'TechCorp Solutions', ...}
Anomalies: []

Example 2: Email Complaint Processing
pythoncomplaint_email = """
From: angry.customer@email.com
Subject: URGENT - Defective Product

I am extremely disappointed with my recent purchase. 
The product is defective and I need immediate resolution!
"""

result = system.process_input(complaint_email)
print(f"Intent: {result.intent.value}")
print(f"Urgency: {result.extracted_data['urgency']}")
print(f"Thread ID: {result.thread_id}")
Output:
Intent: COMPLAINT
Urgency: HIGH
Thread ID: a1b2c3d4e5f6
Sender: angry.customer@email.com
CRM Format: Ready for support ticket creation

Sample Test Results
Test Results
Summary

Total Tests: 10
Passed: 7 ✅
Failed: 1 ❌
Warnings: 2 ⚠️
Skipped: 0
Success Rate: 70.0%
Test Run: June 1, 2025 at 21:06:54 UTC

Detailed Results
✅ Passing Tests (7)
JSON Format Detection

Status: PASS
Timestamp: 2025-06-01 21:06:18

JSON Data Extraction

Status: PASS
Details: Extracted 3 fields
Timestamp: 2025-06-01 21:06:18

Email Format Detection

Status: PASS
Timestamp: 2025-06-01 21:06:22

Email Sender Extraction

Status: PASS
Details: Sender: customer@example.com
Timestamp: 2025-06-01 21:06:22

Thread ID Generation

Status: PASS
Details: Thread: 02c62c2aac51
Timestamp: 2025-06-01 21:06:22

Anomaly Detection

Status: PASS
Details: Found 2 anomalies
Timestamp: 2025-06-01 21:06:24

Memory Storage/Retrieval

Status: PASS
Details: Retrieved result for memory_test_001
Timestamp: 2025-06-01 21:06:29

❌ Failed Tests (1)
Thread Continuity

Status: FAIL
Details: Different thread IDs for related emails
Timestamp: 2025-06-01 21:06:39
Action Required: Review thread ID generation logic for email conversations

⚠️ Warning Tests (2)
Invoice Classification

Status: WARN
Details: Classified as GENERAL
Timestamp: 2025-06-01 21:06:44
Note: Expected more specific classification

Complaint Classification

Status: WARN
Details: Classified as GENERAL
Timestamp: 2025-06-01 21:06:54
Note: Expected more specific classification
