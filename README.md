# SOICT2025 Submission 3654: Comprehensive Assessment of SLM Performance on Vietnamese High School History Tasks

This is the repository behind our submission in the SOICT2025 conference. Here you will find charts, figures and summary tables behind the key findings we made in our experiment which had to be omitted to fit SOICT's 11 page requirement.

- The Dataset folder contains our multiple-choice dataset of 560 questions collected from University Entrance Exams from the years 2020-2024, and a guideline as to how we labeled questions by category.

- Baseline/ZeroshotCOT/FewshotCOT Results folders contain the inference from each and every model for each prompting type. It should be noted that the Qwen3-4b model was tested with both enable_thinking=True and enable_thinking=False, and the GPT-OSS-20B model was tested with reasoning_effort set to low.

- The 'Figures' folder contains any illustrative table or chart from our experiments, as well as the mcq_accuracies Excel file, detailing the accuracy of all 25 SLMs on 3 prompting types, stratified by difficulty and category.

# Performance on Multiple-Choice Questions
---
Accuracy of all 25 models
<img width="1704" height="351" alt="bslne_0shot_5shot" src="https://github.com/user-attachments/assets/d76225a1-e19d-4c2e-a860-6e90b49eb461" />
---

# LLM Judge Performance Analysis: Essay Questions

## Executive Summary

Comprehensive analysis of Large Language Model (LLM) Judge performance in evaluating Vietnamese history essay responses across multiple evaluation criteria. The analysis compares LLM assessments against human rater judgments to identify areas of strength and limitation.

---

## 1. Correlation Analysis: Key Findings

Our correlation analysis examines LLM Judge performance relative to human raters across four evaluation criteria. Table 1 presents the overall Spearman correlation coefficients.

### Table 1: Overall Spearman Correlation Across All Criteria

| Criterion | R1 vs R2 | R1 vs LLM | R2 vs LLM | Human vs LLM (Avg) |
|-----------|----------|-----------|-----------|-------------------|
| Comprehensibility | 0.5395 | 0.5823 | 0.7680 | 0.6752 |
| Correctness | 0.7109 | 0.8353 | 0.7081 | 0.7717 |
| Response Structure | 0.9233 | 0.8863 | 0.8616 | 0.8740 |
| Response Format | 0.8484 | 0.4132 | 0.5782 | 0.4957 |

*Note: R1 represents Rater Liêm; R2 represents Rater Đăng*

### 1.1 Critical Findings by Criterion

**Response Format: Area of Low Agreement**

The Response Format criterion exhibits the largest discrepancy between human and LLM agreement. While inter-rater agreement is high (ρ = 0.8484), the average Human-LLM agreement is the lowest observed in this study (ρ = 0.4957). This pattern indicates that rule-based formatting evaluation, including spelling and invalid character detection, remains a significant challenge for the LLM Judge, despite being a clear and objective task for human raters.

**Correctness: LLM Strength**

For the Correctness criterion, Human-LLM agreement (ρ = 0.7717) exceeds Human-Human agreement (ρ = 0.7109). This finding suggests the LLM Judge not only performs competently but demonstrates greater stability and consistency than human raters in fact-checking information against provided context. This supports the hypothesis that LLMs serve as reliable tools for objective fact-verification tasks.

**Response Structure: Area of Very High Agreement**

Exceptionally high Human-LLM agreement (ρ = 0.8740) nearly matches Human-Human agreement (ρ = 0.9233) for this criterion. These results indicate that the LLM Judge effectively evaluates logical cohesion, argumentation quality, and overall essay structure.

**Comprehensibility: LLM Strength**

Moderate-to-high Human-LLM agreement (ρ = 0.6752) again exceeds Human-Human agreement (ρ = 0.5395). Similar to the Correctness criterion, the LLM Judge demonstrates greater stability and consistency than human raters for this subjective evaluation dimension.

---

## 2. Model-Specific Analysis

To obtain more granular insights, we segmented the correlation analysis by individual model performance. Table 2 presents these results.

### Table 2: Correlation Analysis by Model

| Model | Criterion | R1 vs R2 | R1 vs LLM | R2 vs LLM | Human vs LLM (Avg) |
|-------|-----------|----------|-----------|-----------|-------------------|
| **Vinallama 2.7B** | Comprehensibility | 0.5849 | 0.4978 | 0.4108 | 0.4543 |
| | Correctness | 0.0940 | 0.4490 | 0.2239 | 0.3364 |
| | Response Structure | 0.4847 | 0.2694 | 0.2553 | 0.2623 |
| | Response Format | 0.6985 | 0.1727 | 0.1545 | 0.1636 |
| **Qwen3 8B** | Comprehensibility | 0.6406 | 0.7564 | 0.4447 | 0.6006 |
| | Correctness | 0.7347 | 0.8791 | 0.6521 | 0.7656 |
| | Response Structure | NaN | 0.9009 | NaN | NaN |
| | Response Format | NaN | NaN | NaN | NaN |
| **Vistral 7B** | Comprehensibility | 0.9996 | 0.4326 | 0.4324 | 0.4325 |
| | Correctness | 0.8928 | 0.8953 | 0.7522 | 0.8237 |
| | Response Structure | 1.0000 | 0.8624 | 0.8624 | 0.8624 |
| | Response Format | NaN | NaN | NaN | NaN |
| **Gemma 2B** | Comprehensibility | 0.6758 | 0.6417 | 0.6536 | 0.6476 |
| | Correctness | 0.4304 | 0.6207 | 0.6151 | 0.6179 |
| | Response Structure | NaN | NaN | NaN | NaN |
| | Response Format | NaN | NaN | NaN | NaN |

*Note: NaN values indicate ceiling effects resulting from constant scores*

