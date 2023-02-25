# Protein-sequence-NLP-classifier
Utilizes fastText, a NLP library, to train a classification model on protein sequence vs function. Further analysis on the latent space of the model dictionary

## data preprocessing


## training

## model testing

## model dictionary + latent space analysis 
In the fasttext model, there are 33 words learned. This includes the 20 amino acids and the word "X", which denotes an unknown amino acid. U, B and other words are also included due to incomplete data filtering (TODO: remove excess words). 

Regarding the latent space, each word vector is represented as a 100 dimensional array. 
![image](https://user-images.githubusercontent.com/67357603/221338778-3c8d55b9-221f-4a93-b570-16865e9469b6.png)

Sentences are made up of multiple amino acid words, such as "M A G L T", etc. 

fastText includes a method for getting the nearest neighbor words, given an input word, based on word vector similarity. 

### Interesting similarities include 
`model.get_nearest_neighbors("Y")`, which returns 
```
[(0.6904587149620056, 'W'), (0.5058212280273438, 'F'), (0.5003066658973694, 'I'), (0.4387292265892029, 'C'), (0.30492833256721497, 'X'), (0.2789316177368164, 'N'), (0.22475895285606384, 'T'), (0.22140520811080933, 'A'), (0.20832818746566772, 'H'), (0.1720615029335022, 'SYSTEM')]
```

For reference, here are the molecular structures of Y, W, and F: 
![image](https://user-images.githubusercontent.com/67357603/221339050-9276a8d0-2c40-4464-9998-5ac74f880d78.png)
![image](https://user-images.githubusercontent.com/67357603/221339044-1f61c261-e0e4-48be-9cbd-f579a300942a.png)
![image](https://user-images.githubusercontent.com/67357603/221339031-f21ea02a-5505-4138-90dc-94a77f6226aa.png)

In this case, all three amino acids have cyclical groups in them. 

`model.get_nearest_neighbors("D")`, which returns 
```
[(0.52745121717453, 'Q'), (0.34312954545021057, 'E'), (0.26880571246147156, 'ADHESION'), (0.2516576945781708, 'G'), (0.2177438586950302, '</s>'), (0.21692746877670288, 'K'), (0.21415236592292786, 'S'), (0.08069909363985062, 'A'), (0.07903637737035751, 'FUNCTION'), (0.07583718001842499, 'INHIBITOR')]
```

For reference, here are the molecular structures of D, Q and E 
![image](https://user-images.githubusercontent.com/67357603/221339326-29c44ab9-37b9-41eb-97ff-1fa94c2ab6f7.png)
![image](https://user-images.githubusercontent.com/67357603/221339314-a4cb3de2-f3ae-4c4a-9d6f-f8b8ed354ab6.png)
![image](https://user-images.githubusercontent.com/67357603/221339336-6f872e75-9321-41cd-b0ba-2d20e927a209.png)

In this case, the amino acids share similar structural features, as well as similar molecular charges as D and E are both negatively charged. 

This highlights interesting structural features that are preserved within the data, such as cyclical molecules. Without knowing anything about biochemistry, the NLP model is able to infer structural, chemical, and molecular similarities between amino acids. 

## improvements
Multiple next steps are needed to improve upon the project. The biggest improvement will be better filtering and pre-processing techniques to reduce the model dictionary count for a more accurate reflection of the actual world (reducing 33 words to 20 to represent the amino acids). 

With more test data and multiple different types of proteins, the model should have a better and more general inference of amino acid structure and chemical nature. There may be unseen biases in utilizing only these specific protein functionalities. For example, training on only intermembrane transport proteins will result in the model learning about hydrophobicity of amino acids, while potentially losing information about how certain amino acids act as docking sites/receptors (eg serine/threonine) 

dimensionality reduction and other visualization techniques will be implemented to better visualize how different amino acids cluster together in terms of similarity. 


