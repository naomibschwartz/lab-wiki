---
title: Terrestrial Laser Scanner (TLS)
linktitle: Terrestrial Laser Scanner (TLS)
type: book
date: '2019-05-05T00:00:00+01:00'
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
summary: >
  The Terrestrial Laser Scanner (TLS) is used in the field to take ground LiDAR measurements - here we have some resources on how to use the TLS, and directions for its post-processing
---

***The lab has access to a Faro S350 terrestrial laser scanner. The user guide is available here.***

## Directions for scanning
1. Charge the battery (either in the scanner using the charging cable or using the portable power dock) <br>
    - Do not leave the charger in the power dock while it is not charging as this can discharge the battery
2. Set up the tripod 
    - Maximize stability by extending the legs as little as possible. Ensure tripod feet are planted firmly and are not on soft ground.
3. Attach the scanner to the tripod using the quick-release mechanism,
4. Insert the battery and SD card into the scanner.
    - Only remove the SD card and battery when the scanner is turned off
5. Turn on the scanner by pressing the power button at the top.
6. Update the compass to calibrate.
7. Ensure the inclinometer is on and the scanner is reasonably positioned.
8. Set the scanner parameters:
    - Select a predefined scanning profile (editable)
    - Set Resolution - spacing between points i.e. 1/4 = 1 point every 4 units of distance. For outdoors: 1/4
    - Set Quality - how many times a point is measured. For outdoors: 2x in ideal conditions or 4x in non-ideal conditions
    - Set Colour settings - where is the direction of the lowest light? Likely even in the outdoors.
    - HDR mode - increases colour detail
9. Hide all objects/people out of view from the scanner.

## Connecting to WIFI
1. Turn on wifi on the scanner (WLAN in settings) and on device 
2. Connect to scanner on device - LLS(serial number)
    - passcode: 0123456789
3. Open a browser on device and type in IP address
    - 192.168.43.1

## Directions for post-processing
We do not currently have a subscription to Faro SCENE, however, it is possible to request a 30-day free trial.
1. Insert SD card into computer
2. File -> New Project -> Create processing folder
3. Drag and drop all scans into folder
4. Load all scans by right-clicking on "scans"
5. Create a cluster with scans for registration (if using multi-scan method)

### Registration
- Cloud-based:
  - Right-click on cluster -> operations -> registration -> place scans -> select method
  - Change subsampling - the larger the space between points the faster it will run, but the less likely registration is to work
  - Recommended initial subsampling distance: 0.04
  - Check scan point tension - mean distance between overlapped point, or the % of overlapping points that are less than the subsampling distance apart
    - Used points - how many points from the subsample were used to match

### Exporting scans
- Set max distance to get rid of background points
- For single scans, place 0,0 point at the scanner location
- Include brightness values if needed
- Choose the format to export - las, xyz, etc. 
  - Depends on what programs you will be using after. It is generally possible to export las as xyz and vis versa in external programs.
