# Pneumonia Diagnosis using Transfer Learning (VGG16)
Transfer learning, using the VGG16 model, to classify patients' chest Xrays as Normal, Bacterial Pneumonia, or Viral Pneumonia.

This project applies transfer learning with the VGG16 model to diagnose pneumonia from chest X-ray images. The dataset consists of images labeled into three categories: normal, bacterial pneumonia, and viral pneumonia. This project uses two approaches—one without data augmentation and one with data augmentation—to improve the accuracy of the model.

# Dataset
The dataset used is from the National Institutes of Health (NIH), available on Kaggle: Chest X-ray Dataset. The dataset contains thousands of X-ray images that are labeled for different conditions, including pneumonia. For this project, the X-rays are categorized as:

Normal: Healthy lung X-rays.  
Bacterial Pneumonia: X-rays showing bacterial infection.  
Viral Pneumonia: X-rays showing viral infection.  

You can find the dataset at this link: https://www.kaggle.com/datasets/nih-chest-xrays/data  
The xrays are originally separated only into two folders for normal vs pneumonia. But the xrays in the pneumonia   folder are titled as bacterial or viral, so I separated them into two separate folders: bacterial pneumonia and viral   pneumonia first before training. 

# Project Summary
This project consists of two Jupyter notebooks demonstrating two different approaches for training the model:

Without Data Augmentation: The first notebook represents a baseline model where no data augmentation techniques were applied, achieving 70% accuracy.  
With Data Augmentation: The second notebook applies data augmentation techniques (such as rotation, shifting, and zooming) to increase the diversity of training images, which improved the model accuracy to 80%.  
Both notebooks follow a transfer learning approach using the VGG16 model pre-trained on ImageNet. They freeze the convolutional layers, and train only the classifier layers at the end. 

# Notebooks
1. Xray_VGG16.ipynb (Without Data Augmentation)  
Objective: First attempt at training the VGG16 model using the unmodified dataset.  
Accuracy: Reached 70% accuracy.
Key Steps:
Loading the pre-trained VGG16 model.
Fine-tuning the top layers to fit the pneumonia diagnosis task.
Training on the dataset without applying any data augmentation techniques.

2. Xray_VGG16_w_augmentation.ipynb (With Data Augmentation)
Objective: Second attempt using data augmentation to artificially expand the dataset and improve model robustness.
Accuracy: Achieved 80% accuracy.
Key Steps:
Same approach as the first notebook, but included various data augmentation techniques such as: Slight Rotation, Width and height shifting, Zooming, Rescaling.

These techniques helped the model generalize better, leading to higher accuracy. I myself was surprised that data augmentation helped in this case as chest xrays are such standardized images. For example, one augmentation technique I did not use was horizontal rotation as this would compromise a basic practice of xrays always showing the patients right side on the left side of the scan. 

Model Architecture
Base Model: VGG16 pre-trained on ImageNet.
Modifications: The top layers were replaced to adapt to the pneumonia classification task (3 output categories: Normal, Bacterial Pneumonia, and Viral Pneumonia).
Loss Function: Categorical cross-entropy.
Optimizer: Adam (with a learning rate of 0.001).
Metrics: Accuracy.

# Results
Without Data Augmentation: The model achieved 70% accuracy.
With Data Augmentation: Data augmentation improved the model accuracy to 80%.

I was quite happy with the accuracy after data augmentation. Although detecting pneumonia in a chest x ray is relatively simple for a physician, determining from an xray alone whether a penumonia was bacterial or viral in nature is much more challenging. Often additional workup is necessary. 

The promising results of this project demonstrate that data augmentation can significantly improve performance in medical imaging, even with relatively small datasets, and potentially aid in clinical decision-making. 

# Related Work
Notably, the 2018 paper by Kermany et al. titled Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning Kermany et al., 2018 applied a similar transfer learning approach using the VGG16 model to classify chest X-rays and achieved an accuracy of 92.8% in distinguishing pneumonia from normal X-rays and 90.7% in distinguishing bacterial from viral pneumonia. While their study reached higher accuracy, my project explores a similar task with a focus on the effects of simple data augmentation and using a simple, relatively small, and publicly available dataset. 

# Future Work
Here are some potential directions I am considering to explore in the future:

Other Architectures: Experiment with other architectures like ResNet or Inception. Or unfreeze more layers of the VGG16 model (though I am unfortunately running low on free google colab compute).
Hyperparameter Tuning: Further optimize learning rates, batch sizes, and other hyperparameters.
Larger Dataset: Testing the model on larger or more diverse datasets could help improve generalization.
Model Interpretability: Apply techniques like Grad-CAM to visualize the areas of X-rays the model focuses on for its predictions.
