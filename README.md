# 📦 Dataset Preparation

This project uses the **Amazon Review Dataset (5-core)**.

Download the following files from:

https://cseweb.ucsd.edu/~jmcauley/datasets/amazon/links.html

Required files:

- `reviews_Books_5.json.gz`
- `reviews_CDs_and_Vinyl_5.json.gz`
- `reviews_Movies_and_TV_5.json.gz`

Place the downloaded files in:

```
./dataset/raw/
```

Expected directory structure:

```
dataset/
 └── raw/
      ├── reviews_Books_5.json.gz
      ├── reviews_CDs_and_Vinyl_5.json.gz
      └── reviews_Movies_and_TV_5.json.gz
```

---

# ⚙️ Preprocessing

This step converts **review text into review embeddings**.

Open `preprocessing.py` and select a scenario:

- `movie_to_music`
- `book_to_movie`
- `book_to_music`

Run:

```bash
python3 preprocessing.py
```

---

# 👥 User Split (Train / Val / Test)

This step splits **user indices** for training, validation, and testing.

Open `split_user.py` and select the same scenario used in preprocessing:

- `movie_to_music`
- `book_to_movie`
- `book_to_music`

Run:

```bash
python3 split_user.py
```

---

# 🧠 Pre-Training

Pre-training leverages **target-only (cold-start) users**.

Example:

```bash
python3 main_pre.py \
  --dataset=movie_to_music \
  --lamda=0.3 \
  --noise_steps=1000 \
  --history_len=30
```

---

# 🚀 Fine-Tuning

Fine-tuning leverages **overlapping users**.

Example:

```bash
python3 main.py \
  --run_name=movie2music_20 \
  --dataset=movie_to_music \
  --cold_start_ratio=0.2 \
  --lamda=0.3 \
  --noise_steps=1000 \
  --history_len=30
```

---

# 📋 Dependencies

The experiments were conducted using the following package versions:

```
fastprogress==1.0.3
numpy==1.26.4
scipy==1.13.1
sentence-transformers==4.1.0
torch==2.7.0
