Sign Language Digit Feature Extraction and PCA Analysis

This project processes a dataset of sign language digits using feature extraction techniques such as GLCM (Gray Level Co-occurrence Matrix) and HOG (Histogram of Oriented Gradients) and performs dimensionality reduction on HOG features using PCA (Principal Component Analysis). Extracted features are stored in CSV files, enabling further analysis or training in machine learning models.

1. Introduction
    This project is designed to preprocess and analyze sign language digit images from the Sign-Language Digit Dataset directory. Each image is preprocessed, segmented, and analyzed for textural features using GLCM and shape features using HOG. HOG features are then reduced in dimensionality using PCA to preserve 95% of the variance.

2. Features Extracted
    The project extracts:

    - GLCM Features: Contrast, Dissimilarity, Homogeneity, ASM, Energy, and Correlation
    - HOG Features: 9 orientations, pixels per cell (2x2), cells per block (2x2), for edge directionality and intensity
    - PCA on HOG Features: Reduces HOG features while preserving 95% of variance

3. Requirements
    The following Python packages are required:
    - opencv-python for image processing
    - numpy for array manipulation
    - scikit-image for GLCM and HOG feature extraction
    - matplotlib for plotting explained variance and HOG images
    - scikit-learn for PCA and feature scaling

4. Usage
    - Prepare the Dataset: Place sign language images in subdirectories within Sign-Language Digit Dataset, where each folder name represents a label (e.g., 0, 1, 2...).
    - Run the Script: Execute the Python script to extract features and save them into CSV files.
    - Output: CSV files containing GLCM, HOG, and PCA HOG features.

5. File Structure
    ├── Sign-Language Digit Dataset/         # Dataset directory
    │   ├── 0/                               # Images labeled as 0
    │   ├── 1/                               # Images labeled as 1
    │   └── ...                              # Additional labels
    ├── MLP301BachDuongGLCMFeatures.csv      # CSV file for GLCM features
    ├── MLP301BachDuongHOGFeatures.csv       # CSV file for HOG features
    ├── MLP301BachDuongPCA_HOG_Features.csv  # CSV file for PCA-reduced HOG features
    └── main.py                              # Main script file

6. Functions Explained
    - imagePreprocessing
        Input: RGB image
        Process: Converts the image to HSV, adjusts saturation and brightness, and applies Gaussian blur to reduce noise.
        Output: Blurred and adjusted saturation channel (used as input for segmentation).
    - imageSegmentation
        Input: Preprocessed image
        Process: Applies binary thresholding followed by morphological erosion to segment the region of interest.
        Output: Segmented binary image (ROI).
    - GLCMCalculator
        Input: Region of Interest (ROI)
        Process: Computes GLCM and derives textural properties: contrast, energy, homogeneity, correlation, dissimilarity, and ASM.
        Output: List of GLCM features.
    - HOGCalculator
        Input: ROI, image name, label, show_plot flag
        Process: Resizes ROI, calculates HOG features and visualizes them if specified.
        Output: List of HOG features.
    - PCAHOGCalculator
        Input: List of HOG features
        Process: Standardizes HOG features, applies PCA, and visualizes explained variance.
        Output: List of PCA-reduced HOG features.
    - writeFeaturesToCSV
        Purpose: Writes feature data to CSV files. If the CSV file does not exist, writes the header first.

7. CSV Outputs
    The following CSV files are generated:

    - MLP301BachDuongGLCMFeatures.csv: Contains GLCM features for each image.
    - MLP301BachDuongHOGFeatures.csv: Contains raw HOG features for each image.
    - MLP301BachDuongPCA_HOG_Features.csv: Contains PCA-reduced HOG features for each image.

    CSV Headers
    - GLCM CSV Header: ["Images", "Contrast", "Dissimilarity", "Homogeneity", "ASM", "Energy", "Correlation", "Label"]
    - HOG CSV Header: ["Images"] + ["Feature 1", "Feature 2", ..., "Feature N"] + ["Label"]
    - PCA HOG CSV Header: ["Images"] + ["Feature 1", "Feature 2", ..., "Feature M"] + ["Label"]

    Results
    - The results of PCA on HOG features are shown through a cumulative explained variance plot and a bar graph of explained variance by components. These plots help visualize the effectiveness of dimensionality reduction and ensure that 95% of variance is retained.