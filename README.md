# BRATS-Pretext-Tasks-for-Self-supervised-Deep-Learning
Emma Baskerville & Oakleigh Weekes

# BRATS Dataset
+ Brain Tumor Image Segmentation Benchmark

+ BraTS 2018 is a dataset which provides multimodal 3D brain MRIs and ground truth brain tumor segmentations annotated by physicians, consisting of 4 MRI modalities per case (T1, T1c, T2, and FLAIR). (Bjoern H. Menze et al)

+ Within each modality, or “channel”, the structure becomes an array of size [:,:,:] (Sagittal:Coronal: Axial) . The channel refers to the receiver pathway of the MRI system. They show as different contrasts. These can be accessed using the NiBabel Python toolset.

* “Flair” Channel was used as it shows the brain images in clear contrast.
![image](https://user-images.githubusercontent.com/57076065/132038365-18ca18eb-b4f3-4c43-822d-660e44f35574.png)
![image](https://user-images.githubusercontent.com/57076065/132038371-8b32c821-9804-4a9d-bb79-4f18de1b663c.png)
![image](https://user-images.githubusercontent.com/57076065/132038387-010f212b-5e14-4c4c-bf2a-85e725492434.png)

# Pre-text Tasks
A pretext task is a self-supervised learning task solved to learn visual representations, with the goal of using the learned representations or model weights obtained in the process for a downstream task. E.g. A classification model’s weights used for training a “Segmentation” model.
We trained 4 models*, 2 classification and 2 regression;
+ MRI Brain Direction Classification
+ MRI Brain Rotation Classification
+ MRI Brain slice index Regression
+ MRI Brain image Context Regression

*These Convolution (CNN) Models were created using TensorFlow and Keras’ Libraries.

# Brain Direction Classification

+ The first model learned a simple classification problem. A model was trained using Sagittal, Coronal and Axial Images, and to classify those out-of-sample.
+ Using Keras’ Image Data Generator, training images were organised according to directory saved, with some variation created by train_datagen.

![image](https://user-images.githubusercontent.com/57076065/132038584-4e6c7c86-a10e-49da-a27f-c862128ba25a.png)

# Brain Rotation Classification

+The second model learned the angle of the brain image was visualized in.
+Pre-processing involved manually rotating images and saving into directories.

![image](https://user-images.githubusercontent.com/57076065/132038699-3cc12cb5-c032-427a-b17a-468af6ef28cc.png)

![image](https://user-images.githubusercontent.com/57076065/132038767-d90ee457-f697-4c17-a03c-37a0832e6d34.png)

# MRI Brain Slice Index Regression

+ The third model was a regression model. It would learn the index of a brain slice.
+ 3 versions of this model were created, to separately learn Axial, Sagittal and Coronal array indexes.
+ Different indexes exist for different “Slice Types”, but within these they are similar per brain example. For instance the brain is present in Sagittal Slice Layers ~51-186.
+ A .csv method was used for data input as opposed to the previously used Data Generator technique for Classification.
+ Loss was a more “Accurate” depiction of learning here. RMSE was reduced to 35.92.

![image](https://user-images.githubusercontent.com/57076065/132038942-3a6d7c7e-fa6a-47e2-b5b6-077278b44d26.png)

# Brain Image Context Regression

+ We wanted to create an unpuzzling model, which would essentially rectify an image of the brain in jumbled pieces. We were not able to do so with our experience in a limited timeframe.
+ However, we realised we could use some of this code we created to form a context-learning model. Such as NumPy image splitting.
+ After splitting the images into 9 different equal segments (after “Squaring” the slice images), the algorithm was trained on this data.
+ We made this a regression problem, however it can be argued that this problem is more suitable for classification methods as there are only 9 potential classes, and no ‘particular’ linear relationship between the segments.
+ However, the model learned well with high accuracy, and an unconventional confusion matrix could still be created.
+ Classification may be a better option if this model’s weights were to be brought into a segmentation model, for better context awareness unrelated to index.
+ This model was created using the .csv method, and again one for each “Slice Direction”.

![image](https://user-images.githubusercontent.com/57076065/132039060-c28d923e-8ed2-4d3d-b127-7fa6cfa735e3.png)

![image](https://user-images.githubusercontent.com/57076065/132039081-80133ccc-7878-4ee5-8688-3c54330a75d1.png)

# Outcomes
![image](https://user-images.githubusercontent.com/57076065/132039173-ec0221d5-28df-4588-b265-c76ee18c04d1.png)

+ Models were successfully trained using the BRATS dataset, with good accuracy metrics and perform well on out-of-sample test data.

+ These model’s weights can be saved and brought into a downstream task such as brain tumour segmentation, possibly using U-Net.

# Notebook Set-up

+ Open a notebook from here in Google Colab.
+ Download BRATS dataset https://www.kaggle.com/sanglequang/brats2018.
+ Unzip Dataset into your Google drive e.g. using Zip Extractor https://chrome.google.com/webstore/detail/zip-extractor/mmfcakoljjhncfphlflcedhgogfhpbcd .
+ Mount your google drive in the first notebook code block, and format paths accordingly.

# Links

+ BRATS: https://ieeexplore.ieee.org/document/6975210
+ NiBabel: https://nipy.org/nibabel/
+ U-Net: https://arxiv.org/pdf/1505.04597.pdf
+ Self-Supervised Learning Based on Spatial Awareness for Medical Image Analysis:
https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9186121
