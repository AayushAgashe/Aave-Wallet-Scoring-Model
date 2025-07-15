# Aave Wallet Credit Scoring – ML-based Behavior Analysis

This project builds a machine learning–based credit scoring model to evaluate Ethereum wallets interacting with the Aave V2 protocol. Based on a sample of ~100K transaction-level JSON data, the model assigns a **credit score from 0 to 1000** to each wallet, indicating the reliability and risk of that wallet based on its historical on-chain behavior.

---

##  Goal

Create a scoring system that:
- Assigns **higher scores to trustworthy users** (good repayment behavior, consistent usage)
- Penalizes **risky or exploitative behavior** (liquidations, erratic usage patterns, low repayments)

---

##  Data Format

Each record contains:
- `userWallet`: Ethereum wallet address
- `action`: Type of Aave action (deposit, borrow, repay, etc.)
- `timestamp`: When the action occurred
- `actionData`: Includes `amount`, `assetPriceUSD`, etc.

---

##  Approach

### 1. Feature Engineering

For each wallet:
- `total_deposit_usd`, `total_borrow_usd`, `total_repay_usd`, etc.
- `repay_borrow_ratio`, `redeem_deposit_ratio`
- `num_liquidations`
- `tx_count`, `avg_time_diff` between actions

### 2. Heuristic Labels

We use a rule-based score to generate **proxy labels**:
- `Good (1)` → score ≥ 800
- `Bad (0)` → score ≤ 300

### 3. ML Modeling

We train an **XGBoost Classifier** to learn behavioral patterns:
- Input: Engineered features
- Output: Probability of “good” behavior
- Score = probability × 1000

---

##  Output

Each wallet receives:
- `ml_score` (0–1000): Machine-learned reliability score

The results are saved as:  
``ml_wallet_scores.csv``

---

##  Requirements

- Python 3.8+
- Pandas, Numpy, Matplotlib
- XGBoost
- Scikit-learn

You can run everything directly in Google Colab.

---

##  Files

- `wallet_scoring_ml.ipynb`: Full pipeline (Colab-ready)
- `ml_wallet_scores.csv`: Output scores
- `analysis.md`: Score distribution & behavior breakdown

---

##  Contact

For questions, email or raise an issue on the GitHub repo.
