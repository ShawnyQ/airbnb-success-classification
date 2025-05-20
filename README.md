# 🏡 Predicting Airbnb Listing Success in Dubai

This project builds a full end-to-end machine learning pipeline to predict the **success tier of an Airbnb listing** — categorized as **Excellent**, **Good**, or **Average** — using only publicly available metadata.

> 🔎 **Goal**: Help real estate agents, analysts, and hosts evaluate listing potential before deployment, based on observable features like price, reviews, availability, and host trust signals.

---

## 🎯 Project Summary

- **Type**: Multi-class classification
- **Target**: `success_label` (Excellent / Good / Average)
- **Model**: Tuned Random Forest
- **Evaluation**: Accuracy, F1 Score, Confusion Matrix, Feature Importance

---

## 🧠 What Defines Success?

Since Airbnb doesn’t provide a built-in success score, we engineered a label using:
- ✅ `adj_rating`: Adjusted guest rating (normalized scale)
- ✅ `log_reviews_ltm`: Log-transformed review count (last 12 months)
- ✅ `has_rating`: Has the listing ever been rated?
- ✅ `instant_bookable`: Can it be booked without host approval?
- ✅ `is_superhost`: Airbnb’s trust-based badge

These features were combined into a **composite success score**, and **quantile binned** into 3 classes to ensure balance.

---

## 🧩 Features Used

Cleaned and engineered features from 5 thematic blocks:

| Block        | Examples                                       |
|--------------|------------------------------------------------|
| 📍 Location   | `latitude`, `longitude`, `neighbourhood_encoded` |
| 💵 Price      | `log_price`, `availability_365`, `instant_book_int` |
| 🧽 Reviews    | `has_rating`, `log_reviews_ltm`, `adj_rating` |
| 🏘️ Property   | `property_type_encoded`, `beds_per_guest`, `baths_per_guest` |
| 🧑 Host Trust | `hrt_ord` (ordinal host response time), `is_superhost` |

Also:
- Target leakage was avoided through **explicit column dropping**
- Safe encoding strategies like **train-only target encoding** were applied

---

## 📊 Modeling Approach

- **Baseline**: Random Forest (`n=100`, default)
- **Tuned Model**: GridSearchCV over `max_depth`, `min_samples_split`, `n_estimators`
- **Scoring**: `f1_weighted` (to account for class imbalance)

### Key Metrics

| Metric              | Tuned Model |
|---------------------|-------------|
| Accuracy            | ~0.71       |
| Weighted F1 Score   | ~0.71       |
| Macro F1 Score      | ~0.68       |
| Avg Tree Depth      | ~30–40      |

---

## 📈 Feature Importance (Top 7)

1. `log_reviews_ltm`
2. `has_reviews`
3. `latitude`, `longitude`
4. `log_price`
5. `availability_365`
6. `hrt_ord`
7. `neighbourhood_encoded`

---

## 🔒 Clean Modeling Practices

- 🚫 No leakage: all features used in target creation were excluded from training
- 🧪 Stratified train-test split
- 🧼 Final datasets (`train_df_ready.csv`, `test_df_ready.csv`) exported cleanly

---

## 📁 Files in this Repository

| File                          | Description                                  |
|-------------------------------|----------------------------------------------|
| `airbnb_success_pipeline.ipynb` | Full project notebook                        |
| `train_df_ready.csv`          | Cleaned training data                        |
| `test_df_ready.csv`           | Cleaned test data                            |
| `README.md`                   | This file                                    |

---

## 🚀 Next Steps

- 🧠 Integrate text-based features (e.g., listing description NLP)
- 🗓️ Add booking calendar patterns (seasonality, frequency)
- 📱 Deploy via Streamlit for agent-ready scoring tool

---

## 📂 Download Processed Datasets

Due to GitHub's file size limitations, the full processed CSVs are hosted externally:

- 🔗 [Download csv files here](https://drive.google.com/drive/folders/1pJx0ti0z8aM5jP7q7ZsDw_uCSJZ0yuKL?usp=sharing)

To use them:
1. Download all files
2. Place them in the root of this project directory
3. Open `airbnb_success_prediction.ipynb` and run the notebook

---

## 👨‍💻 Author

**Shawn Waringu**  
Data Scientist & Analyst
[LinkedIn](https://www.linkedin.com/in/shawn-chege-856048312) | [GitHub](https://github.com/your-handle)

---

