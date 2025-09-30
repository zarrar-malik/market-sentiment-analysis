# 📈 Market Sentiment Analysis Dashboard

A comprehensive Python-based tool for collecting financial news, analyzing market sentiment using AI, and creating interactive visualizations to track market sentiment trends across different stocks and time periods.

## 🎯 Project Overview

This project combines web scraping, natural language processing, and data visualization to provide insights into market sentiment from financial news sources. It collects news articles, analyzes their sentiment using advanced NLP models, and presents the results through an interactive dashboard.

### Key Features

- **📰 News Collection**: Automated scraping of financial news from multiple sources
- **🧠 AI-Powered Sentiment Analysis**: Uses pre-trained transformer models for accurate sentiment classification  
- **📊 Interactive Visualizations**: Comprehensive dashboard with multiple chart types
- **💾 Database Storage**: SQLite database for persistent data storage
- **🎨 Beautiful Charts**: Professional-quality visualizations using matplotlib and plotly
- **📈 Stock Tracking**: Monitor sentiment for specific stock symbols
- **⏱️ Time Series Analysis**: Track sentiment changes over time

## 🛠️ Technical Stack

- **Python 3.8+**
- **Web Scraping**: BeautifulSoup, requests
- **NLP/AI**: transformers, torch, textblob
- **Data Analysis**: pandas, numpy
- **Database**: SQLite3
- **Visualization**: matplotlib, plotly, seaborn
- **Development**: Jupyter Notebook

## 📋 Prerequisites

Before running this project, ensure you have:

- Python 3.8 or higher installed
- Jupyter Notebook or JupyterLab
- Stable internet connection for news scraping
- At least 2GB free disk space for models and data

## 🚀 Installation

1. **Clone or Download the Project**
   ```bash
   # If using git
   git clone <repository-url>
   cd market-sentiment-analysis
   
   # Or download and extract the ZIP file
   ```

2. **Install Required Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

   **requirements.txt:**
   ```txt
   pandas>=1.3.0
   numpy>=1.21.0
   matplotlib>=3.4.0
   plotly>=5.0.0
   seaborn>=0.11.0
   beautifulsoup4>=4.10.0
   requests>=2.25.0
   transformers>=4.15.0
   torch>=1.10.0
   textblob>=0.17.0
   jupyter>=1.0.0
   sqlite3
   ```

3. **Install Alternative (if requirements.txt not available)**
   ```bash
   pip install pandas numpy matplotlib plotly seaborn beautifulsoup4 requests transformers torch textblob jupyter
   ```

## 📖 Usage Guide

### Quick Start

1. **Open Jupyter Notebook**
   ```bash
   jupyter notebook
   ```

2. **Run the cells in order**:
   - **Cell 1**: Import libraries and setup
   - **Cell 2**: Initialize database and create tables
   - **Cell 3**: Collect news data (this may take 5-10 minutes)
   - **Cell 4**: Analyze sentiment using AI models
   - **Cell 5**: Create comprehensive visualizations

### Detailed Workflow

#### Step 1: Database Setup
```python
# Creates SQLite database with tables for:
# - articles: Store news articles and metadata
# - sentiment_scores: Store AI-generated sentiment analysis
# - stock_prices: Store stock price data (optional)
```

#### Step 2: News Collection
```python
# Scrapes news from multiple sources:
# - Yahoo Finance
# - MarketWatch  
# - Reuters Business
# - Collects ~50-100 recent articles
```

#### Step 3: Sentiment Analysis
```python
# Uses transformer models for sentiment analysis:
# - Primary: cardiffnlp/twitter-roberta-base-sentiment-latest
# - Fallback: textblob for basic sentiment
# - Generates sentiment scores (-1 to +1) and labels
```

#### Step 4: Visualization Dashboard
```python
# Creates 4 comprehensive charts:
# 1. Sentiment Distribution (Pie Chart)
# 2. Average Sentiment by Stock (Bar Chart)  
# 3. Sentiment Score Distribution (Histogram)
# 4. Sentiment Trends Over Time (Line Chart)
```

## 📊 Output Examples

### Dashboard Components

1. **Sentiment Distribution**
   - Pie chart showing positive/negative/neutral article percentages
   - Color-coded: Green (positive), Red (negative), Blue (neutral)

2. **Stock Sentiment Analysis**
   - Bar chart comparing average sentiment across different stocks
   - Helps identify which stocks have most positive/negative coverage

3. **Score Distribution**
   - Histogram showing the range and frequency of sentiment scores
   - Identifies overall market mood and sentiment intensity

4. **Time Series Trends**
   - Line chart tracking sentiment changes over time
   - Dual-axis showing both sentiment scores and article volume

### Sample Output
```
📊 Found 87 articles in database. Creating visualizations...
📈 Summary Statistics:
   • Total Articles: 87
   • Unique Stocks: 12
   • Average Sentiment: 0.142
   • Sentiment Range: -0.891 to 0.934
✅ All visualizations created successfully!
```

## 🔧 Configuration Options

### Customizing Data Sources

