# BRATS-Pretext-Tasks-for-Self-supervised-Deep-Learning
Emma Baskerville & Oakleigh Weekes

Self-Supervised Deep
Learning; Comparison
of pre-text tasks for
Multi-Modal Brain
Tumour Segmentation


Emma Baskerville & Oakleigh Weekes
BRATS
Dataset
+Brain Tumor Image Segmentation
Benchmark                                         “Flair” Channel was
                                                  used as it shows the
+BraTS 2018 is a dataset which provides
                                                  brain images in clear
multimodal 3D brain MRIs and ground truth
                                                  contrast.
brain tumor segmentations annotated by
physicians, consisting of 4 MRI modalities per
case (T1, T1c, T2, and FLAIR). (Bjoern H.
Menze et al)
+Within each modality, or “channel”, the
structure becomes an array of size [i,:,:]. The
channel refers to the receiver pathway of the
MRI system. They show as different contrasts.
These can be accessed using the NiBabel
Python toolset.
Pre-text Tasks
A pretext task is a self-supervised learning task solved to learn visual representations, with
the goal of using the learned representations or model weights obtained in the process for a
downstream task. E.g. A classification model’s weights used for training a “Segmentation”
model.
We trained 4 models*, 2 classification and 2 regression;
+ MRI Brain Direction Classification
+ MRI Brain Rotation Classification                                           *These Convolution (CNN) Models
                                                                              were created using TensorFlow and
+ MRI Brain slice index Regression                                            Keras’ Libraries.
+ MRI Brain image Context Regression
                 +The first model learned a simple
Brain            classification problem. A model was
                 trained using Sagittal, Coronal and Axial

Direction        Images, and to classify those out-of-
                 sample.

Classification   +Using Keras’ Image Data Generator,
                 training images were organised according
                 to directory saved, with some variation
                 created by train_datagen.
                 +The second model learned the angle of
Brain Rotation   the brain image was visualized in.
                 +Pre-processing involved manually
Classification   rotating images and saving into directories.

                  0                                     180




                  90                                  270
              +The third model was a regression model.
MRI Brain     It would learn the index of a brain slice.
              +3 versions of this model were created, to

slice index   separately learn Axial, Sagittal and
              Coronal array indexes.

Regression    +Different indexes exist for different “Slice
              Types”, but within these they are similar
              per brain example. For instance the brain
              is present in Sagittal Slice Layers ~51-186.
              +A .csv method was used for data input as
              opposed to the previously used Data
              Generator technique for Classification.
              +Loss was a more “Accurate” depiction of
              learning here. RMSE was reduced to
              35.92.
              +We wanted to create an unpuzzling model, which would
              essentially rectify an image of the brain in jumbled pieces.
              We were not able to do so with our experience in a limited

Brain image   timeframe.
              +However, we realised we could use some of this code
              we created to form a context-learning model. Such as

Context       NumPy image splitting.
              +After splitting the images into 9 different equal segments
              (after “Squaring” the slice images), the algorithm was

Regression    trained on this data.
              +We made this a regression problem, however it can be
              argued that this problem is more suitable for classification
              methods as there are only 9 potential classes, and no
              ‘particular’ linear relationship between the segments.
              +However, the model learned well with high accuracy, and
              an unconventional confusion matrix could still be created.
              +Classification may be a better option if this model’s
              weights were to be brought into a segmentation model,
              for better context awareness unrelated to index.
              +This model was created using the .csv method, and
              again one for each “Slice Direction”.
Outcomes   + Models were successfully trained using the
           BRATS dataset, with good accuracy metrics
           and perform well on out-of-sample test data.

           + These model’s weights can be saved and
           brought into a downstream task such as brain
           tumour segmentation, possibly using U-Net.
                • Open a notebook from here:
Notebook Set-     oakleighw/BRATS-Pretext-Tasks-for-
                  Self-supervised-Deep-Learning

up                (github.com) in Google Colab.
                • Download BRATS dataset BRATS-2018
                  | Kaggle .
                • Unzip Dataset into your drive e.g. using
                  Zip Extractor ZIP Extractor - Chrome
                  Web Store (google.com) .
                • Mount your google drive in the first
                  notebook code block, and format paths
                  accordingly.
             • The Multimodal Brain Tumor Image Segmentation Benchmark (BRATS) |


Links &
               IEEE Journals & Magazine | IEEE Xplore

             • Neuroimaging in Python — NiBabel 3.2.1+100.g9fdf5e3e documentation
               (nipy.org)



References
             • U-Net: U-Net: Convolutional Networks for Biomedical Image Segmentation
               (arxiv.org)

             • Self-Supervised Learning Based on Spatial Awareness for Medical Image
               Analysis: IEEE Xplore Full-Text PDF:

