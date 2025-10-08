# Bank_Credit

#  Dataset Overview – Bank GoodCredit Credit Risk Project

## Business Case:

Bank GoodCredit wants to assess the **creditworthiness** of its credit card customers by predicting if a customer is likely to **default** (i.e., become 30+ days past due).
This helps reduce credit risk and improve loan decisions.

**Target Variable:**
`Bad_label`

* `0` → Good credit history
* `1` → Bad credit history (default risk)

---

###  **Dataset Description**

The data is stored in a **MySQL database** with the following three main tables:

---

#### 1. **Cust\_Account**

Customer’s historical account and payment information.

* `customer_no`
* `opened_dt`, `last_paymt_dt`, `closed_dt`
* `cur_balance_amt`, `creditlimit`, `cashlimit`
* `paymenthistory1`, `paymentfrequency`
* `rateofinterest`, `actualpaymentamount`
* ... *(more account-specific fields)*

---

#### 2. **Cust\_Enquiry**

Contains credit enquiry history for each customer.

* `customer_no`
* `enquiry_dt`, `enq_purpose`, `enq_amt`
* Used to evaluate customer's recent credit-seeking behavior.

---

#### 3. **Cust\_Demographics**

Includes demographic and anonymized model features.

* `customer_no`
* `feature_1` to `feature_79`
* `Bad_label` (target variable)

---

### **Project Goal**

Build a classification model using this data to:

* Analyze customer behavior
* Select relevant features
* Predict default risk (Bad\_label)
* Evaluate performance using Gini score and decile ranking




# Report on challange faced :-

### 1. Data Quality Issues
- **Missing Values**: Several fields like `paymenthistory2`, `feature_8`, `feature_9`, etc. have high missingness.
- **Mixed Data Types**: Columns such as `opened_dt`, `last_paymt_dt`, `rateofinterest` contain mixed types (string + numeric).
- **Inconsistent Formats**: Date fields (`opened_dt`, `enquiry_dt`, `closed_dt`) are not standardized and need transformation.

### 2. Data Redundancy & Irrelevance
- Presence of **ID-like variables** (`customer_no`, `upload_dt`) which do not contribute to prediction.
- **Highly correlated features** (e.g., `cur_balance_amt` vs. `high_credit_amt`) create redundancy.
- Some features may be **constant or near-constant**, adding no predictive value.

### 3. Class Imbalance
- Target variable `Bad_label` likely has **fewer bad customers (1)** compared to good ones (0).
- Imbalanced datasets lead to biased models that predict mostly the majority class.

### 4. Privacy & Feature Obfuscation
- Demographic variables (`feature_1` to `feature_79`) are anonymized.
- Lack of semantic meaning makes interpretation and business validation difficult.

### 5. Data Integration Challenges
- Data comes from **multiple sources** (Accounts, Enquiries, Demographics).
- Requires **joining/merging on customer_no**; mismatches or missing keys may cause data loss.

### 6. Outliers & Skewness
- Financial features (`cur_balance_amt`, `enq_amt`, `high_credit_amt`) show **large ranges and skewed distributions**.
- Outliers may distort model performance if not handled.

### 7. Temporal Issues
- Payment history and enquiry data are **time-dependent**.
- Model may overfit if recency trends are not captured properly.
