# NYC Cross-Domain Data Story: Housing Maintenance Complaints (H6) & Street Construction Permits (T3)

**The German International University (GIU) — Faculty of Informatics and Computer Science**  
**Course:** Data Engineering and Visualization (Winter Semester 2026)  
**Instructors:** Dr. Nada Sharaf | **TAs:** Mariam Ali, May Magdy, Mohamed El dagla  
**Milestone 1 Submission Deadline:** 9 November 2026  

---

## 1. Project Overview & Datasets Used

This project investigates the cross-domain relationship between **street-level construction activity** and **indoor residential maintenance complaints** across New York City boroughs and street corridors (`2022–Present`).

| Domain | Catalog ID | Dataset Name | Official NYC Open Data Link | Columns & Scale |
| :--- | :--- | :--- | :--- | :--- |
| **Housing & Development** | **H6** | Housing Maintenance Code Complaints and Problems (`ygpa-z7cr`) | [https://data.cityofnewyork.us/Housing-Development/Housing-Maintenance-Code-Complaints-and-Problems/ygpa-z7cr](https://data.cityofnewyork.us/Housing-Development/Housing-Maintenance-Code-Complaints-and-Problems/ygpa-z7cr) | **33 columns**, ~16.4M total records |
| **Transportation** | **T3** | Street Construction Permits (2022–Present) (`tqtj-sjs8`) | [https://data.cityofnewyork.us/Transportation/Street-Construction-Permits-2022-Present-/tqtj-sjs8](https://data.cityofnewyork.us/Transportation/Street-Construction-Permits-2022-Present-/tqtj-sjs8) | **39 columns**, ~3.96M total records |

---

## 2. Team Members & Individual Contributions (6-Member Team)

As required for a **6-member team**, our project delivers **12 Research Questions + 12 Interactive Visualizations** (2 per member), alongside clearly divided data engineering responsibilities:

| Member | Student Name & ID | Data Cleaning, Integration & Website Role | Assigned Research Questions & Visualizations |
| :--- | :--- | :--- | :--- |
| **Member 1** | **Takiee-Allah** (`16001345`) | Socrata SoQL API ingestion (`Listing 2`), schema inspection, and Borough/Month aggregation pipeline. | **RQ1:** Borough Volume Comparison (Grouped Bar)<br>**RQ2:** Monthly Co-Movement Timeline (Dual-Axis Line) |
| **Member 2** | **Kirolous Bassem** (`16002081`) | Pre-integration cleaning of H6 (`ygpa-z7cr`): null handling, date parsing, and street suffix standardization. | **RQ3:** Street Corridor Permits vs. Complaints (Bubble Scatter)<br>**RQ4:** Utility Excavation vs. Indoor Utility Complaints (Grouped Bar) |
| **Member 3** | **Ziad Khaled Saber Abdullah** (`17006438`) | Pre-integration cleaning of T3 (`tqtj-sjs8`): IQR outlier capping on `permitlinearfeet` & `permittotalsqfeet`. | **RQ5:** Excavation Linear Footage vs. Emergency Complaint Rate (Scatter)<br>**RQ6:** Seasonal Complaints-per-Permit Ratio (Borough × Month Heatmap) |
| **Member 4** | **Ahmed Hany** (`16004257`) | Multi-level outer integration (`borough + street_name_clean + year_month`) & Post-Integration cleaning. | **RQ7:** HPD Resolution Turnaround by Construction Intensity (Box Plot)<br>**RQ8:** Top 15 NYC High-Stress Corridors (Horizontal Bar) |
| **Member 5** | **Abdallah Ahmed Mohamed** (`16004141`) | Interactive Dash website layout (`app.py`), Dropdown filters, Search Mode parser, and `"Generate Report"` callback. | **RQ9:** Borough → Permit Series → Complaint Type Hierarchy (Sunburst)<br>**RQ10:** Complaint Closure Rate by Permit Series (Color-Scaled Bar) |
| **Member 6** | **Mohamed Ahmed** (`16008868`) | GitHub repository structure, cloud deployment on Render, README documentation, and statistical correlation analysis. | **RQ11:** Permit Duration vs. Unique Affected Buildings (2D Density Heatmap)<br>**RQ12:** Cross-Domain Multi-Metric Correlation Matrix (Annotated Heatmap) |

---

## 3. Repository Structure

```text
├── NYC_Housing_Transport_Milestone1.ipynb   # Complete Jupyter/Colab Notebook (EDA, Pre/Post Cleaning, Integration, 12 Charts)
├── app.py                                   # Interactive Dash Web Application (Dropdowns, Search Mode, Generate Report Button)
├── requirements.txt                         # Python dependencies for local execution & cloud deployment
├── Procfile                                 # Gunicorn startup command for Render / Heroku deployment
└── README.md                                # Setup steps, deployment instructions, and team contribution breakdown
```

---

## 4. Local Setup & Execution Instructions

### Step 1: Clone the Repository & Install Dependencies
```bash
git clone https://github.com/Abdel-mohymen/project.git
cd project
pip install -r requirements.txt
```

### Step 2: Run the Interactive Website Locally
```bash
python app.py
```
Open your browser at **`http://127.0.0.1:8050`** to test the dropdown filters, search mode (e.g., type `"Brooklyn 2024 plumbing"`), and the central **"Generate Report"** button.

### Step 3: Run the Jupyter Notebook
You can open `NYC_Housing_Transport_Milestone1.ipynb` directly in **VS Code**, **Jupyter Lab**, or upload it to **Google Colab** (`File -> Upload notebook`).

---

## 5. Free Cloud Deployment Instructions (Render.com)

1. Push all files (`NYC_Housing_Transport_Milestone1.ipynb`, `app.py`, `requirements.txt`, `Procfile`, `README.md`) to a public **GitHub repository**.
2. Sign in to [https://render.com](https://render.com) (using your GitHub account) and click **New +** $\rightarrow$ **Web Service**.
3. Connect your GitHub repository and configure the service:
   - **Runtime:** `Python 3`
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:server --bind 0.0.0.0:$PORT`
   - **Instance Type:** `Free`
4. Click **Create Web Service**. Within 2–3 minutes, Render will provide your live public URL (e.g., `https://nyc-h6-t3-explorer.onrender.com`).
5. Verify that all dropdowns, search queries, and the **"Generate Report"** button update the charts in real time, then send the submission email to **`ICS503Data@gmail.com`** containing:
   - All 6 team member IDs
   - GitHub repository link
   - Live deployed website link
   - Official dataset links for H6 (`ygpa-z7cr`) and T3 (`tqtj-sjs8`)