Edit the news sources in Cell 3:
```python
sources = [
    "https://finance.yahoo.com/news/",
    "https://www.marketwatch.com/latest-news",
    "https://www.reuters.com/business/",
    # Add your preferred financial news sources
]
```

### Adjusting Sentiment Models

Modify the sentiment analysis model in Cell 4:
```python
# Change the model for different analysis approaches
model_name = "cardiffnlp/twitter-roberta-base-sentiment-latest"
# Alternative models:
# "nlptown/bert-base-multilingual-uncased-sentiment"
# "ProsusAI/finbert"
```

### Visualization Customization

Modify chart styles in Cell 5:
```python
# Change color schemes
colors = ['#ff6b6b', '#4ecdc4', '#45b7d1']  # Red, Teal, Blue
# Or use different matplotlib styles
plt.style.use('seaborn-v0_8')  # Options: default, seaborn, ggplot
```

## 📁 Project Structure

```
market-sentiment-analysis/
│
├── market_sentiment_analysis.ipynb    # Main Jupyter notebook
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── market_sentiment.db               # SQLite database (created when run)
│
├── data/                             # Data storage (optional)
│   ├── raw_articles/
│   └── processed_sentiment/
│
└── docs/                             # Documentation (optional)
    ├── technical_details.md
    └── troubleshooting.md
```

## 🐛 Troubleshooting

### Common Issues and Solutions

#### 1. Database Connection Error
```
ProgrammingError: Cannot operate on a closed database.
```
**Solution**: Run all cells in order, or restart kernel and run from Cell 1.

#### 2. Web Scraping Blocked
```
ConnectionError: Max retries exceeded
```
**Solution**: 
- Check internet connection
- Some sites may block automated requests - this is normal
- The code includes fallback mechanisms

#### 3. Model Download Issues
```
OSError: Can't load tokenizer for 'cardiffnlp/twitter-roberta-base-sentiment-latest'
```
**Solution**:
- Ensure stable internet connection
- Model will download automatically (~500MB) on first run
- Clear cache and retry: `transformers-cli cache clear`

#### 4. Memory Issues
```
RuntimeError: CUDA out of memory / RAM usage too high
```
**Solution**:
- Close other applications
- Restart kernel between runs
- Code automatically falls back to CPU if GPU unavailable

#### 5. No Visualizations Appearing
**Solution**:
```python
# Add this at the top of Cell 5
%matplotlib inline
import matplotlib.pyplot as plt
plt.ion()  # Turn on interactive mode
```

### Debug Commands

```python
# Check database status
def check_database_status():
    conn = sqlite3.connect('market_sentiment.db')
    # Check tables and record counts
    
# Clear all data and restart
def reset_database():
    import os
    if os.path.exists('market_sentiment.db'):
        os.remove('market_sentiment.db')
    print("Database reset. Run Cell 2 to recreate.")
```

## 📈 Performance Notes

### Expected Runtime
- **Cell 1** (Setup): ~30 seconds (first run for model download)
- **Cell 2** (Database): ~5 seconds
- **Cell 3** (Data Collection): ~5-10 minutes (depends on sources)
- **Cell 4** (Sentiment Analysis): ~2-5 minutes (depends on article count)
- **Cell 5** (Visualizations): ~10 seconds

### Resource Usage
- **Memory**: 2-4GB RAM during model inference
- **Storage**: ~1GB for models, ~50MB for data
- **Network**: ~500MB for initial model download, ~10MB for news scraping

## 🔮 Future Enhancements

### Planned Features
- [ ] Real-time sentiment monitoring
- [ ] Integration with stock price APIs
- [ ] Advanced sentiment metrics (fear/greed index)
- [ ] Email alerts for significant sentiment changes
- [ ] Web dashboard using Streamlit/Dash
- [ ] Support for multiple languages
- [ ] Integration with social media sentiment (Twitter/Reddit)
- [ ] Machine learning model for price prediction

### Contributing
This project is designed for educational and research purposes. Feel free to:
- Add new data sources
- Implement additional sentiment models
- Create new visualization types
- Optimize performance
- Add new features

## 📄 License

This project is for educational and research purposes. Please ensure compliance with:
- Website terms of service when scraping
- API rate limits and usage policies
- Data privacy regulations
- Model licensing terms

## 🙋‍♂️ Support

**Created for**: S&P Global PM - DATA FEED Department  
**Developed by**: Zarrar Malik (zarrar.malik@spglobal.com)  
**Date**: September 2025

### Getting Help

1. **Check the troubleshooting section above**
2. **Review error messages carefully** - they often contain helpful information
3. **Ensure all cells are run in order**
4. **Restart kernel if experiencing persistent issues**
5. **Verify internet connection for data collection steps**

### Additional Resources

- [Transformers Documentation](https://huggingface.co/transformers/)
- [Plotly Python Documentation](https://plotly.com/python/)
- [BeautifulSoup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)

---

**🎉 Ready to analyze market sentiment? Start with Cell 1 and follow the step-by-step workflow!**
