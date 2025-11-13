# LAB-02 Reporting with PowerBI

Power BI Web Version (app.powerbi.com)

## Overview


## Task 1 – Upload Your Own Data Table

In this task you will upload a data table you created yourself in Excel or CSV format.

Choose a table from your database project or can use any table with 10 or more rows.

### Step-by-Step Instructions (Power BI Web)
1. Prepare your file

Save as:

Excel (.xlsx)

CSV UTF-8 (.csv)

Do not upload Google Sheets directly. Export as Excel or CSV first.

2. Upload the file

Go to https://app.powerbi.com

Sign in with your university Microsoft account

In the left menu, choose:
Workspaces → My workspace

In the top-right corner, click:
New item ▾ → Semantic model

Select Files → Local file

Browse to your Excel/CSV file and upload it

Power BI will create:

A Semantic model (dataset)

(Sometimes) an auto-generated report

3. Create a report from your dataset

If Power BI already created a report:

Click it and then click Edit (top-right)

If not:

Go to My workspace → Semantic models

Hover over your dataset → click … (More options)

Select Create report

4. Verify your fields

In the Fields pane on the right:

Expand your table

Ensure all columns loaded

Confirm data types (icons for Text, Number, Date)

✔ Task 1 is complete when:

Your file is uploaded

The dataset appears in your workspace

A report is open in Edit mode

You see your table and fields in the Fields pane




## Task 2 – Create a Table Visual and a Chart

In this task you will build two visuals from your uploaded data:

A Table

Either a Clustered Bar (or Column) Chart or a Pie Chart

## Part A – Create a Table Visual
1. Add the Table visual

Make sure you are in Edit mode

Click an empty space on the report canvas

In the Visualizations pane, click the Table icon (grid-like symbol)

A blank table appears.

2. Add fields to the Table

Drag 3–5 fields from the Fields pane (right side) into the Values area of the Table visual.

Possible examples:

Name

Category

Price

State

Rating

ReleaseDate

Resize the table so you can see all columns.

Click a column header to sort.

## Part B – Create a Chart (Choose One)

You may create either:

A Clustered Bar Chart

A Clustered Column Chart

OR a Pie Chart

### Option 1 – Clustered Bar/Column Chart
1. Add the chart

Click an empty area of the canvas

In Visualizations, choose:

Clustered bar chart (horizontal bars), or

Clustered column chart (vertical bars)

2. Add fields to the chart

Drag a categorical field into X-axis or Legend

Category

Type

State

Department

Drag a numeric or key field into Values

Power BI will default to Count, which is fine

Your chart should show bars for each category.

### Option 2 – Pie Chart
1. Add the Pie Chart

Click an empty area of the canvas

In Visualizations, click the Pie chart icon

2. Add fields to the pie chart

Drag a categorical field into Legend

Drag a numeric or key field into Values

You should now see a clean proportional pie.

## Part C – Save Your Report

Click Save (or File → Save)

Name it something like:
PowerBI_Lab_YourName

✔ Task 2 is complete when:

A Table visual appears on your report

A Bar/Column Chart OR Pie Chart appears

Both visuals use your dataset

Your report is saved successfully

Task 3 – Add an Interactive Slicer (Filter)

CS415 – Database Management Systems
Power BI Web Version (app.powerbi.com)

A Slicer is an interactive filter that lets users click or select values and dynamically update all visuals on the page.
This helps demonstrate the difference between SQL (static results) and Power BI (interactive dashboards).

## Step-by-Step Instructions
1. Make sure your report is in Edit mode

Go to app.powerbi.com

Open My workspace → Reports

Select your Power BI report

Click Edit (top-right)

2. Add a Slicer visual

Click an empty area on the report canvas

In the Visualizations pane, click the Slicer icon

It looks like a funnel/filter symbol

A blank slicer appears

3. Choose a field for the slicer

Select a field that makes sense to filter your data.
Good examples:

Category

Type

State

Gender

Department

Rating

Year (from a date field)

Add it to the slicer:

From the Fields pane, drag the column (e.g., Category or State)

Drop it into the Field area of the slicer

You should now see a list of values you can click.

4. Change slicer style (recommended)

By default, slicers display as lists.
You can switch to a dropdown to save space:

Select the slicer

In the Visualizations pane, click the Format icon (slider controls)

Expand Slicer settings

Switch Style → Dropdown

Now the slicer works like a menu.

5. Test the slicer

Click one or more values in the list/dropdown.

Your Table updates

Your Chart updates

The entire report becomes an interactive dashboard

Try selecting:

A single category

Multiple values

“Clear selections” (eraser icon in the top-right of the slicer)

## Task 3 Deliverable

After completing this task, your report page should show:

✔ A Slicer visual

✔ Your Table filtering correctly

✔ Your Chart filtering correctly

Take a screenshot of your report showing the slicer in action.

✔ Task 3 is complete when:

The slicer changes what appears in both your table and your chart

You understand how slicers create interactivity in Power BI

Your report is saved successfully
