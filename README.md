# image-explain-api

**Upload any image → GPT-4o-mini provides intelligent AI-powered explanation!**

---

## ✨ Features

- 🖼️ **Image Upload** - Drag & drop or select images
- 🤖 **AI Vision Analysis** - GPT-4o-mini model for detailed explanations
- ⚡ **Fast Processing** - Real-time response using OpenRouter API
- 🎨 **Clean UI** - Simple and intuitive web interface
- 🔒 **Secure** - API key stored securely in environment variables

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Backend** | FastAPI + Uvicorn |
| **AI Model** | OpenAI GPT-4o-mini (via OpenRouter) |
| **Templates** | Jinja2 HTML |
| **Deployment** | Render.com |
| **Language** | Python 3.9+ |

---

## 📋 Prerequisites

```bash
Python 3.9+
pip package manager
OpenRouter API key (free at openrouter.ai)
Local Setup
1️⃣ Clone Repository
bash
git clone https://github.com/bandhana498-source/image-explain-api.git
cd image-explain-api
2️⃣ Install Dependencies
bash
pip install -r requirements.txt
3️⃣ Setup Environment Variables
Create .env file:
Ctext
OPENROUTER_API_KEY=sk-or-v1-your_key_here
Get your free API key: OpenRouter.ai

4️⃣ Run Application
bash
python -m uvicorn main:app --reload
Open: http://127.0.0.1:8000
://127.0.0.1:8000

📡 API Endpoints
GET /
Returns HTML upload form

Response: HTML page with image upload form

POST /explain
Analyzes uploaded image using GPT-4o-mini

Request:

text
Content-Type: multipart/form-data
file: <image_file>
Response:

json
{
  "explanation": "The image shows a detailed AI-powered analysis..."
}
📁 Project Structure
image-explain-api/
├── main.py          # FastAPI app
├── requirements.txt # Dependencies
├── templates/       # HTML templates
│   └── index.html
└── README.md

 file
🔧 requirements.txt
text
fastapi==0.115.0
uvicorn[standard]==0.30.6
python-dotenv==1.0.1
openai==1.51.0
jinja2==3.1.4
python-multipart==0.0.9
💻 Code Example
python
from fastapi import FastAPI, UploadFile, File
from openai import OpenAI

app = FastAPI()
client = OpenAI(
    api_key=os.getenv("OPENROUTER_API_KEY"),
    base_url="https://openrouter.ai/api/v1"
)

@app.post("/explain")
async def explain_image(file: UploadFile = File(...)):
    image_data = await file.read()
    base64_image = base64.b64encode(image_data).decode('utf-8')
    
    response = client.chat.completions.create(
        model="openai/gpt-4o-mini",
        messages=[{
            "role": "user",
            "content": [{
                "type": "text",
                "text": "Identify and explain this image in detail"
            }, {
                "type": "image_url",
                "image_url": {"url": f"data:image/jpeg;base64,{base64_image}"}
            }]
        }]
    )
    return {"explanation": response.choices.message.content}Usage Example
Open http://localhost:8000

Click "Choose File" and select an image

Click "Explain Image"

AI-powered explanation appears instantly!

🔐 Security Notes
✅ .env file NOT committed to GitHub

✅ Use environment variables for sensitive data

✅ API key stored securely on Render dashboard

✅ CORS enabled for productionTroubleshooting
Issue	Solution
ModuleNotFoundError	Run pip install -r requirements.txt
API key error	Check .env file and OPENROUTER_API_KEY
Port 8000 in use	Change port: uvicorn main:app --port 8001
CORS error	Ensure CORS middleware is enabled in main.py
 Resources
FastAPI Docs

OpenRouter API

Render Deployment

OpenAI Vision

