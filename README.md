# 🛒 Amazon Image Auditor

A Streamlit web app that audits Amazon product images, fixes common issues, 
and outputs a formatted Excel report — all in one click.

---

## ✅ What It Does

- Accepts a `.xlsx` file with **Product Title** and **Image URL** columns
- Resolves product page URLs to direct image links (Takealot API + HTML scraping)
- Audits each image against Amazon standards:
  - Minimum 1000px on longest side
  - Pure white background (optional auto-removal)
  - JPEG format, 72 DPI
- Outputs a **single Excel workbook** with 4 sheets:
  - Audit Report (all products)
  - Summary
  - Failed Items
  - Needs Attention

---

## 🚀 Option 1 — Run Locally (Recommended for full features)

### Requirements
- Python 3.9 or higher
- pip

### Steps

```bash
# 1. Clone or download the project folder
cd amazon-image-auditor

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the app
streamlit run app.py
```

The app opens automatically at `http://localhost:8501`

> **Note on background removal:** `rembg` installs a neural network model (~170MB) on first run.
> If you do not need background removal, you can skip it by toggling it off in the UI.
> You can also remove `rembg` and `onnxruntime` from `requirements.txt` to speed up install.

---

## 🌐 Option 2 — Deploy Online (Free Shareable Link)

Use **Streamlit Community Cloud** to host the app and get a public URL.

### Steps

1. Push this folder to a **GitHub repository** (can be private)
2. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub
3. Click **New app** → select your repo and `app.py`
4. Click **Deploy**

Streamlit installs `requirements.txt` automatically.  
Your app will be live at: `https://your-app-name.streamlit.app`

> **Cloud limitation:** Selenium-based URL resolution is not available in the cloud version.
> The app uses the faster requests-based approach instead, which works for Takealot and 
> most standard product pages. For JavaScript-heavy pages, run locally.

---

## 📂 File Structure

```
amazon-image-auditor/
├── app.py              ← Main Streamlit app
├── requirements.txt    ← Python dependencies
└── README.md           ← This file
```

---

## 📋 Input File Format

Your Excel file must have **exactly** these column names:

| Product Title     | Image URL                             |
|-------------------|---------------------------------------|
| Widget Pro 2000   | https://www.takealot.com/widget/PLID123 |
| Blue Sneakers XL  | https://images.example.com/shoe.jpg   |

A sample template is available inside the app on the upload screen.

---

## ⚙️ Settings

| Setting          | Description                                          |
|------------------|------------------------------------------------------|
| Workers (1–10)   | Parallel threads for image processing. Default: 4.   |
| Remove BG        | Toggle background removal via rembg. Off by default. |

---

## 📊 Output Columns

| Column         | Description                                      |
|----------------|--------------------------------------------------|
| Product Title  | From your input file                             |
| Image URL      | Original URL from your file                      |
| Status         | COMPLIANT / ATTENTION / FAILED                   |
| Audit Notes    | Every fix applied or error encountered           |
| Resolved URL   | Final direct image URL that was downloaded       |

---

Built for Amazon Marketplace Sellers · Handles Takealot, Amazon, and generic product pages.
