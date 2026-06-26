# Setup Instructions - Offline Customer Support Chatbot

This guide explains how to set up the local environment and run the offline customer support chatbot.

---

## Prerequisites
- **Python 3.8+**
- **Ollama** installed on your operating system

---

## Step 1: Install Ollama
1. Download the Ollama installer for your operating system:
   - **Windows**: [Ollama Windows Installer](https://ollama.com/download/windows)
   - **macOS**: [Ollama macOS Download](https://ollama.com/download/mac)
   - **Linux**: Run `curl -fsSL https://ollama.com/install.sh | sh`
2. Run the installer and follow the prompt instructions.

*Note: For Windows, you can perform a silent installation using PowerShell:*
```powershell
Start-Process "OllamaSetup.exe" -ArgumentList "/VERYSILENT", "/SUPPRESSMSGBOXES", "/NORESTART" -Wait
```

---

## Step 2: Start Ollama and Pull Llama 3.2
1. Make sure the Ollama application is running (an Ollama icon will appear in the system tray on Windows/macOS).
2. Open your terminal and download the **Llama 3.2 3B** model by running:
   ```bash
   ollama pull llama3.2:3b
   ```
3. (Optional) You can test the model interactively in your terminal:
   ```bash
   ollama run llama3.2:3b
   ```
   Type `/bye` to exit the interactive mode.

---

## Step 3: Setup Project and Python Environment
1. Navigate to the project root directory:
   ```bash
   cd Offline-Customer-Support-Chatbot-with-Ollama-and-Llama-3.2
   ```
2. Create a Python virtual environment:
   ```bash
   python -m venv venv
   ```
3. Activate the virtual environment:
   - **Windows (PowerShell)**:
     ```powershell
     .\venv\Scripts\Activate.ps1
     ```
   - **macOS/Linux**:
     ```bash
     source venv/bin/activate
     ```
4. Install the required Python libraries:
   ```bash
   pip install requests
   ```

---

## Step 4: Run the Chatbot Client
1. Execute the main Python script to run all 20 queries through the model using both Zero-Shot and One-Shot prompts:
   ```bash
   python chatbot.py
   ```
2. The responses will be written to `eval/results.md`.
3. Open `eval/results.md` and manually grade the results using the scoring rubric provided inside.
