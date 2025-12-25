# GLR-Pipeline-Automation
**Automated General Loss Report (GLR) Generation with Streamlit and Groq LLM.**

This application streamlines the insurance reporting process by automatically extracting data from field PDF reports and populating a Word (.docx) template. It leverages the speed of Groq and the reasoning capabilities of Llama 3.3 to identify key-value pairs (Insured Name, Dates, Damages, Narratives) and generate a polished final report.

## 🚀 Features

* **PDF Text Extraction:** Uses `PyMuPDF` (fitz) to scrape text from multiple photo reports and forms.
* **Intelligent Data Extraction:** Utilizes **Groq API (Llama-3.3-70b)** to interpret messy report data into structured JSON.
* **Template Automation:** Dynamically fills a user-provided `.docx` template with the extracted data.
* **Dual Output:** Generates a filled `.docx` file and optionally converts it to `.pdf` (Windows only).
* **Secure:** API keys are input per session and never stored.

## 🛠️ Requirements

* **Python 3.8+**
* **Groq API Key:** Get a free key at [console.groq.com](https://console.groq.com/).
* **Microsoft Word (Optional):** Required only if you want automatic PDF conversion on Windows.

## 📦 Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/glr-automation.git](https://github.com/yourusername/glr-automation.git)
    cd glr-automation
    ```

2.  **Install dependencies:**
    ```bash
    pip install streamlit groq python-docx pymupdf docx2pdf
    ```

    *Note: `docx2pdf` requires Microsoft Word to be installed on the host machine to function.*

## ▶️ Usage

1.  **Run the Streamlit app:**
    ```bash
    streamlit run app.py
    ```
2.  **Open your browser** to the local URL provided (usually `http://localhost:8501`).
3.  **Enter your Groq API Key** in the sidebar.
4.  **Upload files:**
    * **Template:** An empty General Loss Report in `.docx` format.
    * **Source Evidence:** One or more PDF reports (forms, photo sheets).
5.  **Click "Generate Final Report"**.
6.  **Download** the completed `.docx` (or `.pdf`).

## 🧩 How It Works

1.  **Ingestion:** The app reads raw text from all uploaded PDF files.
2.  **Structuration:** The LLM analyzes the text to find specific insurance fields (e.g., `INSURED_NAME`, `LOSS_DATE`, `DWELLING_NARRATIVE`) based on strict extraction rules.
3.  **Generation:** The LLM takes the empty template and the structured data to rewrite the template, filling in placeholders and generating narrative sections.
4.  **Assembly:** The result is compiled back into a clean Word document.

## 📝 Configuration

* **Model:** Defaults to `llama-3.3-70b-versatile` for a balance of speed and accuracy.
* **Extraction Fields:** defined in the `EXTRACTION_FIELDS` list within the script.

## ⚠️ Limitations

* **PDF Images:** Currently relies on text extraction. Scanned PDFs (images without text layers) may need OCR integration (e.g., Tesseract) if `PyMuPDF` cannot read them.
* **PDF Conversion:** The `.docx` to `.pdf` conversion feature relies on `pythoncom` and is strictly Windows-only. The app will gracefully disable this feature on Linux/Mac.
