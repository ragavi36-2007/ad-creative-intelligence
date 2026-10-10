# PS-02: Ad Creative Intelligence

An AI-assisted web application prototype for exploring how advertising creative attributes relate to campaign performance. The project is designed to help marketers review ad creatives, compare performance metrics, identify promising creative patterns, and make evidence-based recommendations.

> **Project status:** Prototype / under development. The features available in a running version depend on the code currently implemented in `app.py` and the frontend files.

## Problem Statement

Advertising teams often create many ad variations but may not know which visual or content elements are associated with better results. Manually reviewing creatives and comparing campaign metrics takes time. This project aims to organize creative information and campaign data so that useful patterns can be identified more consistently.

## Objectives

- Accept advertising creative files through a simple web interface.
- Organize campaign performance data such as spend, impressions, clicks, and conversions.
- Extract or record creative attributes, such as dominant colours, text presence, layout, and visual style, as supported by the implementation.
- Compare creative attributes with performance metrics and rank findings by the strength of the available evidence.
- Report sample sizes and uncertainty where the analysis supports it, and label weak or underpowered findings as inconclusive.
- Explore future additions such as creative-brief generation, creative-fatigue alerts, and video-ad analysis.

## Key Features

- **Web interface:** A browser-based interface built with Flask, HTML, CSS, and JavaScript.
- **Creative-file handling:** Image processing libraries are included for working with image files. PDF and DOCX processing dependencies are also included for supporting-document workflows where implemented.
- **Campaign analysis foundation:** Pandas and NumPy support tabular data processing and calculations.
- **Deployable application:** Gunicorn is included as the production web server for deployment platforms such as Render.
- **Evidence-aware reporting goal:** Findings should include sample sizes and uncertainty where possible. Observational patterns must not be presented as proof that a creative feature caused better performance.

## Technology Stack

| Component | Technology |
|---|---|
| Backend | Python, Flask |
| Frontend | HTML, CSS, JavaScript |
| Data processing | Pandas, NumPy |
| Image processing | Pillow, OpenCV |
| Document processing | PyMuPDF, python-docx |
| Production server | Gunicorn |
| Hosting | Render (optional) |

## Project Structure

```text
ps02-ad-creative-intelligence/
├── static/
│   ├── uploads/       # Uploaded files (keep private; normally not committed)
│   ├── app.js         # Frontend JavaScript
│   └── style.css      # Styles
├── templates/
│   └── index.html     # Main web page
├── app.py             # Flask application
├── requirements.txt   # Python dependencies
├── .gitignore
└── README.md
```

Your local `.venv/` folder should not be uploaded to GitHub.

## Getting Started

### 1. Requirements

- Python installed on your computer
- Git (only needed to clone or push the repository)
- A web browser

### 2. Download the project

```bash
git clone https://github.com/ragavi36-2007/ps02-ad-creative-intelligence.git
cd ps02-ad-creative-intelligence
```

If you already have the project folder on your computer, open that folder in VS Code instead.

### 3. Create and activate a virtual environment

**Windows PowerShell:**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can use Command Prompt and run:

```bat
.venv\Scripts\activate.bat
```

### 4. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 5. Run the application locally

```bash
python app.py
```

Open the local address printed in the terminal (often `http://127.0.0.1:5000`). If your `app.py` does not start the development server directly, use the run instructions configured in that file.

## Suggested Campaign Dataset

For analysis of a collection of ads, a structured table can use one row per creative or creative variant. A recommended CSV schema is:

| Column | Meaning |
|---|---|
| `creative_id` | Unique identifier for the ad creative |
| `image_filename` | Name of the matching image file |
| `spend` | Amount spent on the ad |
| `impressions` | Number of times the ad was shown |
| `clicks` | Number of clicks |
| `conversions` | Number of recorded conversions |

Example (illustrative data only):

```csv
creative_id,image_filename,spend,impressions,clicks,conversions
AD001,ad001.jpg,120.00,15000,450,18
AD002,ad002.png,95.00,12000,240,9
```

Make sure the currency and attribution window are consistent across rows. Avoid including personal, confidential, or customer-identifying information. CSV ingestion is available only if it has been implemented in the current application code.

## Common Performance Metrics

- **Click-through rate (CTR):** `clicks / impressions × 100`
- **Conversion rate (click-based):** `conversions / clicks × 100`
- **Cost per conversion (CPA):** `spend / conversions`

When the denominator is zero, report the metric as unavailable rather than dividing by zero. Confirm that campaigns use comparable goals, budgets, audiences, placements, and reporting windows before comparing them.

## Interpreting Findings Responsibly

- A pattern in a small dataset may be unstable; show the number of creatives behind each finding.
- Use confidence intervals or other uncertainty estimates where suitable, and mark insufficient evidence as **inconclusive**.
- An association does not demonstrate causation. Audience, placement, offer, budget, and campaign timing can also affect outcomes.
- Treat results as decision support, not a guarantee of future campaign performance.

## Deploying on Render

1. Push the project to the GitHub repository.
2. In Render, create a **Web Service** and connect the repository.
3. Set the build command to:

   ```bash
   pip install -r requirements.txt
   ```

4. Set the start command to:

   ```bash
   gunicorn app:app
   ```

5. Deploy, then open the service URL provided by Render and test the application.

The `app:app` command assumes that `app.py` contains a Flask application object named `app`.

## Future Enhancements

- Automated creative-attribute extraction using computer vision and OCR
- Statistical comparisons with effect sizes, sample sizes, and confidence intervals
- Creative-brief suggestions based on supported findings
- Creative-fatigue detection across time periods
- Support for video ads and frame-level analysis
- Exportable reports for campaign teams

## License

No license has been added yet. Add a `LICENSE` file before permitting reuse or redistribution under specific terms.

 FINAL PRODUCT -  https://ps02-ad-creative-intelligence.onrender.com
