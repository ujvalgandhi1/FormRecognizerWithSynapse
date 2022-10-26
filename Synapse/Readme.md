This is the section for Synapse

**Step 1. Provision a Spark Pool for Form Recognizer Piece.**

I used a Small pool (4 vCores/32GB) - 3 to 10 nodes with pausing of idle time at 15 minutes**

Create a requirements.txt file on your local machine
In the requirements.txt file (open using notepad or any editor), type in the following
azure-storage-blob==12.14.0
azure-core==1.26.0
azure-ai-formrecognizer==3.2.0

![requirements.txt](https://github.com/ujvalgandhi1/FormRecognizerWithSynapse/blob/main/Synapse/Images/Spark%20Pool%20Creation.png)


Then go to the Apache Spark Pool (under Manage), then hover your mouse over the pool name and you will see three dots (...) Click that to get to the Workspace Packages
1. Make sure that the "Allow session level packages" is set to Enabled
2. Upload the requirements.txt file and click upload to upload it. It will take some time for it to apply the packages. The pool is grayed out (not operational) during this phase

![Workspace Packages](https://github.com/ujvalgandhi1/FormRecognizerWithSynapse/blob/main/Synapse/Images/Workspace%20Pacakges.png)

Once the pool is operational again, navigate to the "Develop" tab under your Synapse workspace and navigate to the Notebook section
Start a new notebook -- I have called it 1-Processing Form Recognizer Model Data
The notebook for Step 1 can be found under Synapse --> Notebooks --> 1-Processing Form Recognizer Model Data.txt
Open the notebook and copy the code and paste it in your notebook under the Synapse environemnt
Make sure the "Attach to" is the Spark Pool you have created

Make the changes to the file to reflect your settings


**Step 2 : Writing the data to a dedicated SQL Pool**
Once Step 1 is run, we need Step 2 to write the data from the ADLS Gen 2.0 account to a dedicated SQL Pool for dashboarding/further analysis
The notebook for Step 2 can be found under Synapse --> Notebooks --> 2-Loading Form Recognizer output to dedicated sql pool.txt
Open the notebook, paste it under a new notebook under your Synapse instance
Make sure that the Spark Pool is the same as one for the first notebook
Make sure to change the settings to reflect your credentials


**Step 3 (Optional). Masking PII Data**
The form itself might return back PII data - sometimes there is a need to mask and redact PII data
To leverage Synapse notebooks, we can use Presidio (https://github.com/microsoft/presidio)

For Presidio, we need workspace packages in whl format that have to be uploaded. The requirements.txt *might* not work
Create a new Spark Pool. I used a Medium One (8 vCores/64 GB) - 3 to 9 nodes with a 15 minute idle time
I uploaded the workspace packages by following the same approach as Step 1 but this time uploading the .whl files
You can find the files you need under DataAssets folder

You need to upload the following whl files
1. en_core_web_lg-3.2.0-py3-none-any.whl (Note : This whl file is too large to upload via Github, you can download the file at https://github.com/explosion/spacy-models/releases/download/en_core_web_lg-3.2.0/en_core_web_lg-3.2.0-py3-none-any.whl)
2. presidio_analyzer-2.2.29-py3-none-any.whl
3. presidio_anonymizer-2.2.29-py3-none-any.whl

This might take around 20 minutes for the pool to come back

Then open the notebook at Synapse --> Notebooks --> 3-PII Data and Masking_NewApproach.txt

Open a new notebook with the new Spark pool attached to it
Copy the 3rd file and change the settings to reflect your ADLS settings 
