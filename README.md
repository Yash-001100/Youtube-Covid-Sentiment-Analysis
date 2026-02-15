# YouTube COVID-19 News Sentiment Analysis

A Python project that analyzes sentiment in COVID-19–related news videos on YouTube and compares it with viewer comments. Data is collected from Fox News, BBC News, CNN, and Sky News (January 2020 – January 2023).

## Overview

- **Goal:** Compare how news channels framed the pandemic (via video titles) vs. how the public responded (via comments)
- **Output:** Structured datasets (`videos.csv`, `comments.csv`) and sentiment distribution charts
- **Main finding:** Video titles tend to be neutral; comments show stronger positive/negative sentiment

## Project Structure

```
s223079934-HD1/
├── README.md
├── requirements.txt
├── credentials.ini.example
├── .gitignore
└── 1057077/
    └── 001-code.ipynb
```

## Prerequisites

- **Python 3.7+**
- **YouTube Data API key** — get one from [Google Cloud Console](https://console.cloud.google.com/) (enable YouTube Data API v3)

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure YouTube API credentials

1. Copy the example file into the notebook folder:

   ```bash
   copy credentials.ini.example 1057077\credentials.ini   # Windows
   cp credentials.ini.example 1057077/credentials.ini    # macOS/Linux
   ```

2. Edit `1057077/credentials.ini` and add your API key:

   ```ini
   [credentials_youtube]
   developer_key = YOUR_YOUTUBE_API_KEY
   youtube_api_service_name = youtube
   youtube_api_version = v3
   ```

   Replace `YOUR_YOUTUBE_API_KEY` with your key from Google Cloud Console.

## How to Run

1. Open the notebook:

   ```bash
   cd 1057077
   jupyter notebook 001-code.ipynb
   ```

   Or open `1057077/001-code.ipynb` in VS Code or JupyterLab.

2. Run cells **top to bottom** (or use *Run All*).

3. Execution order:
   - **Cell 1:** Install/import libraries (NLTK stopwords will download on first run)
   - **Cell 2:** Set constants (date range, channels, keywords)
   - **Cells 3–7:** Define functions (credentials, data collection, preprocessing)
   - **Cells 8–9:** Call `load_credentials()` and build the YouTube API client
   - **Cell 10:** Fetch videos for all channels
   - **Cell 11:** Fetch comments for each video
   - **Cells 12–13:** Clean and preprocess data
   - **Remaining cells:** Merge data, compute sentiment, generate visualizations

4. Outputs are written to the same folder as the notebook:
   - `videos.csv` — video metadata
   - `comments.csv` — comment text and metadata
   - Charts are shown inline in the notebook

## Dependencies

- pandas  
- seaborn  
- matplotlib  
- google-api-python-client  
- nltk  
- langdetect  
- textblob  
- prettytable  
- tabulate  
- numpy  

See `requirements.txt` for versions.

## Configuration

You can adjust these in the second notebook cell:

| Variable       | Description                          | Default                         |
|----------------|--------------------------------------|---------------------------------|
| `START_DATE`   | Start of date range                  | Jan 1, 2020                     |
| `END_DATE`     | End of date range                    | Jan 1, 2023                     |
| `KEYWORDS`     | Search terms in video titles         | coronavirus, covid, covid-19, pandemic |
| `CHANNELS`     | YouTube channel IDs and names        | Fox News, BBC, CNN, Sky News    |
| `MAX_VIDEOS`   | Max videos per channel per request   | 50                              |

## Notes

- **API quotas:** The YouTube Data API has daily quotas; running the full pipeline may consume a noticeable amount.
- **Disabled comments:** Some videos have comments disabled; those are skipped (403 errors).
- **English only:** Comments are filtered to English using `langdetect`.
- **Credentials:** Never commit `credentials.ini` or share your API key. Use `credentials.ini.example` as a template.

## Pushing to GitHub

1. Create a new repository on [GitHub](https://github.com/new) (do not initialize with a README if one already exists).
2. Run from the project root:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: YouTube COVID-19 sentiment analysis"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
   git push -u origin main
   ```

3. Replace `YOUR_USERNAME` and `YOUR_REPO_NAME` with your GitHub username and repository name.

## License

MIT (or specify your license)
