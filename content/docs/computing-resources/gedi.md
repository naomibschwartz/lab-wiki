---
title: GEDI
linktitle: GEDI
type: book
date: '2019-05-05T00:00:00+01:00'
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
summary: >
  GEDI is ...
---
## Downloading GEDI Data
### Information to know before reading this work flow: 
Anaconda is a program/package that you should use to open and run Jupyter Notebooks (python language) because it makes it very easy to download and use other packages quickly
If you get an error message when trying to follow the workflows below that has to do with loading a package, you can install packages into the environment by opening the terminal through Anaconda. Once you get to the terminal (the black box that will say something like `C:\Users\user>`) you can install the packages you need. Just look up the package name + anaconda, and then copy the conda script (something like `conda install -c anaconda h5py`) into the terminal and press enter. 

## Creating a `.netrc` file

You must have an EarthData account to access GEDI data. Just look up “EarthData login” and create an account. You can set up a .netrc file in the terminal, but the R script for the bulk download of GEDI data (which takes place later in this workflow) will also set one up for you if you haven’t got one already. This is the best method. 

This <ins>[link](https://git.earthdata.nasa.gov/projects/LPDUR/repos/daac_data_download_r/browse)</ins> instructs on how to set up a .netrc file yourself, if you need to for some reason. 

### METHOD A: Accessing Data through Jupyter Notebooks

**<ins>L4A: Above Ground Biomass Data</ins>**

_*NOTE:* Unless you are an experienced coder and are quite familiar with python, I would recommend disregarding this entire workflow and jumping down to Method B. However, it's possible that if you have more coding know-how than I do, this method could be more efficient._

1. If on the lab computer .227, open a Jupyter notebook through Anaconda "geo_env," because this environment now has all the required packages installed on it. If this computer is not available, you will need to set up and install all the packages that are listed in the top of the tutorial link below. 

2. Follow the workflow of the tutorial <ins>[here](https://github.com/ornldaac/gedi_tutorials/blob/main/1_gedi_l4a_search_download.ipynb)</ins>, using the bounding box coordinates of the region of interest.

3. Save the text file with all of the URLs, and do NOT complete the last step of the tutorial, because ‘curl’ and ‘wget’ do not seem to work in python  (if you can get it working, it would save you some steps, but running wget through R as instructed next is just the same)

4. In Rstudio, use the script found <ins>[here](https://git.earthdata.nasa.gov/projects/LPDUR/repos/daac_data_download_r/browse/DAACDataDownload.R
)</ins> to mass download the data. Comment out the first two examples and use option 3 (‘Text File containing links’). Make sure to write the path for your text file, and be very careful what you choose as your output directory. By default, the output directory will be the one that you open your R script through, so I recommend putting it in the same location as you want your data. 

**<ins>L2A: Canopy Height Metrics</ins>**

1. Again, using Jupyter through Anaconda geo_env, follow the workflow in the link below with the same bounding box coordinates as the L4A dataset

2. Save the text file, and use the same script in Rstudio as before to download the data (switching out the L4A text file path for the L2A path. 

_NOTE: Canopy Height Metrics have very high data volume, and using this method will get you the entire granule (orbit)._

### METHOD B: Earthdata Search → Recommended

**<ins>L4A and L2A</ins>**

1. Access <ins>[NASA Earthdata Search GUI](https://search.earthdata.nasa.gov/search?q=gedi)</ins>. 

2. Click on the dataset you want (L2A, L4A, etc.), and then click the square box with the line through it. 

3. Upload a .geojson file of the area of interest (note that you can create a simple polygon .geojson by using geojson.io and inputting the corners of your ROI) — alternatively, you could use a more complicated outline from Arc or some equivalent. 

4. For L2A data, you can click download all, and ensure that the custom bounding box is still selected under ‘spatial subsetting’. Click the green ‘download data’ button, and eventually you will receive notice that zip files have been created. 

5. Do not download the zip files: instead, download the .txt file with all of the URLs for the files, and in Rstudio, use this [script](https://git.earthdata.nasa.gov/projects/LPDUR/repos/daac_data_download_r/browse/DAACDataDownload.R) at this link to mass download the data. Comment out the first two examples and use option 3 (‘Text File containing links’).

6. Unfortunately, for the L4A data, the EarthData search will subset the data to the granules that intersect the bounding box, but not actually subset the data to the area within the bounding box. This means that you need to download a high volume of data and subset it with another workflow.

7. Download the L4A data using the EarthData search and R script as before (but with a new L4A .txt file).

8. Follow this [workflow](https://github.com/ornldaac/gedi_tutorials/blob/main/2_gedi_l4a_subsets.ipynb) to subset the data to the .geojson area you want. Note that you can skip the downloading process and start at step 4, because we have already downloaded the data. 4B and 4C are the main steps of interest here.

_*NOTE:* this process can take a while, even though the end product is a smaller subset of files. For me, subsetting 316 files took around 3 hours to run. I would highly recommend creating a .txt file with only some of the links (eg. 20) so that you can make sure the download works correctly and have a look at the data before commiting to downloading it all._

## Subsetting GEDI Variables
Subsetting GEDI Data to Variables of Interest and a Single File

Follow the python script attached below for both L2A and L4A data (with some variations in the script depending on which dataset you use and which variables you are interested in). If you click on the file you will get a bigger version that you can copy and paste from.

For me, because the L2A data volume was so huge, I had to move half the data from the D drive to the C drive, run the script to subset it, and then delete the data from the C drive and repeat this with the second half. Then, I merged the resultant csv’s. This is a clumsy method, because if something is missing I would have to go back and do it again. As such, if you can keep your data in one batch, I would recommend you do that. If you cannot, there is a second file attached that shows how to merge csv's and make the merged csv into a shapefile or geojson. 

Note that I also needed to delete some L2A files because they were corrupted. Hopefully you do not run into this issue, but if you do, my solution was to run only a certain subset of the files (using the [:X] method to only run up the the X'th file). So, I would run the first 10 files ([:10]) and if I didn't get an error I would run the first 20, etc... If you do get an error, go back 10 and keep adding single files (eg. [:11], [:12]) until you hit the problem file. Then, delete it and carry on. 

This is time consuming, but I only had about 10 corrupt files in 326, so do not despair!

_Subsetting and Merging CSV's is unaccessable to me atm :(_

## Rasters from Subsetted Data

In ArcGIS pro, import the shapefiles created earlier in python OR import the .csv of your data. 

Use the “Point to Raster” tool if you exported shape files. Input "rh98" or "agbd" or any other variable that you added to the table as the “value field." Note that this is the variable that will be rasterized. 

For ‘cell assignment type,’ use ‘mean.’ This means that if two shots are in exactly the same area (which is pretty uncommon), the tool will calculate the mean of the two shots for the raster 

Leave the priority field as “none” and put the cell size to `0.00022500022`. 

➡ _Why this number? This is because the units of the raster size are decimal degrees. To convert to decimal degrees, divide the desired pixel size (eg. 25 meters for my project) by 111,111 meters/degree. Ie. 25meters / 111111meters/degree = 0.000225 degrees_

Here's a <ins>[resource](https://gis.stackexchange.com/questions/295190/setting-cell-size-on-polygon-to-raster-tool-in-arcgis)</ins> that explains this a little better.

Note that if you did not export the data as a shape file from python earlier in the workflow, you can use the ‘XY table to point’ tool to create a shape file with the points, and then carry on from there using the above steps. Make sure to use the latitude and longitude for x and y coordinates, and your variable of interest as your z value. 

***Now you should have some interesting rasters to work with however you like!***
