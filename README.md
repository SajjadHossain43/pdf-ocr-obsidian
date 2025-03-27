# PDF OCR Pipeline to Markdown using Mistral AI

This repository contains a **Jupyter Notebook (`.ipynb`)** that automates the OCR (Optical Character Recognition) process for PDFs using the **Mistral AI** OCR API. It extracts text and images from PDFs and organizes the output into structured markdown documents with images properly linked using Obsidian-style **wikilinks**.

> Beta testing! -> Check [Web App](#web-app) section for the first working preview, where you can upload your PDFs and get the markdown files, and even preview them before downloading anything.

## Features
- **Batch processing:** Place multiple PDFs in the input folder and process them automatically.
- **Text extraction:** Converts scanned PDFs into structured markdown format while preserving document hierarchy.
- **Image extraction:** Saves images separately and links them in the markdown using Obsidian-compatible `![[image-name]]` format.
- **Automatic organization:** Each processed PDF gets its own output folder, and completed PDFs are moved to a `pdfs-done` folder.
- **OCR caching:** Saves the OCR response as JSON to avoid redundant API calls.
- **Notebook-based workflow:** Run step-by-step OCR processing in a Jupyter Notebook.

## Installation
Ensure you have Python 3.9+ and Jupyter installed, then install dependencies:

```sh
pip install mistralai jupyter python-dotenv
```

## Usage
### 1. Set Up API Key

Before running the notebook, you need to set up a free Mistral API key. Go to [Mistral's API Key Console](https://console.mistral.ai/api-keys) and generate your key—it doesn’t cost anything.

An `env.example` file is included in the repository. Edit it to add your API key and rename it to `.env` so the script can use it properly.

Alternatively, you can set it manually as an environment variable:

```sh
export MISTRAL_API_KEY='your_api_key_here'  # For Linux/macOS
set MISTRAL_API_KEY='your_api_key_here'    # For Windows
```

### 2. Open the Notebook
Run the following command to open the Jupyter Notebook:

```sh
jupyter notebook pdf-markdown-ocr.ipynb
```

Or open the [PDF Markdown OCR Notebook](pdf-markdown-ocr.ipynb) file directly in your IDE.

### 3. Place PDFs in pdfs_to_process

Before running the notebook for the first time, you need to manually create the pdfs_to_process folder inside the project directory. Once created, place the PDFs you want to OCR inside this folder.

### 4. Run the Notebook

Execute the cells sequentially to process the PDFs. Make sure each step works correctly.

### 5. Output Structure
Each processed PDF gets its own folder inside `ocr_output`, structured like this:

```
ocr_output/
  ├── MyDocument/
  │   ├── output.md            # Extracted markdown with wikilinks
  │   ├── ocr_response.json    # Raw OCR response (for reuse)
  │   ├── images/
  │   │   ├── MyDocument_img_1.jpeg
  │   │   ├── MyDocument_img_2.jpeg
pdfs-done/
  ├── MyDocument.pdf  # Moved here after OCR completion
```

### 6. Move Output to Obsidian Vault
After conversion, move the generated `output.md` file into your **Obsidian vault**. Additionally, make sure to move the extracted images to your **Obsidian attachment folder**.

**Important:** Ensure that your Obsidian vault is set up to handle **wikilink paths** (`![[image-name]]`). If your vault does not support this structure, the script may not work as expected. Contributions to enhance compatibility are welcome!

## How It Works
1. The notebook scans `pdfs_to_process` for PDFs.
2. Each PDF is uploaded to Mistral AI for OCR processing.
3. The text is extracted and saved as markdown (`output.md`).
4. Images are extracted, saved in a subfolder, and referenced in the markdown using `![[image-name]]`.
5. The original PDF is moved to `pdfs-done` to avoid duplicate processing.
6. The full OCR response is saved as JSON for later use.

## Notes
- The extracted markdown is optimized for use with **Obsidian**, a knowledge management tool that supports wikilinks.
- If a PDF has already been processed, you can reload its OCR data from the saved JSON file instead of making a new API request.
- Contributions to improve compatibility with different Obsidian setups are welcome!

## Web App

- `pip install -r requirements.txt`
- `python app.py`
- Open your browser and go to `http://localhost:5000/`


## Contributing
Feel free to submit issues or pull requests if you have improvements or additional features in mind.

## License
This project is licensed under the MIT License.

