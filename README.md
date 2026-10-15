#  ISO/IEC 5259 Data Quality Agent for AI/ML

An automated Data Quality Assessment tool built in Python and designed for Google Colab. This project implements key data quality dimensions and metrics aligned with the **ISO/IEC 5259** standard series for Artificial Intelligence and Machine Learning data quality.

---

##  Overview

Ensuring high data quality is critical for training robust, fair, and reliable Machine Learning models. This agent evaluates datasets across core compliance dimensions specified in **ISO/IEC 5259-2 (Data Quality Measures)**:

* **Completeness:** Evaluates missing values across the dataset and individual attributes.
* **Uniqueness:** Identifies duplicate records and calculates dataset uniqueness scores.
* **Validity:** Validates data against domain-specific logical constraints and range checks (e.g., non-negative income, valid age ranges).
* **Representativeness & Fairness:** Analyzes categorical distributions across protected or sensitive attributes (e.g., region, gender) to flag potential representation imbalance.

---

##  Features

* **Interactive File Upload:** Upload any `.csv` file directly within Google Colab via interactive prompt.
* **Fallback Sample Dataset:** Built-in test data for quick execution and trial runs.
* **Custom Validation Rules:** Flexible lambda-based validation support for column-specific rules.
* **ISO Compliance Report:** Generates a structured summary printout formatted to compliance reporting standards.

---

##  Prerequisites

To run this notebook/script, you only need Python 3.x and standard data science libraries:

* `pandas`
* `numpy`
* `google-colab` (when running in Google Colab environment)

---

##  Quick Start (Google Colab)

1. Open a new notebook in **Google Colab**.
2. Copy the code from `agent.py` into a code cell.
3. Run the cell.
4. When prompted, click **Choose Files** to upload your CSV dataset.
5. View your **ISO/IEC 5259 Compliance Report** printed in the output!

---

##  Usage & Customization

You can define custom validation rules for your specific dataset columns in the code:

```python
# Custom validity rules aligned with your schema
validation_rules = {
    "age": lambda x: pd.isna(x) or (0 < x < 120),
    "income": lambda x: pd.isna(x) or (x >= 0)
}

# Specify protected attributes for bias & balance checks
agent = ISO5259DataQualityAgent(
    df=df, 
    target_column="target", 
    protected_attributes=["region", "gender"]
)

agent.run_full_evaluation(validity_rules=validation_rules)
agent.print_compliance_report()
