# GIS Vulnerability & Risk Assessment Course — Setup Guide

This guide walks you through two ways to run the course notebooks: **Google Colab** (recommended) and **local Jupyter Notebook**. Pick whichever works best for you.

---

## Option A: Google Colab (Recommended)

Google Colab is a free, browser-based notebook environment from Google. Nothing to install on your computer — it runs entirely in your web browser. This is the setup the notebooks were designed for.

### What You Need

- A Google account (any Gmail or university Google account works)
- A modern web browser (Chrome, Firefox, Edge, Safari)
- The 9 `.ipynb` notebook files from this course

### Step-by-Step Setup

**1. Upload the notebooks to your Google Drive**

- Go to [drive.google.com](https://drive.google.com)
- Create a new folder called `MSER_510_VULNERABILTY` (spelling must match exactly)
- Inside that folder, create a subfolder called `notebooks`
- Upload all 9 `.ipynb` files into the `notebooks` folder

Your Drive should look like this:

```
My Drive/
  MSER_510_VULNERABILTY/
    notebooks/
      Class_0_Data_Setup.ipynb
      Class_1_Exposure.ipynb
      Class_2_Potential_Impact.ipynb
      Class_3_Adaptive_Capacity.ipynb
      Class_4_Vulnerability.ipynb
      Class_5_Probability.ipynb
      Class_6_Consequence.ipynb
      Class_7_Risk.ipynb
      Class_8_Combined_Score.ipynb
```

The `data/` and `outputs/` folders will be created automatically when you run Class 0.

**2. Open a notebook in Colab**

- In Google Drive, double-click any `.ipynb` file
- If it doesn't open in Colab automatically, right-click the file, choose **Open with**, then select **Google Colaboratory**
- If you don't see Google Colaboratory as an option, click **Connect more apps** and search for "Colaboratory", then install it

**3. Run the notebook**

- Start with `Class_0_Data_Setup.ipynb` — always run this one first
- Click the **Play** button on the left side of each code cell to run it, or use the keyboard shortcut **Shift + Enter**
- Run cells from top to bottom, in order
- The very first cell will ask you to authorize Google Drive access — click **Allow** when prompted

**4. Continue with Classes 1 through 8**

- After Class 0 finishes, open each subsequent notebook in order (Class 1, then 2, then 3, etc.)
- Each notebook picks up where the last one left off by reading the GeoPackage file that Class 0 created in your Drive

### Tips for Colab

- **If Colab disconnects:** This happens after about 90 minutes of inactivity. Just reconnect and re-run the cells from the top. Your data is safe in Google Drive.
- **"Run all" shortcut:** Go to **Runtime > Run all** to run every cell in the notebook at once. Useful when re-running a notebook you've already completed.
- **Runtime type:** The default runtime (Python 3, no GPU) is all you need. No special hardware required.
- **Free tier is fine:** You do not need Colab Pro for this course.

---

## Option B: Local Jupyter Notebook

If you prefer to work on your own computer instead of in the cloud, you can run the notebooks locally using Jupyter Notebook or JupyterLab.

### What You Need

- Python 3.9 or newer installed on your computer
- About 2 GB of free disk space (for data downloads)
- An internet connection (for downloading data in Class 0)

### Step-by-Step Setup

**1. Install Python (if you don't have it)**

The easiest way is to install Anaconda, which comes with Python, Jupyter, and many scientific libraries pre-installed.

- Go to [anaconda.com/download](https://www.anaconda.com/download)
- Download the installer for your operating system (Windows, Mac, or Linux)
- Run the installer and follow the prompts (accept all defaults)

If you already have Python installed, you can skip this step.

**2. Install the required libraries**

Open a terminal (Mac/Linux) or Anaconda Prompt (Windows) and run:

```
pip install geopandas fiona shapely pyproj requests duckdb folium seaborn matplotlib pandas numpy
```

If you're using Anaconda, you can also use conda:

```
conda install -c conda-forge geopandas fiona shapely pyproj requests duckdb folium seaborn matplotlib pandas numpy
```

**3. Create your course folder**

Create a folder on your computer for the course. For example:

- **Windows:** `C:\Users\YourName\Documents\MSER_510_VULNERABILTY`
- **Mac/Linux:** `/Users/YourName/Documents/MSER_510_VULNERABILTY`

Inside that folder, create two subfolders: `data` and `outputs`. Then place the 9 notebook files there:

```
MSER_510_VULNERABILTY/
  data/
  outputs/
  Class_0_Data_Setup.ipynb
  Class_1_Exposure.ipynb
  Class_2_Potential_Impact.ipynb
  ... (all 9 notebooks)
```

**4. Make a small edit to each notebook**

The notebooks are written for Google Colab, so two small changes are needed for local use.

**Change 1 — Skip the Google Drive cell.** Each notebook has a cell near the top that looks like this:

```python
from google.colab import drive
drive.mount('/content/drive')
```

**Do not run this cell locally.** It will cause an error because `google.colab` only exists in Colab. Just skip it (or delete it).

**Change 2 — Update the file path.** Each notebook sets a `BASE_DIR` variable that points to your Google Drive. You need to change it to your local folder path instead.

Find the cell that says:

```python
BASE_DIR = '/content/drive/MyDrive/MSER_510_VULNERABILTY'
```

Change it to your local path:

- **Windows:**
  ```python
  BASE_DIR = r'C:\Users\YourName\Documents\MSER_510_VULNERABILTY'
  ```
  (The `r` before the quote tells Python to treat backslashes as regular characters.)

- **Mac/Linux:**
  ```python
  BASE_DIR = '/Users/YourName/Documents/MSER_510_VULNERABILTY'
  ```

Make this same change in **all 9 notebooks**.

**5. Launch Jupyter Notebook**

Open a terminal (Mac/Linux) or Anaconda Prompt (Windows) and run:

```
jupyter notebook
```

This opens Jupyter in your web browser. Navigate to your course folder and open `Class_0_Data_Setup.ipynb`.

Alternatively, if you prefer JupyterLab (a newer interface):

```
jupyter lab
```

**6. Run the notebooks**

- Start with Class 0, then work through 1 to 8 in order
- Click inside a cell and press **Shift + Enter** to run it
- Run cells from top to bottom

### Tips for Local Jupyter

- **Skip the `!pip install` cells.** Since you already installed libraries in Step 2, you can skip the cells that start with `!pip install`. Running them again won't hurt anything, though — they'll just confirm everything is already installed.
- **If you get an import error:** It usually means a library wasn't installed. Go back to your terminal and run `pip install <library-name>`.
- **Your data persists automatically.** Unlike Colab, local files don't disappear between sessions. You can close Jupyter and come back later — your data will still be in the `data/` folder.

---

## Working with the Output Data in Desktop GIS

One of the big advantages of this course is that the GeoPackage files created by the notebooks can be opened directly in QGIS or ArcGIS Pro.

### Opening the GeoPackage in QGIS

1. Open QGIS
2. Go to **Layer > Add Layer > Add Vector Layer**
3. Click the **...** button next to Source and navigate to your `data/` folder
4. Select `vulnerability_risk_data.gpkg`
5. QGIS will ask which layers to add — select the ones you want (parcels, flood_zones, buildings, study_area)
6. Click **Add**

Or simply drag and drop the `.gpkg` file from your file explorer into the QGIS map window.

### Opening the GeoPackage in ArcGIS Pro

1. Open ArcGIS Pro and create or open a project
2. In the **Catalog** pane, right-click **Databases**
3. Click **Add Database**
4. Navigate to your `data/` folder and select `vulnerability_risk_data.gpkg`
5. Expand the database in the Catalog pane to see the layers
6. Drag any layer onto your map

### Syncing Between Colab and Desktop GIS

If you're using Google Colab and want to open the same data in QGIS or ArcGIS Pro on your computer:

1. Install **Google Drive for Desktop** from [google.com/drive/download](https://www.google.com/drive/download/)
2. Sign in with the same Google account you use for Colab
3. Your Drive files will appear as a folder on your computer
4. Navigate to `Google Drive/My Drive/MSER_510_VULNERABILTY/data/`
5. Open the GeoPackage from there in QGIS or ArcGIS Pro

Any updates you make in Colab will sync automatically to your desktop.

---

## Course Notebook Order

Always run the notebooks in this order:

| Order | Notebook | What It Does |
|-------|----------|--------------|
| 1st | Class 0 — Data Setup | Downloads all data and creates the GeoPackage |
| 2nd | Class 1 — Exposure | Identifies which parcels are in the flood zone |
| 3rd | Class 2 — Potential Impact | Scores how badly each parcel could be affected |
| 4th | Class 3 — Adaptive Capacity | Scores how well-prepared each building is |
| 5th | Class 4 — Vulnerability | Combines impact and capacity into a vulnerability score |
| 6th | Class 5 — Probability | Scores how likely flooding is at each location |
| 7th | Class 6 — Consequence | Scores how severe the financial impact would be |
| 8th | Class 7 — Risk | Combines probability and consequence into a risk score |
| 9th | Class 8 — Combined Score | Brings vulnerability and risk together into a final score |

Each notebook builds on the one before it. If you skip ahead, the data fields from earlier classes won't exist yet and you'll get errors.

---

## Troubleshooting

**"ModuleNotFoundError: No module named 'geopandas'"**
The library isn't installed. Run `pip install geopandas` in your terminal (local) or `!pip install geopandas` in a Colab cell.

**"No such file or directory" when loading the GeoPackage**
Class 0 hasn't been run yet, or the `BASE_DIR` path is wrong. Double-check your folder path and make sure you ran Class 0 first.

**"google.colab module not found" (local Jupyter only)**
You're running locally and hit the Google Drive mount cell. Skip that cell — it only works in Colab.

**Colab disconnected and my variables are gone**
Colab resets when it disconnects, but your data is safe in Google Drive. Re-run the notebook from the top — it will reload the data from the GeoPackage.

**The map doesn't show up in the notebook**
Try running the cell again. If using local Jupyter, make sure `matplotlib` is installed. For interactive maps (folium), they should display automatically in both Colab and Jupyter.

**"CRS mismatch" or coordinate system warnings**
The notebooks handle coordinate system alignment automatically. If you see a warning, it's usually safe to ignore. If you get an actual error, make sure you ran the earlier notebooks in order — they set up the coordinate systems.
