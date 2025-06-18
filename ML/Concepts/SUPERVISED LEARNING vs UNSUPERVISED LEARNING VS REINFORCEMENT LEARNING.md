#ML #Algorithms 
# 🧠 Machine Learning Types

## 🔹 Supervised Learning

- **Goal**: Learn a mapping from input `X` to output `Y` using **labeled data**.
- **Labeled Data**: ✅ Yes
- **Output**: Predict labels or continuous values
- **Examples**:
  - Classification: Spam detection, disease diagnosis
  - Regression: House price prediction, stock price forecasting
- **Real-world Analogy**: Student learning with an answer key — gets feedback.
- **Popular Algorithms**:
  - Linear Regression
  - Logistic Regression
  - Decision Trees
  - Support Vector Machines (SVM)
  - Neural Networks

---

## 🔹 Unsupervised Learning

- **Goal**: Discover hidden patterns from **unlabeled data**.
- **Labeled Data**: ❌ No
- **Output**: Groupings, clusters, structure, feature reduction
- **Examples**:
  - Clustering: Customer segmentation, social network analysis
  - Dimensionality Reduction: PCA, t-SNE
- **Real-world Analogy**: Student trying to categorize books without genre info.
- **Popular Algorithms**:
  - K-Means Clustering
  - Hierarchical Clustering
  - DBSCAN
  - Principal Component Analysis (PCA)
  - Autoencoders

---

## 🔹 Reinforcement Learning

- **Goal**: Learn to make decisions by interacting with an **environment** to maximize **reward**.
- **Labeled Data**: 🚫 No fixed dataset; learns via experience
- **Output**: A **policy** — best strategy to take actions
- **Core Concepts**:
  - **Agent**: Learner/decision-maker
  - **Environment**: Where the agent acts
  - **State**: Current situation
  - **Action**: Choice made by the agent
  - **Reward**: Feedback signal
- **Examples**:
  - Game AI: AlphaGo, Dota 2 bot
  - Robotics: Balancing, walking
  - Autonomous Vehicles
- **Real-world Analogy**: Dog learning tricks with treats and scolding.
- **Popular Algorithms**:
  - Q-Learning
  - Deep Q-Networks (DQN)
  - Proximal Policy Optimization (PPO)
  - Actor-Critic methods

---

## 🔁 Summary Table

| Feature        | Supervised        | Unsupervised         | Reinforcement             |
|----------------|-------------------|-----------------------|----------------------------|
| Data Type      | Labeled           | Unlabeled             | Trial & error experience  |
| Feedback       | Direct (correct labels) | None            | Indirect (reward)         |
| Goal           | Predict outcome   | Discover structure    | Learn policy (best action)|
| Key Usage      | Classification, Regression | Clustering, Feature Reduction | Games, Robotics, Real-time decisions |


