# ASD-Facial-Emotion-Recognition
Facial emotion recognition in children with ASD using MediaPipe Face Mesh, MobileNetV2, ResNet18, Valence-Arousal mapping, and Streamlit.
Facial Emotion Recognition in Children with Autism Spectrum Disorder
Segmentation-Based CNN and Valence–Arousal Mapping

This repository accompanies the research manuscript “Facial Emotion Recognition in Children with Autism Spectrum Disorder Using Segmentation-Based CNN and Valence-Arousal Mapping” by Junidar et al., submitted to Jurnal RESTI (Rekayasa Sistem dan Teknologi Informasi).

The study investigates facial-expression classification for two emotion categories—joy and sadness—using landmark-guided facial-region segmentation, convolutional neural networks (CNNs), and a predefined Valence–Arousal mapping. A web interface was developed using Streamlit to demonstrate image-based inference and emotion visualization.
Repository status: The research description and instructions are documented here. Source-code files, trained model weights, and executable setup instructions must be checked against the actual implementation before this repository is described as fully reproducible.

Research objectives
- Identify facial regions relevant to emotion recognition (eyes, eyebrows, nose, and mouth) using MediaPipe Face Mesh landmarks.
- Compare MobileNetV2 and ResNet18 for classifying segmented images into joy or sadness.
- Map discrete emotion predictions to predefined two-dimensional Valence–Arousal coordinates.
- Present the classification and mapping results through a Streamlit web application.
Dataset
Source: Autistic Children Emotions Dataset — Dr. Fatma M. Talaat (Kaggle)

The selected research subset contains 606 images:
Partition	Total images	Joy	Sadness
Training	440	280	160
Validation	110	70	40
Testing	56	42	14
Total	606	392	214


The reported evaluation uses an image-level split. The source documentation does not establish that images from the same child are excluded across different partitions; therefore subject-independent generalization cannot be claimed from this split.

Privacy: This repository does not include or redistribute children's facial images. Obtain data directly from the original source and verify its usage conditions, consent documentation, and any redistribution restrictions.
Proposed processing pipeline
1. Face detection and cropping: Locate the face and crop around the detected facial region.
2. Facial landmark estimation: Identify facial landmarks using MediaPipe Face Mesh (468 landmarks in the implementation described in the study).
3. Region-of-interest segmentation: Retain the eyes, eyebrows, nose, and mouth using landmark-based regions, convex-hull masks, dilation, and bitwise masking.
4. Image preparation: Resize to 224 × 224 pixels and normalize using ImageNet channel statistics.
5. Training augmentation: Apply slight rotation, horizontal flipping, translation, and brightness adjustment to training images.
6. CNN inference: Classify each image as joy or sadness with MobileNetV2 or ResNet18.
7. Emotion mapping: Convert the predicted class to a fixed Valence–Arousal coordinate.
8. Web visualization: Show the predicted class and its mapped point in Streamlit.
Models and training
The study compares two CNN architectures, MobileNetV2 and ResNet18, using segmented face images. Training is reported for 30 epochs for each architecture. The best validation checkpoint was obtained at epoch 19 for MobileNetV2 and epoch 15 for ResNet18 (epoch numbering as described in the thesis). The documented optimizer is Adam with a learning rate of 0.001, and the loss function is cross-entropy. Class weighting was used to address label imbalance.

The original methodology lists batch-size options of 16 / 32; it does not unambiguously specify one final batch size for each reported run. Refer to the actual training scripts or logs for exact run configuration.
Experimental results
Results reported on the 56-image test partition:
Model	Accuracy	Precision	Recall	F1-score
MobileNetV2	92.86%	92.80%	92.86%	92.67%
ResNet18	94.64%	95.00%	94.64%	94.41%


The study reported a paired t-test result of p = 0.322 for the model comparison. This was not statistically significant at the 0.05 level. The analysis is based on one image-level test split; results should not be taken as evidence of clinical validity or performance on unseen participants.
Valence–Arousal mapping
The application assigns fixed coordinates to the predicted emotion label:
Emotion	Valence	Arousal
Joy	+0.8	+0.6
Sadness	−0.7	−0.4


These values are predefined lookup coordinates, not continuous Valence–Arousal values predicted by a regression model.
Streamlit implementation
The study describes a Streamlit interface that allows users to upload a facial image and view its predicted emotion along with a Valence–Arousal visualization.
Running the app locally
The exact entry-point filename and dependencies must be confirmed from the actual code. If the repository contains requirements.txt and the Streamlit entry point is app.py, the typical commands are:
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS / Linux:
# source .venv/bin/activate
pip install -r requirements.txt
streamlit run app.py
Replace app.py with the actual Streamlit script filename if different. Ensure that any required model weights are obtained legally and placed at the path expected by the code. The commands above are a setup template, not a claim that the current repository already contains these files or has been tested end-to-end.
Suggested files to publish
- Streamlit application entry point and supporting Python modules.
- Preprocessing/segmentation and inference code.
- Model training and evaluation scripts, when available.
- A tested requirements.txt and updated instructions with exact commands.
- Model weights only if sharing is authorized and appropriate.
Do not publish children's facial images, private credentials, or other sensitive information.
Limitations and responsible use
- The reported dataset contains only two emotion classes and a limited number of test images.
- The reported partition does not establish a subject-wise split.
- The system was assessed on static images; real-time video performance was not evaluated.
- The emotion classification is not a diagnostic test for Autism Spectrum Disorder and should not replace professional assessment.
- Images of children constitute sensitive personal data. Any new data collection or real-world deployment requires appropriate consent, privacy safeguards, and applicable ethical review.
Citation
If you use this research or implementation, please cite the associated manuscript once its final bibliographic details and DOI become available:
Junidar et al., “Facial Emotion Recognition in Children with Autism Spectrum Disorder Using Segmentation-Based CNN and Valence-Arousal Mapping,” Jurnal RESTI, manuscript under editorial evaluation.

Do not assign a volume, issue, page range, or DOI until the journal provides the publication record.
Contact and code availability
For questions regarding the research, contact the corresponding author using the contact information provided in the manuscript. The existence of this public repository does not by itself establish that all source-code components have been released; check the files currently present.
License
No open-source software license has been selected yet. Unless a license is added by the authors, public visibility of this repository does not grant blanket permission to reuse or redistribute its contents.
