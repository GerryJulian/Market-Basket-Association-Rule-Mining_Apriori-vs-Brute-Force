# Methodology — Association Rule Mining Comparison

## 1. Problem Statement

Given a large retail transaction dataset, identify **frequent itemsets** and derive **association rules** that reveal co-purchasing patterns. Compare two algorithms — Apriori and Brute-Force — in terms of execution time and rule output quality across varying dataset sizes.

---

## 2. Algorithms

### 2.1 Apriori Algorithm
- Based on the **anti-monotone property**: if an itemset is infrequent, all its supersets are also infrequent.
- Uses a breadth-first search (BFS) approach to generate candidate itemsets level by level.
- Significantly reduces the search space via pruning.
- Implementation: `mlxtend.frequent_patterns.apriori`

### 2.2 Brute-Force (Pairwise Enumeration)
- Exhaustively checks **all size-2 itemset combinations**.
- No pruning — every pair is evaluated for support and confidence.
- Serves as a baseline for understanding the performance advantage of Apriori.
- Complexity: O(n²) where n = number of unique items.

---

## 3. Evaluation Metrics

| Metric | Formula | Description |
|--------|---------|-------------|
| **Support** | P(A ∪ B) | Frequency of the itemset in all transactions |
| **Confidence** | P(B\|A) = P(A ∪ B) / P(A) | Probability B is bought given A is bought |
| **Lift** | Confidence / P(B) | Degree of rule strength over random chance |
| **Leverage** | P(A ∪ B) − P(A)·P(B) | Deviation from independence |
| **Conviction** | (1 − P(B)) / (1 − Confidence) | Sensitivity to counterexamples |

---

## 4. Scalability Study Design

| Subset | Transactions |
|--------|-------------|
| Sample 1 | 5,000 |
| Sample 2 | 10,000 |
| Sample 3 | 15,000 |
| Sample 4 | 20,000 |

Each subset is processed through both algorithms independently, and execution time is recorded using Python's `time` module.

---

## 5. Actionable Rule Criteria

A rule is considered **actionable** if it meets both thresholds:
- **Lift ≥ 1.2** (positive correlation above chance)
- **Confidence ≥ 0.6** (at least 60% conditional probability)
