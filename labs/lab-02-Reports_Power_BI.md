# CS 415 Database Management Systems
## Lab-01 – Import/Export - 40 Points
## Recommended Due: 20 November 2025 (Final Due: 04 December 2025 at 5 pm.)




---

## **Overview**
This lab introduces you to Microsoft Power BI using **your own dataset**.  


You will complete three beginner‑level tasks:

1. **Upload your own data into Power BI Web**  
2. **Create a Table visual and a Chart visual**  
3. **Add an interactive Slicer to filter your report**

*Power BI Web Version (app.powerbi.com)*

This lab focuses on learning the basics of **data uploading, visualizing, and filtering**.

---

# # **Task 1 – Upload Your Own Data Table**

Choose or create a small dataset with **your own topic** (books, movies, students, cars, games, recipes, etc.).

### **Requirements**
Your dataset must have:
- At least **4 columns**
- At least **10–20 rows**
- A clear **header row**
- A mix of data types:  
  - Text  
  - Number  
  - Optional date  

### **Accepted file types**
- **Excel (.xlsx)**
- **CSV UTF‑8 (.csv)**

---

## **Step‑by‑Step Instructions**

### **1. Prepare your file**
Make sure the first row contains column names.

Examples:
```
Title,Genre,Rating,Price
Dune,Sci‑Fi,9,14.99
```

---

### **2. Upload your file into Power BI Web**
1. Go to **https://app.powerbi.com**  
2. Sign in  
3. In the left menu choose:  
   **Workspaces → My workspace**  
4. In the top‑right, click:  
   **New item ▾ → Semantic model**  
5. Select **Files → Local file**  
6. Upload your Excel/CSV file

Power BI will create:
- A **Semantic model** (dataset)  
- Possibly an **auto‑generated report**

---

### **3. Create a new report**
If Power BI auto‑created a report:
- Click it → click **Edit**

If not:
1. Go to **My workspace → Semantic models**  
2. Hover over your dataset → click **…**  
3. Select **Create report**

---

### **4. Verify your fields**
On the right under **Fields**:
- Expand your table  
- Confirm each column is listed  
- Optional: verify data types (text, number, date)

---

### ✔ *Task 1 Complete When…*
- Your data is uploaded  
- A report is open in **Edit mode**  
- Your fields appear correctly in the Fields pane  

---

# # **Task 2 – Create a Table Visual and a Chart Visual**

You will now build two visuals using your dataset.

---

## **Part A – Create a Table Visual**

### **1. Insert the Table**
1. Click an empty area on the canvas  
2. In **Visualizations**, click the **Table** icon (grid symbol)

---

### **2. Add fields to the Table**
Drag **3–5 fields** from **Fields** → **Values**

For example:
- Title  
- Category  
- Price  
- Rating  
- ReleaseDate  

Resize and sort the table as needed.

---

## **Part B – Create a Chart (Choose One)**

You may create **either**:
- A **Clustered Bar Chart**  
- A **Clustered Column Chart**  
- A **Pie Chart**

---

### **Option 1 – Bar/Column Chart**
1. Click empty space  
2. Insert **Clustered bar chart** **or** **Clustered column chart**  
3. Drag a **categorical field** into **X‑axis** (or **Legend**)  
4. Drag a **numeric or key field** into **Values**

Power BI will display automatic counts.

---

### **Option 2 – Pie Chart**
1. Click empty space  
2. Insert **Pie Chart**  
3. Drag a **categorical field** into **Legend**  
4. Drag a **numeric or key field** into **Values**

---

### ✔ *Task 2 Complete When…*
Your report page contains:
- A working **Table**  
- A **Bar/Column Chart** *or* **Pie Chart**  
- Both display your own data  

---

# # **Task 3 – Add an Interactive Slicer**

A **Slicer** lets users filter visuals dynamically.

---

## **Step‑by‑Step Instructions**

### **1. Add the Slicer visual**
1. Click empty canvas space  
2. In **Visualizations**, choose the **Slicer** icon (funnel/filter symbol)

---

### **2. Choose a field for filtering**
Drag a field such as:
- Category  
- State  
- Genre  
- Rating  
- Department  
- Gender  
- Type  

into the **Field** area of the slicer.

---

### **3. Optional: Change slicer style to dropdown**
1. Select the slicer  
2. Go to **Format (slider icon)**  
3. Expand **Slicer settings**  
4. Change **Style → Dropdown**

---

### **4. Test your slicer**
Click one or more items:

- The **Table** updates  
- The **Chart** updates  
- You now have an **interactive dashboard**

---

### ✔ *Task 3 Complete When…*
Your slicer correctly filters:
- Your table  
- Your chart  

---

# # **Submission Instructions**

Share a read‑only link with Prof. Lehman (jlehman@huntington.edu)
1. Click **Share → Share report**  
2. Copy the link  
3. Submit the link in Moodle  


---

# ✔ End of Assignment
You have now learned how to:
- Upload your own data  
- Build visuals  
- Add interactivity  
- Create a simple dashboard in Power BI Web  

-- end --
