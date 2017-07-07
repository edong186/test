
# Exercise 2 - Create Resolution
[<img src="https://github.com/edong186/ml/blob/master/ml101/media/DSE2E2.png">](https://github.com/edong186/ml/blob/master/ml101/lab2/)

 In this lab we will explore how a data scientist utilizes DSX and IBM
 Bluemix cloud services to easily analyze data using machine learning
 techniques and to visualize the outcomes using DSX, R, and Brunel. For
 the lab, we have chosen two algorithms to demonstrate supervised and
 unsupervised machine learning in DSX. Decision tree-based
 classification is one of the domains that allowed scientists to have
 direct insights into the reasoning behind classification choices.
 Association rules algorithms support market basket analysis.

 The lab shows how to use these machine learning algorithms for
 uncovering the data insights in sales data.

## Overview

1.  **Source Data Repository**: **Object Storage Service**
> NOTE: This usually is the data hosted in a secure enterprise
> environment that could be securely retrieved through a network tunnel
> using the BlueMix Secure gateway. Since getting access to a data
> hosted in an enterprise infrastructure can be a compliance and privacy
> issue for this lab, we will be using sample datasets hosted in the IBM
> Object Storage that would be used as a source data set.

2.  **Exploring sales data** (for this lab, the data from IBM sample DB “GOSALES” was used):

    a.  **Using Decision Tree**: **DSX Notebooks**, **Brunel**, **R** 
    
    <img src="https://raw.githubusercontent.com/edong186/ml/master/ml101/lab2/doc/media/Decision-Tree-Lab-Flow.jpg">
    
    
    b.  **Using Association Rules**: **DSX RStudio** 
    
    <img src="https://raw.githubusercontent.com/edong186/ml/master/ml101/lab2/doc/media/Association-Rules-Lab-Flow.jpg">
    

## Lab environment setup 

1.  Download Lab-DSX-ML.zip archive from the github.com location below and extract the data file (transactions.csv) to your laptop:

    > <https://github.com/edong186/ml/tree/master/ml101/lab2/archive>
    
    Here is the content of the downloaded archive:
    
    -   Folder “data” contains the sample data “transactions.csv”
    
    -   Folder “lab” contains the following files:
    
        -   machine-learning-with-DSX-lab.ipynb – the notebook for the machine learning lab using decision trees;
        
        -   ml-lab-installation.ipynb – the notebook for installing software packages for the machine learning lab (decision trees) ;
        
        -   RStudio-apriori-demo.R – R code for the machine learning lab using association rules;
        
        -   RStudio-apriori-demo-installation.R – R code for installing software packages for the machine learning lab (association rules)


2.  A quick outline of the procedures:

    a.  Decision tree lab (based on the DSX notebooks):

        i.  Provision an Object Storage service and load a file with
            sales data (transactions.csv) for the analysis

        ii. Provision an Apache Spark service to run notebooks on

        iii. Load the sample notebooks with the
            lab (machine-learning-with-DSX-lab.ipynb) and the
            installation of the software
            packages (ml-lab-installation.ipynb) needed for the lab;

        iv. Run the code in the notebook with the installation sequence

        v.  Run the code in the notebook with the lab

    b.  Association rules lab (based on RStudio):

        i.  Start RStudio

        ii. Load the data file into RStudio (transactions.csv
            into ~/data)

        iii. Load the R-code with the lab (RStudio-apriori-demo.R) and
            the installation R-code for the software
            packages (RStudio-apriori-demo-installation.R) needed for
            the lab

        iv. Run the R-code with the installation sequence

        v.  Run the R-code with the lab

> NOTE: If the same environment is sequentially used by different users,
> then the installation procedure needs to be done once per environment
> and the user only needs to go through executing the code with the lab
> without need to spend time on the installation procedures – there is
> no need to reinstall the labs for the same environment.


> NOTE: In the instructions the sequence “Menu &gt; Submenu &gt; Final
> Item” would represent the sequence of users’ actions where they choose
> first “Menu” from the menu bar, then the “Submenu” item in the opened
> submenu list, and finally “Final Item” in the yet another opened menu
> list.


# Decision Tree

## Step 1. Adding a data asset

1. Login to DSX <http://datascience.ibm.com/>

2. Open the Default Project

2. Click "add data assets", and add "tranactions.csv" to the assets of the project.
> Note: File "tranactions.csv" is located at "Lab-DSX-ML\data"

## Step 2. Importing notebooks

1.  Click "add notebooks"

2.  On the “Create Notebook” page, switch to “From File” tab, name the notebook “Mml-lab-installation”, and choose the notebook file on your disk from the archive: ml-lab-installation.ipynb; alternatively you can switch to “From  URL” tab and use the following “Notebook URL”:
> https://github.com/edong186/ml/blob/master/ml101/lab2/labs/ml-lab-installation.ipynb

 >NOTE: you can get to this page from the home page of DSX by clicking on "Start", please choose the default pre-filled values in the fields (Project: Default project, Spark Service: the service that you provisioned for this lab)

3. Click on Create Notebook

4. Save the current state by clicking on File &gt; Save Version from the menu

5. Return back to the project overview page (or DSX home page)

6. Load the second notebook “machine-learning-with-DSX-lab” (from the file machine-learning-with-DSX-lab.ipynb, or from URL https://github.com/edong186/ml/blob/master/ml101/lab2/labs/machine-learning-with-DSX-lab.ipynb ) by following the same steps 1-5 as above

## Step 3. Inserting code

1.  From the loaded notebook “machine-learning-with-DSX-lab” click on "Find and Add data" (1001 icon): ![]

2.  The expanded "Find and add Aata" would show transactions.csv under “Files” section

3.  Identify the cell with the implementation of getObjectStorageFileWithCredentials and replace the code to use your Object Storage service:

    a.  Place your cursor to the cell with the default getObjectStorageFileWithCredentials implementation
    b.  Create an empty code cell just above the code cell with the default getObjectStorageFileWithCredentials by clicking on the following menu items: “Insert” &gt; “Insert Cell Above” and place your cursor into the new cell

    ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Replacing-the-object-storage-service-inserting-cell.jpg)

    c.  Clicking on “Insert to code” on Transactions.csv will show the options to insert the code: choose “insert R DataFrame” 

    d.  Here is a similar code that will be inserted into your new cell: ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Replacing-the-object-storage-service-the-code-inserted.jpg)

    e.  Replace the existing implementation of getObjectStorageFileWithCredentials (starts with “&lt;- function” and finishes with the end of block “}”) with the generated code in the new cell for getObjectStorageFileWithCredentials\_&lt;unique sequence&gt;; Here is the example of the highlighted code that needs to be replaced:
     ![](https://github.com/ibmdataworks/datafirst/blob/master/datascientist/machinelearning/doc/media/Replacing-the-object-storage-service-highlighted-code.jpg)

     Take the new code (highlighted with the green rectangle) and place instead of the old code (highlighted with the red rectangle):

     ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Replacing-the-object-storage-service-code-replacement.jpg)

    f.  Remove the cell with the newly generated code after replacing the default implementation of getObjectStorageFileWithCredentials

    g.  Check point: after the modifications, the section code should still define a data frame variable df which is used in the notebook; the modifications should be done only for replacing  getObjectStorageFileWithCredentials with the newly generated code for the new Object Storage service


