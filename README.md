# 🎬 Movie Recommendation System

A smart movie recommender using:
- 🔥 Popularity (vote average & count)
- 🎯 Content similarity (TF-IDF + cosine)
- 🧠 Embeddings with natural language input (SentenceTransformer)

---

## 📂 Features

- Recommend top-rated movies overall
- Find movies similar to a title you've seen
- Type what you're in the mood for and get personalized suggestions

---

## 🛠️ Setup

Install required dependencies:

```bash
pip install pandas scikit-learn sentence-transformers tqdm
```

Make sure your project folder includes the following datasets:

```
movies_metadata.csv
ratings.csv
```

---

## 🚀 Example Usage

```python
from sentence_transformers import SentenceTransformer

# Load the model
sentence_model = SentenceTransformer("all-MiniLM-L6-v2")

# --- 1. Popularity-based Recommender ---
popularity_df = movie_night_recommender(
    df=movies_metadata,
    method='popularity',
    criterion='vote_average',
    top_n=5
)
print(popularity_df[['title', 'vote_average']].to_string(index=False))

# --- 2. Similarity-based Recommender ---
similarity_df = movie_night_recommender(
    df=cosine_sim_df,
    method='rating_similarity',
    user_input="The Matrix",
    top_n=5
)
print(similarity_df.to_string(index=False))

# --- 3. Embedding-based Recommender ---
embedding_df = movie_night_recommender(
    df=movies_metadata,
    method='movie_description',
    user_input="A gritty sci-fi thriller with philosophical undertones",
    model=sentence_model,
    top_n=5
)
print(embedding_df[['title', 'similarity']].to_string(index=False))
```

---

## 🧠 How It Works

- **Popularity**: Sorts movies by highest vote average or count.
- **Content Similarity**: Uses TF-IDF on movie descriptions with cosine similarity.
- **Embeddings**: Converts your text prompt into vector space using `SentenceTransformer`, then compares it to movie embeddings.

---