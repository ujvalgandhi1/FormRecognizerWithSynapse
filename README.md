# How to integrate extraction of key value pairs from Form Recognizer Model with Synapse to have an end to end process

Azure Form Recognizer is an excellent resource for setting up a GUI driven process to load test forms, develop the model and then test the model with 1-3 forms. The issue though is doing the work at "industrial scale" where you want to call the endpoint. 

There are a lot of articles around using the Form Recognizer endpoint but most don't extract the key-value pairs in a csv format which most data analysts prefer for end analysis. The default code supplied in Python within Form Recognizer outputs the fields in a set of print statements which is not very useful

The actual model creation is out of the scope for this work but few tips are provided
1. If you want to leaverage the new Neural model, there is a set of regions that support it. 
https://learn.microsoft.com/en-us/azure/applied-ai-services/form-recognizer/concept-custom-neural?view=form-recog-3.0.0#supported-regions

Make sure that the work is done in a region that supports Neural model in case you want to leverage a custom model with that functionality. 

2. If you are using a custom model, drawing a region box around even typed in records provides better results. For handwritten/scanned forms, it is highly recommended to use the region box

3. In case you want to go back and make changes to the underlying model, remember it will force you to create a new model. As of October 2022, there is no support yet for overwriting an existing model with the same model name. This is critical -- Make sure you "batch" all your changes together after initial model creation instead of going one change at a time


Refer the high level architecture used for the solution
![Architecture](https://github.com/ujvalgandhi1/FormRecognizerWithSynapse/blob/main/Images/Github%20Architecture.jpg)

**Refer to the section on Synapse for the actual data extraction and processing pieces**
