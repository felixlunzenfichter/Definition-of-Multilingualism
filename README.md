# Definition of Multilingualism

## 1. Set of All Statements

Let S be the set of all possible statements, where each statement s is a two-tuple (syntax, semantics):

- syn(s): the linguistic form/expression
- sem(s): the meaning/content

## 2. Graph Structure

- **Nodes**: V is the set of all language speakers that exist
- **Edges**: E = V × V \ {(i,i) : i ∈ V}, a directed graph with no self-loops

## 3. Vocabulary Definitions

For each speaker i ∈ V:

- **Active vocabulary**: vocab_active(i) ⊆ S, the finite set of all statements i produces in their lifetime (in natural situations). The restriction to natural situations ensures we only count real communicative acts, not artificial attempts to game the metric by reciting lists or deliberately producing statements solely to manipulate the multilingual score.
- **Passive vocabulary**: vocab_passive(i) ⊆ S, the infinite set of all statements i can understand
- Note: vocab_active(i) ⊆ vocab_passive(i)

## 4. Communication Improvement

For each (k,i,j) with k ∈ V and (i,j) ∈ E, define the Communication Improvement Set:

COMM_IMPROVEMENT(k; i,j) = {(s,s') : s ∈ vocab_active(i) \ vocab_passive(j),
s ∈ vocab_passive(k),
s' ∈ vocab_passive(j) ∩ vocab_active(k),
sem(s) = sem(s')}

Define the Total Communication Improvement Set for a speaker k:

TOTAL_COMM_IMPROVEMENT(k) = ⋃_(i,j)∈E COMM_IMPROVEMENT(k; i,j)

## 5. Normalization Constant

### 5.1 Comprehension
For speakers i, j ∈ V:
- comprehension(i→j) = |vocab_active(i) ∩ vocab_passive(j)| / |vocab_active(i)|

### 5.2 Mutual Comprehension Group
A set G ⊆ V is a 99% comprehension group if:
- ∀i,j ∈ G: comprehension(i→j) ≥ 0.99

### 5.3 Maximal Mutual Comprehension Group
A 99% comprehension group G is maximal if:
- ∀j ∈ V\G, ∀i ∈ G: comprehension(i→j) < 0.99 ∨ comprehension(j→i) < 0.99

### 5.4 M₁ Definition
Let MCG = {G₁, G₂, ..., Gₙ} be the set of all maximal 99% comprehension groups.

M₁ = (1/|MCG|) × Σ_G∈MCG [(1/|G|) × Σ_i∈G |{syn(s) : s ∈ vocab_active(i)}|]

This captures the average size of syntactic variation within each language community.

## 6. Multilingualism Scores

- **Passive Multilingual Score: M_passive(k)** = |{s : ∃s' with (s,s') ∈ TOTAL_COMM_IMPROVEMENT(k)}| / M₁
- **Active Multilingual Score: M_active(k)** = |{s' : ∃s with (s,s') ∈ TOTAL_COMM_IMPROVEMENT(k)}| / M₁

These yield the normalized multilingualism scores for passive (understanding) and active (speaking).