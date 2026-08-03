# High School Biology LLM Evaluation Benchmark (RLHF Pairwise Dataset)

![Domain](https://img.shields.io/badge/Domain-Biology-blue)
![Format](https://img.shields.io/badge/Format-Pairwise%20Preference%20(RLHF)-green)
![Tool](https://img.shields.io/badge/Labeling%20Platform-Label%20Studio-orange)
![License](https://img.shields.io/badge/License-MIT-brightgreen)

## Executive Summary

This repository contains a human-in-the-loop (HITL) evaluation dataset designed to benchmark Large Language Model (LLM) performance on **High School Biology curriculum standards** (Grades 9–10). 

Using a pairwise comparison methodology (Model A vs. Model B), candidate model outputs were evaluated across domain accuracy, pedagogical suitability, and common model failure modes (such as omitted steps, mischaracterized gradients, or inaccurate chemical descriptions). Annotations and rationales were captured via a custom **Label Studio** visual evaluation workspace.

---

## Key Evaluation Criteria

Each prompt evaluation tests models on three key dimensions:

1. **Scientific Accuracy:** Correct identification of biological structures, mechanisms, and chemical inputs/outputs (e.g., active vs. passive transport gradients, ATP requirements).
2. **Clarity:** Clear explanations suitable for high school learners, avoiding overly dense technical jargon while maintaining scientific precision.
3. **Completeness & Constraint Adherence:** Complete execution of multi-part prompts (e.g., including examples, maintaining 1–2 paragraph length constraints).

---

## Workspace Setup (Label Studio)

Annotations were performed in a custom side-by-side pairwise interface configured in **Label Studio**.

### UI Configuration (`label_studio/config.xml`)
The workspace includes:
* **Custom Branded Header:** Evaluator metadata and case study identifier.
* **Side-by-Side Render:** Dual-card view comparing Model A and Model B responses.
* **Interactive Pairwise Selection:** `<Pairwise>` and `<Choices>` tags for winner declaration.
* **Structured SME Critique:** Mandatory `<TextArea>` input for qualitative failure analysis.

---

## Dataset Schema

The processed master dataset (`evaluations/benchmark_dataset.json`) follows this JSON schema:



```json
[
  {
    "id": "PROMPT_01",
    "domain": "Biology",
    "category": "Cellular transport mechanisms",
    "prompt": "Compare facilitated diffusion and active transport across a cell membrane...",
    "responses": {
      "model_a_name": "Model A",
      "model_a_response": "Both facilitated diffusion and active transport...",
      "model_b_name": "Model B",
      "model_b_response": "Facilitated diffusion and active transport are both ways..."
    },
    "evaluation": {
      "winning_model": "Model A",
      "sme_critique": "Model A clearly defined concentration gradients (high-to-low vs low-to-high) and accurate energy dependencies. Model B failed to mention concentration gradients entirely..."
    }
  }
]
```
## Workspace Setup & Human Annotation Interface

Annotations were performed in a custom side-by-side pairwise interface built with **Label Studio**. The UI is configured to facilitate rapid qualitative evaluation, error tagging, and detailed SME rationale submission.

![Label Studio Evaluation Workspace](assets/High_School_Biology_RLHF_benchmark.png)
*Figure 1: Custom Label Studio visual interface featuring side-by-side candidate outputs, preference selections, and SME rationale breakdown.*

### Interface Features

* **Custom Branded Header:** Displays evaluator credentials (**Margaret Kyalo**) and case study metadata (`Case Study: High School Biology RLHF benchmark`).
* **Side-by-Side Response Rendering:** Displays **Model A** (Claude) and **Model B** in styled dark-card containers for clear comparison against the target prompt.
* **Interactive Model Selector:** Checkbox selections allowing single-choice winner declaration (`Model A`, `Model B`, or `Tie / Equal Quality`).
* **Structured SME Rationale & Evaluation Breakdown:** Dedicated input area for capturing criteria-based evaluations, including:
  1. **Protein Requirement:** Evaluates explanation of phospholipid bilayer permeability.
  2. **Concentration Gradient:** Verifies correct directionality (`high-to-low` vs. `low-to-high`).
  3. **Energy (ATP):** Ensures proper distinction between passive and active mechanisms.
  4. **Example Accuracy:** Checks pedagogical validity of real-world biological examples (e.g., Glucose vs. Aquaporins).