## Step 6. Installing Software Libraries and Packages

1.  Open “ml-lab-installation” notebook in the Edit mode

2.  Execute every code section in the order in which the sections appear by clicking on the button ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Execute-section.png) or by using the menu Cell&gt; Run Cells

3.  Ensure that there are no installation failures before proceeding to the lab

>NOTE: the software packages installation may take a few minutes, but it
>needs to be done only once per account

## Step 6. Running Decision Tree Lab 

1.  Open “machine-learning-with-DSX-lab” notebook in the Edit Mode

2.  Execute every code section in the order in which the sections appear by clicking on the button ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Execute-section.png) or by using the menu Cell&gt; Run Cells. The lab covers the following actions:

    a.  Declaring the libraries used in the lab

    b.  Loading the data from the Object Storage into a data frame

    c.  Transforming the data for using with C5.0

    d.  Training the classification model (C5.0)

    e.  Transforming the classification model to visualize it in Brunel

    f.  Using a tree map for visualizing and exploring the decision tree in Brunel

    g.  Using a tree for exploring the decision tree in Brunel

    h.  Showing the native R visualization of the decision tree for comparison

3.  \[Optional step\] Clean-up the output of all sections to prepare the lab for the next user: click on Cell&gt;All Output&gt;Clear


## End of Decision Tree

# Start Association Rules

## Step 7. Association Rules Lab Installation

1. On the DSX home page, navigate to Tools > RStudio


## Step 8. Importing Source Code and Data for Machine Learning Lab in RStudio

1.  In “Files” tab use “New folder” to create 2 folders in the user’s home directory - data and demo (please do not mix it with the “File” menu item in the main menu and locate “Files” in the frame depicted here):
> ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/RStudio-Files-tab.jpg)

2.  Using “Upload” button upload transactions.csv into the data folder and RStudio-apriori-demo-installation.R, RStudio-apriori-demo.R into the demo folder


## Step 9. Installing Software Libraries and Packages

1.  Double-click on the name of the file RStudio-apriori-demo-installation.R: RStudio will open the source code:
 > ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/RStudio-Source-code.jpg)

2.  Rename ~/.Rprofile to ~/old.Rprofile: check the file .Rprofile and click "Rename", change the name to old.Rprofile
 > ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Renaming-rprofile.png)

3.  Quit the current session and start the new one:

    a. Select Session>Quit Session:
    
 > ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Session-menu.png)
 
    b. Select "Don't Save": 
    
 > ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Quitting-R-session.png)

    c. After the old session has been finished, start a new session:
    
 > ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/Starting-a-new-R-session.png)
    
4.  Run the code in RStudio-apriori-demo-installation.R using the Run button ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/RStudio-running-source-code.png): please decline the options to update any packages while installing the new packages

5.  Check point: ensure that all packages install without errors

6.  Close the source code editor window for RStudio-apriori-demo-installation.R

 >NOTE: the software packages installation may take a few minutes, but it  
 >needs to be done only once per account
7.  Rename ~/old.Rprofile back to ~/.Rprofile (see the supporting images in the item 2 above)

8.   Quit the current session and start the new one (see the supporting images in the item 3 above)

#Step 10. Running Association Rules Lab 

1.  Click on the name of the file RStudio-apriori-demo.R: RStudio will open the source code

2.  Execute every code section in the order in which the sections appear by clicking on the button ![](https://github.com/edong186/ml/blob/master/ml101/lab2/doc/media/RStudio-running-source-code.png) . The lab covers the following actions:

    a.  Declaring the libraries used in the lab

    b.  Loading the sales data into a data frame

    c.  Data wrangling with R: transforming data to the form required by arules package for Apriori algorithm

    d.  Applying Apriori algorithm

    e.  Reviewing the generated rules in the console window

    f.  Visualizing the rules with arulesViz package

3.  \[Optional step\] Quit RStudio

***End of Lab: Association Rules***