### 2.1 Interpretation of Results

The NaN values in Table 2 represent ceiling effects rather than errors. These occur when raters assign constant scores across all responses from a single model for a specific criterion, resulting in zero variance and mathematically undefined correlation coefficients.

**Performance Divergence Patterns**

*High-Performance Models (Qwen3, Gemma, Vistral):* These models consistently produced responses with such excellent Response Structure and Response Format that raters assigned constant maximum scores, making correlation measurement impossible. This consistency precluded meaningful variance analysis.

*Low-Performance Model (Vinallama):* This model was the only one producing sufficient variance in Response Structure. However, on this data, LLM Judge agreement with humans was extremely low (ρ = 0.2623), substantially below Human-Human agreement (ρ = 0.4847).

These findings indicate that the LLM Judge struggles to evaluate nuanced, rule-based criteria such as Response Structure when quality is inconsistent. Conversely, for complex criteria including Correctness and Comprehensibility, where variance exists across all models, the LLM Judge maintains stability and reliability, often achieving high correlation with human raters.

---

## 3. Question Type Analysis

We analyzed whether LLM Judge performance varies based on cognitive complexity by grouping the 200 responses according to annotated question types and recalculating correlations. Table 3 presents these results.

### Table 3: Correlation Analysis by Question Type

| Question Type | Criterion | Samples | R1 vs R2 | Human vs LLM (Avg) |
|---------------|-----------|---------|----------|-------------------|
| **So sánh, đối chiếu** | Comprehensibility | 32 | 0.5785 | 0.7757 |
| (Comparison) | Correctness | 32 | 0.7056 | 0.8395 |
| | Response Structure | 32 | 0.9455 | 0.8578 |
| | Response Format | 32 | 0.9025 | 0.6861 |
| **Đánh giá** | Comprehensibility | 60 | 0.5775 | 0.6657 |
| (Evaluation) | Correctness | 60 | 0.6484 | 0.7520 |
| | Response Structure | 60 | 0.9275 | 0.8730 |
| | Response Format | 60 | 0.8441 | 0.4182 |
| **Kết quả / Ý nghĩa** | Comprehensibility | 56 | 0.5191 | 0.6163 |
| (Outcome / Significance) | Correctness | 56 | 0.6818 | 0.7123 |
| | Response Structure | 56 | 0.9119 | 0.8999 |
| | Response Format | 56 | 0.8450 | 0.4470 |
| **Bối cảnh / Nguyên nhân** | Comprehensibility | 52 | 0.5041 | 0.6898 |
| (Context / Cause) | Correctness | 52 | 0.8156 | 0.7909 |
| | Response Structure | 52 | 0.9240 | 0.8578 |
| | Response Format | 52 | 0.8245 | 0.5206 |

### 3.1 Key Conclusions

This analysis confirms two critical findings. First, the LLM Judge's strong performance on Correctness and Comprehensibility extends beyond simple factual questions, maintaining high agreement with humans even for complex comparison and evaluation tasks. Second, the judge's poor performance on Response Format and inflated correlation on Response Structure remain consistent across question types, confirming these behaviors are independent of the question's reasoning complexity.

---

## 4. Response Length Analysis

To test the hypothesis that the LLM Judge relies on surface-level cues and struggles with longer, complex essays, we analyzed correlations based on response length. The 200 responses were segmented into three equal-sized quantiles based on token count: Short (13-51 tokens), Medium (52-355 tokens), and Long (356-2050 tokens).

### Table 4: Correlation Analysis by Response Length

| Length Group | Criterion | Samples | R1 vs R2 | Human vs LLM (Avg) |
|--------------|-----------|---------|----------|-------------------|
| **Short (13-51 tokens)** | Comprehensibility | 68 | -0.6747 | 0.1556 |
| | Correctness | 68 | 0.6746 | 0.7250 |
| | Response Structure | 68 | 1.0000 | 0.9453 |
| | Response Format | 68 | NaN | NaN |
| **Medium (52-355 tokens)** | Comprehensibility | 65 | 0.6842 | 0.8092 |
| | Correctness | 65 | 0.8104 | 0.8604 |
| | Response Structure | 65 | NaN | NaN |
| | Response Format | 65 | 1.0000 | 0.8739 |
| **Long (356-2050 tokens)** | Comprehensibility | 67 | 0.8655 | 0.7530 |
| | Correctness | 67 | 0.6694 | 0.7965 |
| | Response Structure | 67 | 0.8155 | 0.7755 |
| | Response Format | 67 | 0.7097 | -0.1815 |

### 4.1 Key Findings

**Robust Criteria Performance**

For Correctness and Comprehensibility, Human-LLM agreement remained high and stable regardless of response length. This indicates the LLM Judge demonstrates robustness when evaluating semantic content and overall quality.

**Performance Degradation in Long Texts**

The most critical findings relate to rule-based criteria. While ceiling effects were observed in short and medium response groups, the LLM Judge's performance deteriorated substantially in the long response group:

- **Response Format:** The Human-LLM correlation inverted to -0.1815, while Human-Human agreement remained high (0.7097). This suggests the LLM Judge fails to track formatting rules across extended context windows.

- **Response Structure:** The Human-LLM correlation (0.7755) fell below Human-Human correlation (0.8155), supporting the hypothesis that the judge's ability to assess semantic cohesion weakens as logical complexity increases.

---

## Conclusions

This analysis reveals distinct patterns in LLM Judge performance across evaluation criteria, models, question types, and response lengths. The LLM Judge demonstrates particular strength in evaluating semantic content (Correctness and Comprehensibility) while showing significant limitations in rule-based formatting assessment, especially for longer responses. These findings have important implications for the deployment of LLM-based evaluation systems in educational contexts.
