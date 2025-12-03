# 🏥 Ophthalmology AI - Clinical Decision Support System

A full-stack AI-powered web application for diabetic retinopathy detection and clinical report generation.

![Next.js](https://img.shields.io/badge/Next.js-14-black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)
![Python](https://img.shields.io/badge/Python-3.11-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 📋 Overview

This system combines state-of-the-art computer vision (ConvNeXt-Tiny) with vision-language models (Llama 3.2-Vision 11B) to provide:
- **Automated DR screening** across 5 severity levels
- **Multi-condition detection** for 13 retinal abnormalities
- **AI-generated clinical reports** with treatment recommendations
- **Real-time analysis** with comprehensive visualizations

### 📊 Performance Metrics
| Metric | Value |
|--------|-------|
| Overall AUROC | 83.5% |
| Diabetic Retinopathy AUROC | 98.7% |
| Training Dataset | 60,000+ fundus images |
| Conditions Detected | 13 retinal abnormalities |
| Severity Levels | 5 (No DR, Mild, Moderate, Severe, Proliferative) |

## 🏗️ System Architecture
```
┌─────────────────────────────────────────────────────────────┐
│                 USER INTERFACE (Browser)                    │
│            Next.js 14 + TypeScript + Tailwind               │
└─────────────────────────┬───────────────────────────────────┘
                          │ HTTP/REST API
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                 BACKEND API (Flask)                         │
│            Python 3.11 + Flask + CORS                       │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│              AI INFERENCE PIPELINE                          │
│                                                             │
│  1. Vision Model: ConvNeXt-Tiny (PyTorch)                   │
│     - Input: 224x224 fundus images                          │
│     - Output: 13 conditions + 5 severity levels             │
│     - Performance: 83.5% AUROC                              │
│                                                             │
│  2. VLM: Llama 3.2-Vision 11B (Ollama)                      │
│     - Input: Image + Vision model predictions               │
│     - Output: Clinical reports                              │
│     - RAG: Medical knowledge base integration               │
└─────────────────────────────────────────────────────────────┘
```

## 🛠️ Tech Stack

### Frontend
- **Framework:** Next.js 14 (App Router)
- **Language:** TypeScript 5
- **Styling:** Tailwind CSS 4
- **UI Components:** shadcn/ui + Radix UI
- **State Management:** Zustand (with persist)
- **Charts:** Recharts
- **Animations:** Framer Motion

### Backend
- **API Server:** Flask 3.0
- **Image Processing:** OpenCV, Pillow
- **Deep Learning:** PyTorch 2.1, torchvision
- **Vision Model:** ConvNeXt-Tiny (timm)
- **VLM:** Llama 3.2-Vision 11B (Ollama)

### AI/ML Models

**1. Vision Model (ConvNeXt-Tiny)**
- Architecture: ConvNeXt-Tiny with custom multi-task head
- Parameters: 38.4M
- Input: 224x224 RGB fundus images
- Tasks: Binary classification (13 conditions) + Multi-class (5 DR severity levels)

**2. Vision-Language Model (Llama 3.2-Vision 11B)**
- Purpose: Clinical report generation
- Input: Fundus image + vision model predictions
- Output: Structured clinical reports with RAG-enhanced recommendations

## 📁 Project Structure
```
ophthalmology-ai-nextjs/
├── app/                          # Next.js app directory
│   ├── dashboard/                # Analysis dashboard page
│   ├── history/                  # Analysis history page
│   ├── layout.tsx                # Root layout
│   ├── page.tsx                  # Home page
│   └── globals.css               # Global styles
├── components/
│   ├── analysis/                 # Analysis-related components
│   │   ├── SeverityGauge.tsx     # Animated severity display
│   │   ├── PredictionsTable.tsx  # Conditions table
│   │   ├── ImagePreview.tsx      # Image viewer with zoom
│   │   ├── ClinicalReport.tsx
│   │   └── ExportButtons.tsx
│   ├── layout/
│   │   └── Navbar.tsx
│   └── ui/                       # shadcn/ui components
├── lib/
│   ├── api.ts                    # API client for Flask backend
│   ├── types.ts                  # TypeScript definitions
│   └── utils.ts
├── stores/
│   └── analysisStore.ts          # Zustand state management
├── python-backend/
│   ├── app.py                    # Flask API server
│   ├── requirements.txt
│   └── uploads/
└── public/
```

## ⚡ Installation & Setup

### Prerequisites
- Node.js 20+
- Python 3.11+
- CUDA-capable GPU (recommended)
- Ollama

### 1. Clone Repository
```bash
git clone https://github.com/YourUsername/ophthalmology-ai-nextjs.git
cd ophthalmology-ai-nextjs
```

### 2. Frontend Setup
```bash
npm install
```

### 3. Backend Setup
```bash
cd python-backend
pip install -r requirements.txt
```

### 4. Install Ollama and Pull Model
```bash
# Install Ollama from https://ollama.ai
ollama pull llama3.2-vision:11b
```

### 5. Configure Environment
```bash
# Create .env.local in root directory
NEXT_PUBLIC_API_URL=http://localhost:8000
```

## 🚀 Running the Application

You need **3 terminals**:

| Terminal | Command | Purpose |
|----------|---------|---------|
| 1 | `ollama serve` | VLM Server |
| 2 | `cd python-backend && python app.py` | Flask Backend |
| 3 | `npm run dev` | Next.js Frontend |

Access the application at: **http://localhost:3000**

## ✨ Features

### Core Features
- 🔬 **Real-time Image Analysis** - Upload fundus images for instant analysis
- 🎯 **Multi-Condition Detection** - Detects 13 retinal abnormalities
- 📊 **Severity Classification** - 5-level DR severity grading
- 📝 **AI-Generated Reports** - Clinical reports with treatment recommendations
- 📈 **Interactive Visualizations** - Animated gauges, charts, and tables
- 💾 **Analysis History** - Persistent storage of past analyses
- 🔍 **Advanced Search & Filter** - Search conditions, filter by severity
- 📥 **Multiple Export Formats** - JSON, CSV, TXT downloads

### UI/UX Features
- Animated severity gauge with color coding
- Searchable and sortable predictions table
- Image preview with zoom and rotation
- Processing timeline with step-by-step progress
- Analytics dashboard with distribution charts
- Responsive design (mobile-friendly)
- Dark theme interface

## 📊 Model Performance

### Vision Model Metrics

| Condition | AUROC |
|-----------|-------|
| Overall | 83.5% |
| Diabetic Retinopathy | 98.7% |
| Microaneurysms | 87.3% |
| Hemorrhages | 89.1% |
| Hard Exudates | 85.6% |
| Soft Exudates | 82.4% |
| Neovascularization | 91.2% |

### Severity Classification

| Level | Precision | Recall | F1-Score |
|-------|-----------|--------|----------|
| No DR | 0.92 | 0.94 | 0.93 |
| Mild | 0.78 | 0.76 | 0.77 |
| Moderate | 0.81 | 0.79 | 0.80 |
| Severe | 0.85 | 0.83 | 0.84 |
| Proliferative | 0.89 | 0.91 | 0.90 |

## 🔌 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/health` | GET | Health check |
| `/api/analyze` | POST | Analyze fundus image |

## 💻 Usage Example
```typescript
import { apiClient } from '@/lib/api';

const result = await apiClient.analyzeImage(file, 'comprehensive');

console.log(result.severity);     // { level: 0, confidence: 0.99, name: "No DR" }
console.log(result.conditions);   // Array of 13 conditions
console.log(result.report);       // Clinical report text
```

## 📄 License

This project is licensed under the MIT License.

## 👤 Author

**Yassir**
- Al Akhawayn University - Big Data Analytics
- GPA: 3.6 | Dean's List

## 🙏 Acknowledgments

- ConvNeXt architecture: Facebook AI Research
- Llama 3.2-Vision: Meta AI
- UI Components: shadcn/ui

---

**⭐ If you find this project helpful, please give it a star!**
