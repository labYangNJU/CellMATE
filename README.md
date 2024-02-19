# CellExpanda
# Introduction
CellExpanda is implemented by python to take full advantage of paired single-cell multimodal data for holistic representation of cells. Running CellExpanda on GPU is recommended if available.

For more details, please check our publication later.


# Directory structure
      .
      ├── CellExpanda          # Main Python package
            ├── configs        # Config yaml files for each dataset 
            ├── main.py
            ├── model.py
            ├── modules.py
            ├── ...  
      ├── data                 # Input datasets
      ├── scripts              # Scripts for reproducibility of results in the manuscript
      ├── env.yaml             # Reproducible Python environment via conda
      ├── LICENSE
      └── README.md


# Input Data
CellExpanda takes count matrices from paired single-cell multimodal data. There is no limitation for the types and numbers of modalities.
An expample input dataset can be found in the CellExpanda/data/ directory. Note: You should change the "sampleName" of files according to your own dataset.
Three files are required:

1.sampleName_SparseMatrix.txt 

The raw count sparse matrix for the multimodal dataset with features from all modalities.

2.sampleName_barcode.txt  

The barcode file with one barcode per line for each cell.

3.feature_discriminator.txt  

The file with feature information. You can increase weight for selected features which could be more important for cell clustering. For example, features can be selected using tools like DubStepR (PMID: 34615861
        
        ). The first column is feature name and the second column is the additional weight for particular features. If no additonal weigh is needed, set 0 for the feature.


# Installation
option 1:
Create a conda environment with python3 and install all the dependencies.

option 2:
Create an environment from the env.yml file (We tested with conda==4.12.0, python==3.6.9).

      conda env create -f env.yaml

Notes: 
If any dependencies are not installed automatically, you should install them by pip or conda.
If GPU is used, the torch version should be compiled with your version of the CUDA driver.


# Usage
1.Activate conda environment

      conda activate CellExpanda

2.Configure your sampleName.yaml files under the directory CellExpanda/configs/. Detailed instructions can be found in the ReadMe_for_ConfigYaml_file.txt file.

3.Run the CellExpanda model.

      python3 main.py --dataset=sampleName


# Output 
The output includes 1) the representation of cells; 2) the reconstructed single-cell multimodal data.

The representation of cells would be generated in the directory CellExpanda/result/.

      result
      ├── sampleName                                
            ├── latent-sampleName-512-10.txt        # The latent representation of cells (can be used to generate UMAP emmbeddings).
            ├── GMVAE-alpha-gan-tsne-pred.png       # The tSNE visualization of cells. 
            ├── ...  
      └── sampleName-512-10-cluster_result.csv      # The clustering information of cells with tSNE emmbeddings. 
      
The reconstructed data would be generated in the directory CellExpanda/model/ and can be extracted as: 
      

# Dependencies
+ Python3
+ sklearn
+ torch
+ matplotlib
+ numpy
+ networkx
+ igraph
+ pyyaml
+ pandas
+ tensorboardX
+ python-louvain
+ leidenalg
+ umap
+ torchsummary
+ pysam
+ pytorch_metric_learning
