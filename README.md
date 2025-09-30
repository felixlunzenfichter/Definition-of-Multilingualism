# Definition of Multilingualism

## Overview

Multilingualism is the ability to understand and/or produce statements across multiple languages, enabling communication between speakers who would otherwise not understand each other.

## Core Components

### 1. Set of All Statements

Let S be the set of all possible statements, where each statement s is a two-tuple (syntax, semantics):

- syn(s): the linguistic form/expression
- sem(s): the meaning/content

### 2. Graph Structure

- **Nodes**: V is the set of all language speakers that exist
- **Edges**: E = V × V \ {(i,i) : i ∈ V}, a directed graph with no self-loops

### 3. Vocabulary Definitions

For each speaker i ∈ V:

- **Active vocabulary**: vocab_active(i) ⊆ S, the finite set of all statements i produces in their lifetime (in natural situations). The restriction to natural situations ensures we only count real communicative acts, not artificial attempts to game the metric by reciting lists or deliberately producing statements solely to manipulate the multilingualism score.

- **Complete passive vocabulary (Vollständiger passiver Wortschatz)**: vocab_passive_complete(i) ⊆ S, the infinite set of all statements i could theoretically understand, including all grammatically correct constructions in known languages.

- **Active-passive vocabulary (Aktiv-passiver Wortschatz)**: vocab_passive_actual(i) ⊆ S, the set of statements i has actually heard and understood during their lifetime. This represents the real-world passive vocabulary based on actual exposure.

- Note: vocab_active(i) and vocab_passive_actual(i) may overlap but neither is necessarily a subset of the other. One can produce statements never heard before, and hear statements never produced. Both are subsets of vocab_passive_complete(i)

### 4. Communication Improvement

For each (k,i,j) with k ∈ V and (i,j) ∈ E, define the Communication Improvement Set:

COMM_IMPROVEMENT(k; i,j) = {(s,s') : s ∈ vocab_active(i) \ vocab_passive_complete(j),
s ∈ vocab_passive_complete(k),
s' ∈ vocab_passive_complete(j) ∩ vocab_active(k),
sem(s) = sem(s')}

Define the Total Communication Improvement Set for a speaker k:

TOTAL_COMM_IMPROVEMENT(k) = ⋃_(i,j)∈E COMM_IMPROVEMENT(k; i,j)

### 5. Multilingualism Scores

Let M₁ = (1/|V|) × Σ_i∈V |{sem(s) : s ∈ vocab_active(i)}|

Since different languages correspond to different syntactic forms mapping to the same semantics, we use this normalization constant to capture the average size of the minimal set of expressions or statements necessary to express everything a person actually says in practice.

- **M_passive(k)** = |{s : ∃s' with (s,s') ∈ TOTAL_COMM_IMPROVEMENT(k)}| / M₁
- **M_active(k)** = |{s' : ∃s with (s,s') ∈ TOTAL_COMM_IMPROVEMENT(k)}| / M₁

These yield the normalized multilingualism scores for passive (understanding) and active (speaking).

## Examples

### Example 1: Bilingual Translator
Consider a translator who speaks English and Spanish fluently. They can:
- Understand statements from English-only speakers that Spanish-only speakers cannot
- Produce equivalent Spanish statements that convey the same meaning
- Enable communication between monolingual English and Spanish speakers

### Example 2: Complete Passive vs Active Multilingualism
A person might:
- **Complete Passive**: Theoretically understand multiple languages (high vocab_passive_complete)
- **Active-Passive**: Have actually heard and understood fewer statements (smaller vocab_passive_actual)
- **Active**: Only speak one or two languages fluently (vocab_active)
- This captures the distinction between theoretical understanding, actual exposure, and production ability