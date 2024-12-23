# CNN Model for Predicting BN-Doped Biphenylene Properties

This repository contains the code and data for the paper:

**"Boron and nitrogen doping engineering of biphenylene electronic and optical properties using deep learning"**  
Published in *Materials Today Communications*, Volume 40, 2024.  
DOI: [10.1016/j.mtcomm.2024.109847](https://doi.org/10.1016/j.mtcomm.2024.109847)  
[Link to the Paper](https://www.sciencedirect.com/science/article/pii/S2352492824018282)

## Abstract

The research investigates the effects of randomized nitrogen and boron doping on the structural, electronic, and optical properties of biphenylene monolayers using convolutional neural networks (CNNs). A dataset of 35 different doping configurations is used to train the CNN model to predict band gaps and permittivities with high accuracy.

## Repository Structure

The repository contains the following files:

- `BNDopedBiphenylene3.csv` - Contains the configurations of doped biphenylene, along with their corresponding properties (band gaps, permittivities, etc.).
- `BNDopedBiphenylene_CNN.ipynb` - Jupyter notebook with the code to define, train, and evaluate the CNN model on the dataset.
- `requirements.txt` - Lists all the Python libraries required to run the code (TensorFlow, Keras, Pandas, etc.).

## Data Overview

The dataset, `BNDopedBiphenylene3.csv`, contains 35 unique configurations of BN-doped biphenylene networks. Each configuration is represented as a $5\times5$ matrix corresponding to a 24-atom supercell of the biphenylene monolayer, with an additional atom added to match the dimensions required by the model. The matrix uses the following encoding:

- **0.5**: Carbon atoms
- **0.0**: Boron dopant
- **1.0**: Nitrogen dopant

The output data for the model includes the structural, electronic, and optical properties derived from density functional theory (DFT) calculations, such as lattice vectors, direct and indirect band gaps, and dielectric permittivities.

## CNN Model Overview

### Model Architecture:

The CNN model used in this research has the following architecture:

- **Convolutional layers**:
  - 1st layer: 16 filters
  - 2nd layer: 32 filters
  - 3rd layer: 64 filters
  - 4th layer: 128 filters
  - All convolutional layers use a $2\times2$ kernel.
  
- **Pooling**: A max-pooling layer follows the final two convolutional layers with a pool size of $2\times2$.
  
- **Fully Connected (FC) layers**:
  - After the convolution layers, the feature map is flattened and passed through seven fully connected layers with the following neuron counts:
    - 280, 350, 105, 280, 315, 140, 175 neurons respectively.
  - The **sigmoid** activation function is applied to the FC layers.

- **Dropout**: A dropout layer with a rate of 0.25 is added after the FC layers to prevent overfitting.

- **Output Layer**: The final output layer with one neuron uses the **sigmoid** activation function for predictions.

- **Optimizer**: The model uses the **RMSprop** optimizer with a learning rate of **0.0014**.

- **Training Strategy**: The model employs early stopping, halting training when no improvement is observed in the validation loss for 120 consecutive epochs.

### Hyperparameter Tuning:

Hyperparameters were tuned using KerasTuner's RandomSearch.

## How to Run the Code

1. If you're using Google Colab, upload both the data file `BNDopedBiphenylene3.csv` and the `requirements.txt` file to your Google Drive. If you're running the code locally, download both files from the GitHub repository.
2. Open the Colab notebook `BNDopedBiphenylene_CNN.ipynb` if you're using Google Colab. If you're running locally, open the Jupyter Notebook or your preferred Python environment and load the `BNDopedBiphenylene_CNN.ipynb` file.
3. Set the appropriate paths in the notebook to load the dataset and the requirements file:
   - For Google Colab, make sure to point to the files in your Google Drive.
   - For local use, ensure the paths correctly reference the location of the files on your system.
4. Before running the code, ensure that the required Python libraries are installed:
    - If you're using Google Colab, you can install the dependencies by running the following command in a code cell:
      ```bash
      !pip install -r /path/to/requirements.txt
      ```
      Make sure to replace `/path/to/` with the actual path to the `requirements.txt` file in your Google Drive.
    - If you're running the code locally, navigate to the repository folder in your terminal and install the dependencies by running:
      ```bash
      pip install -r requirements.txt
      ```
5. Once the dependencies are installed, you can proceed to run the notebook. Train the model and visualize the results using the provided scripts.

