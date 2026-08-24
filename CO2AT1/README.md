# Academic Profile
* **Name:** L Nihas Goud
* **Register Number:** 192472346
* **Course Code & Slot:** CSA15 - Slot B
* **Faculty Name:** Dr. C. Rajesh Babu

---

## 🚀 Capstone Project: SkillHire (Cloud-Native NLP Skill-Gap Analysis Platform)

### 🎯 Overview
SkillHire is a cloud-native NLP platform that accepts candidate resume PDFs and job descriptions, extracts SKILL entities using spaCy Named Entity Recognition (NER), computes a skill gap score, and delivers ranked learning recommendations via a React dashboard.

---

## ☁️ CO2 AT1: Capstone Infrastructure Sizing Workbook Summary

### 📋 Sizing & Architecture Specifications
* **Capstone Title:** SkillHire — Cloud-Native NLP Skill-Gap Platform
* **Target Workload:** Hybrid (API Backend + AI/Python NLP Inference Module + Managed Database/Storage)
* **Prototype VM Sizing:** AWS EC2 `t3.xlarge` (4 vCPU, 16 GB RAM, 100 GB EBS gp3 SSD) running Ubuntu 22.04 LTS[cite: 4]
* **Pilot / Production Migration:** API Layer on `t3.medium` (2 vCPU, 4 GB RAM); NLP Inference offloaded to AWS Lambda (3 GB RAM, Docker ECR image)[cite: 4]
* **Storage Strategy:** 100 GB EBS SSD for OS & application dependencies; resume PDFs & exported reports offloaded to Amazon S3 (private bucket, SSE-S3 encryption, 90-day lifecycle rule)[cite: 4]
* **Database & Auth Tier:** Amazon DynamoDB (`SkillHireMatches` table with Streams enabled) + AWS Cognito for OAuth 2.0 JWT authentication[cite: 4]
* **Virtualization Approach:** Type 2 (VirtualBox) for local dev testing; AWS Nitro Hypervisor (Type 1) & AWS Firecracker microVM for serverless Lambda execution[cite: 4]

### 📄 Final Infrastructure Recommendation
1. **VM Sizing:** The SkillHire prototype runs on a single AWS EC2 `t3.xlarge` instance (4 vCPU, 16 GB RAM, 100 GB EBS gp3 SSD)[cite: 4]. This is justified by a CPU score of 10 (driven by the spaCy NLP module at +3 and analytics at +2) and a RAM footprint of 13.75 GB (rounded to 16 GB) dominated by in-process spaCy model loading (6 GB)[cite: 4]. Disk space covers OS (40 GB), prototype local DB (10 GB), logs (5 GB), and a 30% safety buffer (16.5 GB)[cite: 4].
2. **Hypervisor & Virtualization:** Local development uses VirtualBox (Type 2)[cite: 4]. Cloud production utilizes AWS Nitro Hypervisor (Type 1) for EC2 instances and AWS Firecracker microVMs for Lambda containers[cite: 4].
3. **Containerization:** The spaCy NLP engine is packaged as a Docker container image (Python 3.11, `spaCy en_core_web_lg`, `pdfplumber`) stored in AWS ECR and executed on AWS Lambda with 3 GB RAM per invocation[cite: 4]. In production, the REST API migrates to Docker containers on ECS Fargate[cite: 4].
4. **Storage Plan:** VM disk (100 GB) covers OS/app files only[cite: 4]. PDF resumes and gap reports are offloaded directly to Amazon S3 via pre-signed URLs[cite: 4]. Structured match records sit in DynamoDB[cite: 4].
5. **Snapshot & Clone Strategy:** EBS snapshots are taken prior to deployments, schema changes, and OS upgrades (3–7 day retention)[cite: 4]. DynamoDB Point-In-Time Recovery (PITR) is continuously enabled (35-day window)[cite: 4]. VM clones are created for developer staging environments at sprint start and discarded post-sprint[cite: 4].
6. **Compute Split:** Frontend on AWS Amplify + CloudFront CDN; Backend API on EC2/ECS Fargate; NLP Engine on containerized AWS Lambda; Database & Storage on managed DynamoDB and S3[cite: 4].

---

## ✈️ Previous Guided Projects

### Project 01: SaaS-Based Flight Ticket Reservation System
* **Objective:** Built a multi-tenant cloud aviation database application with relational lookups, reporting views, and operational KPI dashboards on Zoho Creator[cite: 1].
* **Artifact:** `flight_reservation_dashboard.png`

### Project 02: Chennai Property SaaS
* **Objective:** Built a property management system tracking local real estate with dynamic form rules and role-based data containers[cite: 2].
* **Artifact:** `chennai_property_dashboard.png`
