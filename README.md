# Guide to Using Thellier GUI  with an example dataset

#### Step 0:  Update/download Thellier_GUI standalone and example files
- Go to EarthRef.org/PmagPy/cookbook and download the standalone (according to your Operating System). Follow the link and instructions (up to download the zip folder “pmag_GUI.4.2.39.app.zip” the folder name will change with new updates).

- Once downloaded, move it to your new working directory. Then unpack the zip file and launch the pmag_gui app (You may need to update your operating system's security settings to authorize the opening of the app)
For this example, download an example file at the following link: https://github.com/PmagPy/raw/master/data_files/Pmag_GUI/SIOfiles.zip
- Move the downloaded file to your working directory and explore the example files format: a) **thellier experiment measurement file** ( **na_sw.thel**); b) **cooling rate experiment** (**na_nw.cool**) and c) the **anisotropy correction** (**na_sw.atrm**)
 - **na_sw.thel** is SIO format and will have the following columns (a tab delimited file): specimen, treatment step (with XX.0, XXX.1, and XXX,2 being the zero field, in-field and pTRM check steps, respectively), CSD, Moment (in emu), Declination, Inclination, other info (date, temperature step, laboratory field, units…). [A handy tool on PmagPy to create a chart for your thellier experiment can be found at https://pmagpy.github.io/PmagPy_MagIC.html#chartmaker ]
 - In a text editor, open **Na_nw.cool** (same format as **na_sw.thel**) to check out the format for the **cooling rate experiment**.
 - Open **Na_sw.atrm** (same format as **na_sw.thel**) to check out the format for the **atrm experiment**. In this experiment, the decimal point after the temperature indicates a different field direction.
 - The data for this example come from https://doi.org/10.1029/2018GC007509

#### Step 1: Importing Data

- When PmagGUI is opened, it will prompt you to choose a directory. Navigate to the SIOFiles folder (or where you saved your working directory) and press **open**.

- Press the yellow button saying **1. Convert magnetometer files to MagIC format**.

- Depending on the type of data files, your lab outputs, you may need to select a different type of format from the list and it may prompt slightly different options for importing . For the example today, we will be using the SIO format. Select the **SIO format** radio button, and press **Import File**. NB: it's not possible to import multiple files at the same time, you'll need to import them one by one.

- First you need to import the measurement file for the **standard thellier experiment**. In this example, **na_sw.thel**. Under **choose file**, press the **add** button and select **na_sw.thel**.
 - For **Experiment Type**, select **Thermal (Includes thellier but not TRM)**
 - In this example, the experiment was conducted in a 40uT lab field, oriented upwards along the Z direction in specimen coordinates. In the **lab field** section, input the options **B: 40, dec: 0, inc: -90**.
 - Our specimens are named with the following convention. **XXXX-YYZ** where Z is the specimen, YY is the sample and XXX is the site (we can check this by opening our .thel file in a text editor). In the **number of terminal characters that distinguish specimen from sample** file, we put **1**. This is because we have 1 character for the specimen (a single Z).
 - In the sample site naming convention, use the dropdown menu to select **XXXX-YY**.
 - All other boxes can be left blank. You can add the **Location name** (These experiments are from the South-Western US, **Four Corners**).  Your screen should look like the following image:
 ![Alt](/figures/Thellier_Import_Settings.png "Import settings for the Thellier experiment measurement data")
 - Press OK.


- Then import the file associated with the **anisotropy correction**:
 - Select the **SIO Format** radio button again and press **Import File**.
 - Browse for the **na_sw.atrm** file.
 - Under **Experiment Type**, select  **Thermal (Includes thellier but not TRM)** and **Anisotropy Experiment**
 - Leave the lab field blank and use the same settings for naming convention and location as we did for the thellier experiment measurement file. Your settings should look like the following image:
 ![Alt](/figures/Anisotropy_Import_Settings.png "Import settings for the anisotropy experiment measurement data")
 - Press OK


- Now import the file associated with **cooling rate correction**:
 - Select the **SIO Format** radio button once again and press **Import File**
 - Browse for the **na_sw.cool** file. Under **Experiment Type**, select **Cooling Rate Experiment**. Use the same lab field as in step 6 and keep other settings the same.
 - The slow cooling of these samples were cooled at **43.6, 1.3, 43.6 K/min**. Type these values into the K/min box and press OK. Your settings should look like the following:
![Alt](/figures/Cooling_rate_Import_Settings.png "Import settings for the anisotropy experiment measurement data")
 - Press OK


- After importing ALL desired files, Press **go to next step**

- This step Thellier_GUI combines all 3 format files into a single file for measurements. All 3 files (measurements, atrm, cooling rate) should be present here. If not, press **add file** and find them. Press **OK** to combine these files.

- The next window combines different specimens, sites and samples files together. At the moment, we don't want to do this because we need to add some additional information (see Step 3 of this tutorial), so we just press **OK**. In case you only have one or more measurement files without cooling rate or atrm, you can press **OK** and you can skip to Step 3 of this tutorial.

#### Step 1.1: Adding Information to MagIC tables
- Before we can analyze the data in Thellier GUI with the cooling rate, we need to add the original cooling rate of the samples to the data. These data were cooled originally at 6.2e11 K / Ma.

- Press the yellow button marked **3. (optional) Add MagIC metadata for uploading data to MagIC**.

- We want to add the cooling rate to the original samples.txt. In the box marked **samples_optional**, scroll until you find the **cooling_rate** option. Select this and press the **Add** button. Then press **OK**.
- The first screen that comes up allows us to edit our specimen table. We only want to edit the samples, so press **Save and Continue** and **Yes** to all warning messages.
- We are now at the samples table. Press on the top of the **cooling_rate** column in the table to edit all the cells, and type 6.2e11 to set the original cooling rate in K/Ma. Press **Save and Continue**.
- At the site table, set the **lat** column to 35 and the **lon** column to 254 (please note that only positive values are accepted for longitude) to set the (approximate) latitudes and longitudes of these sites.
- The other tables allow you to add age information, types of locations etc. These are unnecessary to add now, but they are useful to produce a file that can be uploaded to the MagIC database (https://www2.earthref.org/MagIC ), described in Step 6 of this tutorial. Press save and continue until you get back to the main screen of the pmag_gui program.

#### Step 2: Setting up Thellier_GUI
- Now that we have our data transformed into Pmag_GUI readable files, we can launch the Thellier_GUI program. This program displays a dropdown menu with all your specimens and their treatment steps below, Arai plots of the data, along with Zijderveld, Equal area, the M/T plot, the site level statistic live results. Thellier_GUI allows you to interpret your data (Step 3 of this tutorial) and export figures and results (Step 4 of this tutorial).

![Alt](/figures/Thellier_GUI.png "Image of the Thellier GUI Program")

- To calculate the anisotropy tensors for each specimen, click on the **Anisotropy** tab at the top of the screen and press **Calculate Anisotropy Tensors**.

- To switch between specimens, use the dropdown box by the specimen name or press the **previous**/**next** buttons
- The paleointensity statistics associated with a particular interpretation are displayed at the bottom of the screen. These statistics can be changed by pressing the **Preferences** tab at the top of the screen and pressing **specimen paleointensity statistics**. This will cause your program to restart. For more information about paleointensity statistics, see https://earthref.org/PmagPy/SPD/spdweb.html
- For our example, we are going to use the following statistics: **int_n, frac, b_beta, scat, gmax, int_mad, int_dang, k_prime**.
![Alt](/figures/Paleointensity_statistics.png "Acceptance Criteria for these specimens")


- We can also set threshold values for these statistics as criteria to select our data. We do this by going to the **Analysis** tab and going to **Acceptance criteria > Change acceptance criteria**. (your changed criteria will get saved into a **criteria.txt** file into your working directory). We will set the following criteria for our data:
![Alt](/figures/Acceptance_Criteria.png "Acceptance Criteria for these specimens")


#### Step 3: Analyzing and Interpreting data Manually
- To select an interpretation, in the temperatures section, select **start (lower T) and end (higher T) temperatures** using the two drop down boxes and Thellier_GUI will show you all criteria which your specimen passed in GREEN and all that failed in RED. Click on **Save** to save your current interpretation. If 2 or more specimens per site are successful they will appear in the plot for site data.

![Alt](/figures/Interpretation.png "Example of a successful interpretation")

- Once you have gone through analyzing ALL your specimens you can skip to Step 5 of this tutorial.

#### Step 3.1: Analyzing Data with Auto Interpreter
- The Thellier Auto interpreter is a tool that automatically searches for interpretations that conform to our criteria, and selects the set of interpretations that minimizes the standard deviation at a site level.

- Click on **Auto Interpreter>Run Thellier Auto Interpreter** from the toolbar and wait (it may take several minutes). This option will use the criteria you have set in step 3.6 and 3.7
- Once finished, you can view the results, selecting on the toolbar **Auto Interpreter>Open auto-interpreter output files** or simply by clicking through the specimens.

#### Step 4: Saving and Exporting Interpretations
- On the toolbar, select Analysis> **Save Current Interpretations to a redo file**. This will save a Thellier_redo.txt file which you can open next time you launch the program, and click OK for saving all calculations (into a specimen, samples and sites tables)

- You can also save each individual plot by selecting **File>save plot** on the toolbar.
- To save data into the MagIC format go to the toolbar and select **File > Save Magic Tables**. This will go through several messages for the specimens/samples/sites tables. Press **OK** for each.
