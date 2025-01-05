# Anime Recommendation App

DEMO: [45.136.205.175](http://45.136.205.175/)

**Stack:** Python 3.10, FastAPI, Next.js, Nginx, MongoDB

---

### Architecture
![Architecture](/docs/9.png)

---

## Run the Project

```bash
git clone https://github.com/Tsuchikage/anime-recommendation-app.git
```

```bash
mkdir -p anime-recommendation-app/server/src/datasets
```

```bash
cd anime-recommendation-app/server/src/datasets
```

```bash
wget https://storage.yandexcloud.net/anime/ratings.csv
```

```bash
wget https://storage.yandexcloud.net/anime/migration.xlsx
```

```bash
cd ~/anime-recommendation-app/
```

```bash
cp .env.example .env
```

```bash
docker-compose up --build -d
```

---

### Screenshots
![Screenshot 1](/docs/1.jpg)
![Screenshot 2](/docs/2.jpg)
![Screenshot 3](/docs/3.jpg)
![Screenshot 4](/docs/4.jpg)
![Screenshot 5](/docs/11.jpg)
![Screenshot 6](/docs/5.jpg)
![Screenshot 7](/docs/6.jpg)
![Screenshot 8](/docs/7.jpg)
![Screenshot 9](/docs/8.png)

---

## Project Description

### Objective
Develop a recommendation service that provides high-quality suggestions for spending leisure time, taking into account user preferences in genres and limited time availability (10-20 minutes).

---

### Recommendation System Description

The project includes two types of recommendation systems: **item-based** (based on item similarity) and **content-based** (based on content analysis).

#### **Item-based Recommendation System**

This system analyzes item similarities based on user ratings, leveraging a k-nearest neighbors (k-NN) algorithm. Key steps include:

- **Data Preparation:**
  - Load anime data from MongoDB, including titles, descriptions, types, and episode counts.
  - Split data into **60% training** and **40% testing** sets.
  - Create a `train_ratings` dataset containing user ratings.

- **User-Item Matrix Creation:**
  - Convert `train_ratings` into a pivot table where rows represent users, columns represent anime, and values are ratings.
  - Replace missing values (NaN) with zeros.
  - Convert the dense matrix into a CSR (Compressed Sparse Row) format for efficiency.

- **Finding Nearest Neighbors:**
  - Initialize a k-NN model using cosine distance and the "brute" algorithm.
  - Train the model on the training dataset.

- **Generating Recommendations:**
  - Filter anime based on the search query.
  - Identify the matrix index of the selected anime.
  - Find the nearest neighbors and retrieve recommendations.
  - Return a dictionary with recommendations.

---

#### **Content-based Recommendation System**

This system analyzes similarities between items based on their textual features using TF-IDF and k-NN. Key steps include:

- **Data Preparation:**
  - Load anime data from MongoDB.
  - Create a **tfidf_matrix** based on anime descriptions using TF-IDF.
  - Load a k-NN model using cosine distance and the "brute" algorithm.

- **Generating Recommendations:**
  - Search for anime titles matching the query.
  - Find the index of each selected anime in the feature matrix.
  - Use k-NN to identify similar items.
  - Return a dictionary with recommendations.

---

### Metrics
**Mean average precision at K (map@K)** - дает представление о том, насколько релевантен список рекомендуемых элементов. 

![Metrics Graph](/docs/10.png)
