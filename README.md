
# 🔍 Trend Analysis Using AI Agent

A scalable Python project for discovering and tracking trending topics in large volumes of customer reviews — powered by **state-of-the-art transformer-based sentence embeddings**.

---

## ⭐️ Features

✅ **Semantic Topic Grouping**  
Groups reviews by actual meaning (not just keywords), using transformer-based embeddings (`all-mpnet-base-v2` supported by default).

✅ **Automatic Topic Discovery**  
Identifies new, never-before-seen customer themes dynamically. Topics are auto-labeled with readable snippets extracted from review text.

✅ **Topic Capping & Merging**  
Prevents over-splitting by enforcing a configurable topic cap. Automatically merges the most similar new topics when the limit is reached.

✅ **Rolling Trend Tracking**  
Maintains per-topic daily review counts in a rolling time window (default: 31 days), ideal for spotting spikes and long-term trends.

✅ **Business-Ready Trend Reports**  
Generates clean, filterable pandas DataFrames — ready for dashboards or reporting pipelines.

---

## 🧠 How It Works

### 🔧 Initialization
- Loads a `SentenceTransformer` model (default: `all-mpnet-base-v2`).
- Seeds with known topics and computes initial centroid embeddings.

### 📝 Review Processing
- Each review is embedded and compared to existing topics using **cosine similarity**.
- If similarity exceeds threshold, the review is assigned to a topic.
- If not, a **new topic** is created using a snippet from the review.
- When topic count exceeds `max_topics`, the two most similar topics are automatically **merged**.
- All topic frequencies are stored in a **rolling time window** for trend tracking.

### 📈 Reporting
- Generates a trend table (`pandas.DataFrame`) with:
  - Rows → Topics  
  - Columns → Daily counts over the last `N` days  
- Ready for visualization, alerting, or analysis.

---

## 📊 Workflow Diagram



## ⚙️ Configuration Options

| Parameter             | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `max_topics`          | Maximum number of topics to retain; closest topics are merged if exceeded. |
| `similarity_threshold`| Cosine similarity threshold to assign reviews to existing topics.           |
| `window_days`         | Rolling time window (in days) for trend reports. Default is `31`.          |
| `model`               | SentenceTransformer model (default: `all-mpnet-base-v2`).                   |

---

## 📦 Installation


## 🚀 Example Usage

```python
from your_module import TopicLimiterReviewTrendAgent

# Define seed topics
seed_topics = {
    "Delivery issue": ["Order late", "Delivery delayed", "Order cancelled"],
    "Payment issue": ["Payment failed", "Couldn't pay"],
    # ...
}

# Example daily batches (replace with your real data):
 daily_data = {
     '2024-06-01': [
         "Delivery guy was rude and late",
         "Food was stale",
         "Maps not working properly",
         "Instamart should be open all night",
         "Payment failed multiple times",
         "Customer support was unresponsive",
         "Please bring back 10 minute delivery",
         "Order was delayed",
         "Maps not loading properly",
         "I love the app"
    ],
}

agent = TopicLimiterReviewTrendAgent(seed_topics)

# Process review data
for date, reviews in daily_data.items():
    agent.process_daily_batch(pd.to_datetime(date).date(), reviews)

# Generate trend report
trend_df = agent.get_trend_report(end_date)
```

---

## 📁 Output Example

| Topic                 | 2023-06-24 | 2023-06-25 | ... | 2023-07-24 |
|----------------------|------------|------------|-----|------------|
| Delivery issue        | 2          | 0          | ... | 1          |
| new_topic 4: GPS not  | 0          | 1          | ... | 3          |

---

## 🧱 Built With
- [SentenceTransformers](https://www.sbert.net/)
- [scikit-learn](https://scikit-learn.org/)
- [pandas](https://pandas.pydata.org/)
- [numpy](https://numpy.org/)
- [tqdm](https://tqdm.github.io/)

---

## 🧪 Future Ideas
- Sentiment-aware topic tracking
- Multi-language review support
- Anomaly/spike alerts

---

## 📄 License

MIT License
