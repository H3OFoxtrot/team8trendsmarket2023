# team8trendsmarket2023
Trends Marketplace 2023 project for team 8: Predicting Interstitial Glucose using Wearable Devices (i.e. Smartwatches)

Note: This project repository is created in partial fulfillment of the requirements for the Big Data Analytics course offered by the Master of Science in Business Analytics program at the Carlson School of Management, University of Minnesota.

Introduction/Executive Summary:

Installation Instructions:

0. Collect your data

Collecting your data will vary depending on what type of device or devices you are utilizing.
For this process it is strongly recommended that data only be used from a single type of wearable device (both for glucose sensor and for smartwatch).
For best results we recommend using the Dexcom G6 brand sensor/transmitter and the E4 wrist sensor.
For each patient there should be six different file types exported: ACC, BVP, EDA, IBI, TEMP, and HR. These will all be in .csv format.
Each batch of patient files MUST be labeled with their patient number at the end of the file name in the following format: "ACC_001.csv".
If there is a large number of patients, a simple python script could be used to assist in renaming the files.

If you are adding your own training data, then you will also need to collect both Dexcom sensor data, as well as food logs from each patient.
The Dexcom data should come ready to use. You may need to rename the file to the correct format, which is "Dexcom_001.csv".
The food logs, however, will need to be collected manually.

The food logs will need to be manually entered into a file in the following format: "Food_Log_001.csv". The columns will be in the following format:

date	time	time_begin	time_end	logged_food	amount	unit	searched_food	calorie	total_carb	dietary_fiber	sugar	protein	total_fat

2/13/2020	18:00:00	2/13/2020 18:00		Berry Smoothie	20	fluid ounce	Strawberry Smoothie	456	85	1.7	83	16	3.3

This shows the template for how the file should be formatted. If this is made in excel, don't forget to convert to csv before uploading to storage!

More details as to how to collect device data can be found at the following links:

https://support.empatica.com/hc/en-us/articles/201608896-Data-export-and-formatting-from-E4-connect-

https://www.dexcom.com/en-us/faqs/can-i-export-raw-data

Once you have all 8 files (ACC, BVP, EDA, IBI, TEMP, HR, FoodLog and Dexcom) for each patient, then you are ready to move on to the next step.


2. Set up and configure Azure Blob Storage


3. Set up and configure Azure Databricks


5. Set up and configure Azure ML Studio


7. Set up and configure PowerBI

 
9. How to feed unlabeled data into pipeline


Link to flier

Link to video

Link to dataset

Link to Articles/Sources
