# Code Quality Analysis

This project is made as a part of HackVita 2025 of JEC. We solved the **problem statement 9 (Code Quality Porblem)** Code Quality Analyser is an AI-powered tool designed to analyze you code quality. It can annalyse codefiles in your codebases and automatically generate comprehensive documentation for your projects, including security design, threat modeling, attack surface analysis, and more. The tool can be run locally using Docker or directly via Streamlit.

## Features
- AI-powered analysis that supports multi llm and works with OpenAI, OpenRouter, Anthropic, and Google models
- Docker-based execution for consistency and containerisation
- Streamlit UI for an interactive experience
- Generates security reports in Markdown format for better readeability.

---

## Installation & Setup

### 1️⃣ Clone the Repository
```sh
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
```

### 2️⃣ Set Up API Keys
Before running the tool, set up the required API keys:
*note that you can change this command based on the API key you are using*
```sh
export GOOGLE_API_KEY=your-google-api-key
export GEMINI_API_KEY=your-gemini-api-key
```
(For Windows PowerShell)
```powershell
$env:GOOGLE_API_KEY="your-google-api-key"
$env:GEMINI_API_KEY="your-gemini-api-key"
```

---

## Running Locally with Docker 🐳

### 1️⃣ Build the Docker Image
```sh
docker build -t code quality checker .
```

### 2️⃣ Run the Analysis
```sh
docker run -v $(pwd):/target \
       -e GOOGLE_API_KEY=${GOOGLE_API_KEY} \
       -e GEMINI_API_KEY=${GEMINI_API_KEY} \
       ai-security-analyzer \
       dir -v -t /target/uploads -o /target/security_design.md \
       --agent-provider google --agent-model gemini-2.0-flash-thinking-exp
```
This will generate `security_design.md` containing the security analysis.

---

## Running Locally with Streamlit 🚀

### 1️⃣ Install Dependencies
```sh
build your docker image
```

### 2️⃣ Run the Streamlit App
```sh
pip install streamlit
streamlit run app.py
```

### 3️⃣ Open in Browser
Once started, open the displayed **local URL** (e.g., `http://localhost:8501`) to interact with the security analyzer via the UI.

---

## Project Structure
```
📦 AI-Security-Analyzer
├── 📂 ai_code_quality          # Core analyzer logic
├── 📂 data                     # Example reports and datasets
├── 📂 scripts                  # Helper scripts
├── 📂 uploads                  # Uploaded files for analysis
├── Dockerfile                  # Docker setup
├── app.py                      # Streamlit UI
├── requirements.txt            # Python dependencies
├── security_design.md          # Generated security report
└── README.md                   # Project documentation
```

---

## Contributing 🤝
If you’d like to contribute:
1. Fork the repo
2. Create a feature branch (`git checkout -b feature-name`)
3. Commit changes (`git commit -m 'Added feature'`)
4. Push (`git push origin feature-name`)
5. Create a Pull Request

---

## License 📜
This project is licensed under the MIT License.

---

## Contact 📬
For questions or issues, feel free to reach out via GitHub Issues or email at `ayanbiswa.dutta2022@vitstudent.ac.in`, `akashdutta3113@gmail.com`.

