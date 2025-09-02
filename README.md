# HR Analytics: Job Change of Data Scientists  

## 📌 Project Overview  
A company active in **Big Data and Data Science** wants to hire data scientists among people who successfully pass the training courses it conducts.  

Many individuals sign up for these courses. However, the company needs to determine which candidates truly intend to work for the company after training and which ones are mainly seeking other employment opportunities. This insight helps reduce costs and time, improves the quality of training, and supports better planning and categorization of candidates.  

The company already has access to valuable information from candidate signups and enrollment, including **demographics, education, and work experience**. This project integrates and analyzes that data to better understand employment motivation.  

---

## 📊 Data Sources  

### 1. Enrollies’ Data  
As enrollies submit their requests to join the course via Google Forms, their information is stored in a Google Sheet containing:  
- **enrollee_id**: unique ID of an enrollee  
- **full_name**: full name of an enrollee  
- **city**: the name of an enrollee’s city  
- **gender**: gender of an enrollee  

📂 Source: [Google Sheet](https://docs.google.com/spreadsheets/d/1VCkHwBjJGRJ21asd9pxW4_0z2PWuKhbLR3gUHm-p4GI/edit?usp=sharing)  

---

### 2. Enrollies’ Education  
After enrollment, each participant completes a form about their education level. This information is digitized manually and stored in Excel format.  

Columns include:  
- **enrollee_id**: unique identifier for each enrollee  
- **enrolled_university**: university enrollment status (`no_enrollment`, `Part time course`, `Full time course`)  
- **education_level**: highest level of education attained (e.g., Graduate, Masters)  
- **major_discipline**: primary field of study (e.g., STEM, Business Degree)  

📂 Source: [Excel File](https://assets.swisscoding.edu.vn/company_course/enrollies_education.xlsx)  

---

### 3. Enrollies’ Working Experience  
Collected via a manual survey and stored in CSV format.  

Columns include:  
- **enrollee_id**: unique identifier for each enrollee  
- **relevent_experience**: indicates whether the enrollee has relevant work experience (`Has relevent experience` / `No relevent experience`)  
- **experience**: number of years of work experience (numeric or range, e.g., `>20`, `<1`)  
- **company_size**: size of the company worked at (e.g., `50−99`, `100−500`)  
- **company_type**: type of company worked at (e.g., Pvt Ltd, Funded Startup)  
- **last_new_job**: years since last job change (e.g., `never`, `>4`, `1`)  

📂 Source: [CSV File](https://assets.swisscoding.edu.vn/company_course/work_experience.csv)  

---

### 4. Training Hours  
From the LMS database, we can retrieve the number of training hours each student has completed.  

Database connection details:  
- **Database type**: MySQL  
- **Host**: 112.213.86.31  
- **Port**: 3360  
- **Login**: etl_practice  
- **Password**: 550814  
- **Database name**: `company_course`  
- **Table name**: `training_hours`  

---

### 5. City Development Index  
The **City Development Index (CDI)** measures the level of development in cities and may be significant for predicting employment motivation.  

📂 Source: [City Development Index](https://sca-programming-school.github.io/city_development_index/index.html)  

---

### 6. Employment  
From the LMS database, we can also retrieve employment status. If a student is marked as **employed**, it indicates they started working for the company after finishing the course.  

Database connection details:  
- **Database type**: MySQL  
- **Host**: 112.213.86.31  
- **Port**: 3360  
- **Login**: etl_practice  
- **Password**: 550814  
- **Database name**: `company_course`  
- **Table name**: `employment`  

---

## ⚙️ Project Steps & Decisions  

### 1. Data Collection  
- **What was done**: Extracted raw data from Google Sheets, Excel, CSV, MySQL, and HTML sources. Merged datasets using `enrollee_id` as the unique key.  
- **Why**: To consolidate information from multiple systems into one unified dataset, ensuring each enrollee’s profile is complete for analysis.  

---

### 2. Data Cleaning  
- **What was done**:  
  - Handled missing values (imputation for `education_level`, removal of duplicates).  
  - Normalized categorical variables (e.g., `education_level`, `company_type`).  
  - Standardized inconsistent values (e.g., company size ranges, job change categories).  
  - Converted data types (e.g., transforming `experience` ranges into numeric values).  

- **Why**: To improve data quality and consistency. Clean data reduces bias, prevents errors in analysis, and ensures reliable model performance.  

---

### 3. Data Transformation  
- **What was done**:  
  - Created a **binary employment outcome** (employed vs. not employed).  
  - Grouped years of experience into categorical bins.  
  - Merged **City Development Index (CDI)** into the main dataset.  

- **Why**: To prepare the dataset for analysis and modeling. These transformations simplify complex variables, reduce noise, and incorporate external context that may influence employment outcomes.  

---

## 📂 Code & Notebook  
- Full analysis is available in the Colab notebook: [Google Colab Link](https://colab.research.google.com/drive/1TPV5f0WXtNPRJvEak92_N71BN1PI1b91?usp=sharing)  
- Or in the attached file: **`HR Analytics- Job Change of Data Scientists.ipynb`**
- The final data after ETL can be found in **`HR_enrollies_data_2025`**
