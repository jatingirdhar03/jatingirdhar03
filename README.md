## Hi there 👋
I'm Jatin Girdhar, 
MBA Student at UCW,
Vancouver, BC.

# DAP Design and Implementation (Individual work – Jatin)

# Introduction

In the era of data-driven decision-making, the ability to extract, process, and analyze data efficiently is essential for organizations and individuals alike. This project focuses on designing and implementing a Data Analytics Platform (DAP) using AWS cloud-based services, applied specifically to the ‘Public Art – Artists’ dataset from Vancouver's Open Data portal. The primary objective is to harness the potential of data to uncover meaningful insights, such as understanding the distribution of artists by country in Vancouver and exploring artist-related data within specific geographies like North America. By leveraging AWS tools such as Amazon S3, AWS Glue DataBrew, and AWS Glue, this project outlines a systematic approach to data ingestion, profiling, cleaning, and transformation, culminating in a robust pipeline for both descriptive and exploratory analysis. This project aims to demonstrate the value of cloud-based analytics in enhancing decision-making and delivering actionable insights.

## Dataset Selection
For my part, I chose the ‘Public art – Artists’ dataset from [Vancouver Open Data](https://opendata.vancouver.ca/explore/dataset/public-art-artists/information/).

### Figure 2a
<img width="846" alt="Screenshot 2024-12-05 at 5 06 59 PM" src="https://github.com/user-attachments/assets/afd075de-b8de-4517-a301-6074dc637edb">

**Original DataSet**

---

## Descriptive Analysis

The main goal of performing Descriptive Analysis from the available data was to get information regarding the country that has the maximum number of artists in the city of Vancouver. Analyzing this on the Open Data Vancouver website, we get the following column chart, where the maximum number of artists are from Canada (346), followed by the USA (15). This graph should be the target of our Data Analytics process, and the result after all the four steps should match this graph.

### Figure 2b
<img width="891" alt="Screenshot 2024-12-05 at 5 07 07 PM" src="https://github.com/user-attachments/assets/c31be3c2-db3e-4f0d-bd8a-a53b008d4d09">

**Column Chart showing the total number of artists from each country.**

---

## Data Storage

Based on my dataset, to store the data, three buckets were created:
1. `pa-artist-raw-jat`
2. `pa-artist-trf-jat`
3. `pa-artist-cur-jat`

### Figure 2c
<img width="799" alt="Screenshot 2024-12-05 at 5 07 15 PM" src="https://github.com/user-attachments/assets/b9810e4c-9588-47a6-807e-b4f0016df485">

**Creation of three buckets**

---

## Draw.io Representation
### Figure 2d
<img width="812" alt="Screenshot 2024-12-05 at 5 07 21 PM" src="https://github.com/user-attachments/assets/068e8ddc-41d7-427b-acef-ad9618cb91a0">

**Data Analytics Platform (DAP) using draw.io for 1st Pipeline**

The AWS services used in developing this DAP were Amazon S3, AWS Glue DataBrew, and AWS Glue. The figure above illustrates the implementation of different buckets and processes. In this setup, data is initially ingested into a raw bucket on AWS. It then undergoes processing via DataBrew, where profiling and cleaning tasks are completed. The processed output is stored in a transformed (`trf`) bucket. Subsequently, an ETL (Extract, Transform, Load) pipeline utilizes this data to produce final results that are saved in a curated bucket with two folders—`system` and `user`—for use according to specific requirements.

### Figure 2e
<img width="605" alt="Screenshot 2024-12-05 at 5 07 28 PM" src="https://github.com/user-attachments/assets/ac8cedb6-7298-4318-bde5-5288ed366bd0">

**draw.io for the 1st pipeline**

---

## Step 1: Data Ingestion

The first step of designing any DAP is to fetch the structured dataset from the source. Data can be uploaded into the raw bucket either in Excel or CSV format; however, as per our requirements, Excel is more suitable.

### Figure 2f
<img width="995" alt="Screenshot 2024-12-05 at 5 07 35 PM" src="https://github.com/user-attachments/assets/2ae82bb7-3c14-4891-9f55-11b88f35ebf3">

**Uploading Excel file into the raw bucket**

---

## Step 2: Data Profiling

The next step after feeding the data is Data Profiling, which is done using the AWS ‘Glue DataBrew’ service. It assesses the quality of data ingested and makes changes as per the requirement.

### Figure 2g
<img width="988" alt="Screenshot 2024-12-05 at 5 07 42 PM" src="https://github.com/user-attachments/assets/7f33f12c-6fbe-4130-8a15-64714b609503">

**Result of Data Profiling**

First, a dataset is created to establish the connection between the two services. Then, the profiling process is run by creating projects and recipe jobs.

### Figure 2h
<img width="924" alt="Screenshot 2024-12-05 at 5 07 48 PM" src="https://github.com/user-attachments/assets/15cbdf10-7f61-4023-88ac-d49543bef910">

**Recipe Jobs**

---

## Step 3: Data Cleaning

In this process, data is prepared for analysis by undergoing a cleaning procedure. This involves managing missing data, eliminating duplicates, and addressing formatting issues. My specific dataset had a lot of `null` values in the `Country` column and a few extra columns unnecessary for achieving the desired results. The null values were replaced with `No country`. The clean data is then stored in the `data-cleaning` folder within the `trf` bucket.

### Figure 2i
<img width="950" alt="Screenshot 2024-12-05 at 5 07 53 PM" src="https://github.com/user-attachments/assets/d5d2846d-f661-42ba-8915-1e07752534cd">

**Storing the clean data in S3**

---

## Step 4: Data Pipeline Design

A pipeline is utilized to perform ETL (Extract, Transform, Load) operations on the transformed data from Steps 2 and 3. The result of this process is referred to as analytical data. In our case, the initial step involves retrieving the cleaned data from the transform bucket and starting the elimination of unnecessary columns. Post this, the count function is applied to calculate the total number of artists by grouping them country-wise. This information is stored in two folders created in the curated bucket—one for the system and another for the user.

### Figure 2j
<img width="983" alt="Screenshot 2024-12-05 at 5 08 01 PM" src="https://github.com/user-attachments/assets/01e5759f-b59e-4b49-8d0b-6d2abf9d0080">

**1st ETL Pipeline**

### Figure 2k
<img width="1014" alt="Screenshot 2024-12-05 at 5 08 08 PM" src="https://github.com/user-attachments/assets/e9ede00d-d66a-4ee3-bd60-4b4c5e9b05a6">

**Final Result**

---

## Exploratory Analysis

Due to the limitations in the dataset, there wasn’t much scope for exploratory analysis. However, applying creativity, I extracted the list of artists and their details from the continent ‘North America’, including Canada and the USA. This analysis evaluates the quality of the dataset while also shedding light on broader implications regarding how artists and their contributions are valued and preserved worldwide.

---

## Draw.io Representation
A new pipeline is created in the DAP platform for this purpose.

### Figure 2l
<img width="487" alt="Screenshot 2024-12-05 at 5 08 14 PM" src="https://github.com/user-attachments/assets/cf2c4ab9-2e89-4fbb-8d91-ccfb297f3766">

**Data Analytics Platform (DAP) using draw.io for 2nd pipeline**

### Figure 2m
<img width="936" alt="Screenshot 2024-12-05 at 5 08 22 PM" src="https://github.com/user-attachments/assets/7a8636bf-020a-4e87-b8a8-eec3e0a54959">

**draw.io for the 2nd Pipeline**

---

## Step 1: Data Ingestion

Since I’m using the same data source, this step is the same as in ‘Descriptive Analysis’.

---

## Step 2: Data Profiling

AWS Glue DataBrew performs data profiling to assess data quality and saves the results in the transformed S3 bucket.

### Figure 2n
<img width="926" alt="Screenshot 2024-12-05 at 5 08 30 PM" src="https://github.com/user-attachments/assets/8778e004-11d8-436c-ab7f-8aa5949c07da">

**Data Profiling Success**

---

## Step 3: Data Cleaning

Since the data was already cleaned in the ‘Descriptive Analysis’, there was no need to clean it again.

---

## Step 4: Data Pipeline Design

For exploratory analysis, instead of using `Aggregate` in the ETL pipeline, I used the `Filter` option and matched the results based on the value `Canada` OR `USA`. This gave all the artists from ‘North America’.

### Figure 2o
<img width="897" alt="Screenshot 2024-12-05 at 5 08 37 PM" src="https://github.com/user-attachments/assets/e617d18f-c2bf-49a3-b95f-bfb37f53efaa">

**2nd ETL Pipeline**

### Figure 2p
<img width="949" alt="Screenshot 2024-12-05 at 5 08 44 PM" src="https://github.com/user-attachments/assets/1bebde86-41e5-4b47-b8a8-d04997c2da65">
<img width="699" alt="Screenshot 2024-12-05 at 5 08 53 PM" src="https://github.com/user-attachments/assets/9fdf7514-ff3d-424e-b30d-be2b118b1f5c">
**Final Result**

### Conclusion

The implementation of a Data Analytics Platform (DAP) for the ‘Public Art – Artists’ dataset illustrates the power of cloud-based tools in transforming raw data into actionable insights. Through a step-by-step process encompassing data ingestion, profiling, cleaning, and pipeline design, this project achieved its primary goals of identifying the country-wise distribution of artists and analyzing North American contributions. The use of AWS services streamlined the data lifecycle, from ingestion in S3 buckets to processing via Glue DataBrew and final transformation using ETL pipelines. These findings emphasize the importance of robust data management practices in uncovering trends and supporting informed decision-making. This project not only highlights the technical capabilities of AWS but also showcases the broader implications of data analytics in understanding cultural and artistic contributions. Future projects can build on this foundation to explore more complex datasets and incorporate advanced analytics techniques.



---

For more information, visit my [LinkedIn profile](https://www.linkedin.com/in/jatin-girdhar-49b035143).

![image](https://github.com/user-attachments/assets/26c2081b-d45f-4a5b-a14a-f728d1e3d8be)

