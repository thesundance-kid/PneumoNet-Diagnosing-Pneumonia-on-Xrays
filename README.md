# PneumoNet: Deep Learning for Pediatric Pneumonia Detection  

## Project Overview  
This repository demonstrates the application of deep learning for automated detection and classification of pneumonia from pediatric chest X-rays, utilizing transfer learning with the InceptionV3 architecture. It was trained to do three way classification of pediatric patients' chest X-rays as Normal, Bacterial Pneumonia, or Viral Pneumonia. 

## Impact & Significance  
Pneumonia is a leading cause of childhood mortality worldwide. This project shows how deep learning can:  
    - Support radiologists in rapid X-ray screening  
    - Provide preliminary diagnosis in resource-constrained settings  
    - Demonstrate AI's potential in pediatric medical imaging  

## Dataset
The dataset used is from the National Institutes of Health (NIH), available on Kaggle: Chest X-ray Dataset. The dataset contains over 5000 X-ray images that are labeled for different conditions, including pneumonia. For this project, the X-rays are categorized as:

Normal: Healthy lung X-rays.  
Bacterial Pneumonia: X-rays showing bacterial infection.  
Viral Pneumonia: X-rays showing viral infection.  

You can find the dataset at this link: https://www.kaggle.com/datasets/nih-chest-xrays/data  
The xrays are originally separated only into two folders for normal vs pneumonia. But the xrays in the pneumonia folder are titled as bacterial or viral. I separated them into two separate folders: bacterial pneumonia and viral pneumonia before training.  

## Repository Structure  

notebooks: contains notebooks for training and testing the Inception V3 model. For reference, I also used VGG16 for transfer learning and the notebooks for its training and testing is included as well. It approached similar accuracy.  

models: model weights  

README.md: project documentation


## Results  

The model achieves:  

79.01% accuracy in three-way classification (Normal/Bacterial/Viral)  
89.74% accuracy in binary classification (Normal/Pneumonia)  
99.23% sensitivity for pneumonia detection (Normal Vs Pneumonia) 
73.93% specificity for normal case identification  

Significant points: 

The model had a very high sensitivity for detecting pneumonia. One way to interpret that fact, is that if the model classifies a pediatric chest xray as normal (not having pneumonia of either type), we can be very confident in that prediction. This however is not that impressive as physicians are pretty good at detecting pneumonia on xrays with just their eyes (sensitivity of around 93%, Taghizadieh A, Ala A, Rahmani F, Nadi A. Diagnostic Accuracy of Chest x-Ray and Ultrasonography in Detection of Community Acquired Pneumonia; a Brief Report. Emerg (Tehran). 2015 Summer;3(3):114-6. PMID: 26495396; PMCID: PMC4608340.)  

A more suprising result however is that the model has a good deal to say about bacterial pneumonia. It has a sensitivity of 92.95, and speficitiy of 79.8% We get these numbers if we reduce the problem to a 2 way classification of bacterial pneumonia vs not bacterial pneumonia (which includes no pneumonia and viral pneumonia)  This high sensitivity is much more impressive since determining from an xray alone whether a penumonia was bacterial or viral in nature is much more challenging and not often possible without additional workup. This is also a potential use-case as combatting the overprescription of antibiotics is a large global health effort. If this model can be well trusted at ruling out bacterial infections, providers can feel safe in knowing that they can avoid prescribing an antibiotic without putting the patient in uneccessary risk.  

Within the testing notebook for the inception v3 transfer model, there is a Confusion Matrix with the full breakdown of the results of the model on classifying the test set.  


## Related Work
Notably, the 2018 paper by Kermany et al. titled Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning Kermany et al., 2018 applied a similar transfer learning approach using the VGG16 model to classify chest X-rays and achieved an accuracy of 92.8% in distinguishing pneumonia from normal X-rays and 90.7% in distinguishing bacterial from viral pneumonia. I offer a more detailed breakdown of my results on the test set, and I believe a pneumonia detection model with higher sensitivity. This model detected pneumonia with a 99.2% sensitivity and 73.9% specificty.  

# Future Work
Here are some potential directions I am considering to explore in the future:

Other Architectures: Experiment with other architectures like ResNet. Or unfreeze more layers of the InceptionV3 model (though I am unfortunately running low on free google colab compute).  
Hyperparameter Tuning: Further optimize learning rates, batch sizes, and other hyperparameters.  
Larger Dataset: Testing the model on larger or more diverse datasets could help improve generalization.  
Model Interpretability: Apply techniques like Grad-CAM to visualize the areas of X-rays the model focuses on for its predictions.
