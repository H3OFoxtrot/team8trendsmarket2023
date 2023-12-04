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

[![food-log-example.png](https://i.postimg.cc/bwKmfs8L/food-log-example.png)](https://postimg.cc/bZ9xQYZ2)

This shows the template for how the file should be formatted. If this is made in excel, don't forget to convert to csv before uploading to storage!

More details as to how to collect device data can be found at the following links:

https://support.empatica.com/hc/en-us/articles/201608896-Data-export-and-formatting-from-E4-connect-

https://www.dexcom.com/en-us/faqs/can-i-export-raw-data

Once you have all 8 files (ACC, BVP, EDA, IBI, TEMP, HR, FoodLog and Dexcom) for each patient, then you are ready to move on to the next step.


2. Set up and configure Azure Blob Storage

A basic guide on setting up and using Azure Blob Storage can be found here:
https://learn.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal

Here I will outline some important points.

First: After logging into Azure, we first need to create a new storage account.

[![blob-sc1.png](https://i.postimg.cc/bN5T1sG8/blob-sc1.png)](https://postimg.cc/8jhMSkBn)

[![blob-sc2.png](https://i.postimg.cc/mk5Q35gV/blob-sc2.png)](https://postimg.cc/JHjDMKJB)

We do this by clicking on storage accounts, then on the Create button.

Here is where we create the new storage account. There are many different settings here, most of which can be left as the default.

However, it is critically important that you select both the correct subscription and resource group.

This will ensure that the various steps of your pipeline can communicate with the data storage properly.

More details on how to create a storage account can be found here:
https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal

[![blob-sc3.png](https://i.postimg.cc/PxfZgjL2/blob-sc3.png)](https://postimg.cc/R38Nt2LH)

Now that we have our storage account, we need to make a new container. We do this by clicking on storage accounts > your created storage account > containers (on the left bar under Data storage) > + container (right above the container search bar).

This container will be named "patientdata". You could choose to name it something else, but this may lead to compatability issues with the databricks code, and thus require modification within the code. Keep the default access level setting and click create.

Looking inside the new container you shouldn't see anything there. This is where the patient files will be uploaded. When you are ready, click the Upload button, select all of your patient files and click Upload.

It will take some time, but eventually all of the files will upload to the blob storage. A progress notification will appear at the top right of the screen under the notifications (bell) icon if you want to check in later.


3. Set up and configure Azure Databricks
   

After the sotrage of data in Azure Blob Storage, we make use of Azure Databricks to generate features feeding the model.
We should setup Databricks account firstly, and here is the link to databricks https://community.cloud.databricks.com/.

After login, we need to build a new cluster and start a notebook.

Following pic shows where to build a new cluster and notebook.

<img width="454" alt="image" src="https://github.com/H3OFoxtrot/team8trendsmarket2023/assets/145874767/b4b5f50e-7c46-4d09-8561-5fcc8cd15655">


<img width="1392" alt="image" src="https://github.com/H3OFoxtrot/team8trendsmarket2023/assets/145874767/6e7eea78-0d55-472c-8c84-a1d81dc08454">



Then we take following steps to generate the features file.


Step1: input the storage_account_name, storage_account_key, and container to gain the access to Azure Blob Storage

storage_account_name = "tmfall2023pa******"

storage_account_key = "b9CrNE7Gq8QiiqC6YX9c2F09********"

container = "pati*******"



Step2: Import the packages we need in the process of feature engineering such as StructType,StructField,Window,and pandas

Specific coding could be found in the features_engineering. file.



Step3: Read data from Azure Blob Storage and start feature engineering.

There are data from 16 patients and each one have 8 category of original features, ACC, EDA, HRV, Food_log, Dexcom, Temp, HR, and IBI. 

Each of the data are distributed, and stored in one file in Azure Blob Storage. The output should be a table with columns PatientId, Gender,

ACC_mean, ACC_max, etc.

The process of building features and merging is: 

read ACC file from Azure Blob Storage for patient1 --> build ACC related features for patient1 --> read ACC file from Azure Blob Storage for patient1 
--> .........  --> merge the features for patient1

↓
↓

read ACC file from Azure Blob Storage for patient2 --> build ACC related features for patient2 --> read ACC file from Azure Blob Storage for patient2
--> .........  --> merge the features for patient2

↓
↓

.......

↓
↓

read ACC file from Azure Blob Storage for patient16 --> build ACC related features for patient16 --> read ACC file from Azure Blob Storage for patient16
--> .........  --> merge the features for patient16

↓
↓

Merge the featurs from patient1 to patient16 into one file, then write it into Azure Blob Storage.



All the features engineering coding could be found in feature_engineering.ipynb file, and we woule not introduce here again.


5. Set up and configure Azure ML Studio



6. Set up and configure PowerBI


 
7. How to feed unlabeled data into pipeline



Link to flier

Link to video

Link to dataset

Link to Articles/Sources
