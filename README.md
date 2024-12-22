# Show_and_Tell

Image Captioning Project using 2 Slightly different **Encoder-Decoder architectures**

## Dataset
- **Flickr8k** dataset consisting of **8000** images each having 5 captions to desribe it
- Link: https://www.kaggle.com/datasets/aladdinpersson/flickr8kimagescaptions/data

## Frameworks and Resources : 

1. Python
2. Pytorch
3. 2x T4 GPU'S in Kaggle Notebook

## Data Distribution

- Training dataset: **5600** images with 5 captions for each
- Validation Set: **1200** images with 5 captions for each
- Test Set : **1200** images with 5 captions for Each
- Mini-Batch Gradient Descent was used with a Batch size of **32**

## Model-1

### Encoder

- Encoder consists of **ResNet-50** Model. The last layer is removed and replaced by a custom linear layer supplemented with batch-normalization
- Other layers of ResNet-50 are Freezed. Only thr last layer is trainable in the Encoder

### Decoder

- Decoder Consists of a Single **LSTM**
- The captions are first sent via an **Embedding layer** with a dropout rate of 0.5
- The image features obtained from the encoder will be the initial Hidden state in the Decoder
- Inital cell state is initialized to zero tensor
- **Teacher forcing** is done to enable the LSTM to learn Fast and not Deviate
- Weights are initialized with **Xavier initialization method**
- The hidden states outputted at each timestep is sent via a Linear layer of vocabulary to get scores from which we out the word w

### Hyperparamters

- Epochs: 10
- Embedding Dimension: 256
- Hidden State Dimension and Cell state Dimension: 512
- Vocabulary_size : Around 8000
- Loss Function: Cross Entropy Loss Function
- Optimizer: Adam Optimizer with learning rate of 1e-4 and decay rate of 1e-4
- Learning rate sceduler has been applied with step size of 5 and decrement rate being 0.1

### Architecture 

![Model-1](https://github.com/user-attachments/assets/4a3c1e9f-369d-42b4-9a6c-799912cdb444)


### Training Summary


![image](https://github.com/user-attachments/assets/f7b1fb97-4d4c-4363-add1-a0c623fba815)


![image](https://github.com/user-attachments/assets/9c8cf634-d526-48dc-b8d6-3ac4ea71396b)


### Result 

**BLEU Score on Test Dataset : 13%**

- Note : Greedy Search Has Been Applied

**Remark**:
Since It's a vanilla Model hence we do not see great results on Test data

### Demo:


![image](https://github.com/user-attachments/assets/4931a404-5477-4201-9275-006e9d3952ed)   

![image](https://github.com/user-attachments/assets/5ec8a7fe-7574-4760-b01d-43a5a64836a8)

![image](https://github.com/user-attachments/assets/c36a214c-ccea-4cbf-a2d0-384e42a0332f)

![image](https://github.com/user-attachments/assets/a8d38222-e46f-4053-8963-9bcbd85e1cac)




## Model-2

### Encoder

- Encoder consists of **ResNet-50** Model. The last layer is removed and replaced by a custom linear layer supplemented with batch-normalization
- Other layers of ResNet-50 are Freezed. Only thr last layer is trainable in the Encoder

### Decoder

- Decoder Consists of a **2 layer LSTM**
- The captions are first sent via an **Embedding layer** with a dropout rate of 0.5
- Inital cell state and Hidden state  are initialized to zero tensor
- The image features obtained from the encoder will be concatenated with the output hidden state at each time step
- The concatenated vector is passed via a linear layer through which we obtain logit scores and extract the word from it
- Teacher forcing is done to enable the LSTM to learn Fast and not Deviate
- Weights are initialized with **Xavier initialization method**

### Hyperparamters,Loss Function and Optimizer

- Epochs: 10
- Embedding Dimension: 256
- Hidden State Dimension and Cell state Dimension: 512
- Vocabulary_size : Around 8000
- Loss Function: Cross Entropy Loss Function
- Optimizer: Adam Optimizer with learning rate of 1e-4 and decay rate of 1e-4
- Learning rate sceduler has been applied with step size of 5 and decrement rate being 0.1

### Architecture

![Model-2](https://github.com/user-attachments/assets/8f0ae253-d142-4d6b-986f-55b0a34a2e3e)


### Training Summary

  
![image](https://github.com/user-attachments/assets/63817cea-3c39-49a9-a452-977a869f04af)


![image](https://github.com/user-attachments/assets/a34ec742-48fb-40ea-929a-e334a54e5cbf)


### Result

**BLEU Score on Test Dataset : 12%**

- Note: Beam Search has been applied with window size of 3

Remark: Inspite of increasing the number of layers in LSTM and also providing the image information at each time step, No improvement Found

### Demo


![image](https://github.com/user-attachments/assets/f3b6e18a-c225-45ce-afdc-ccde1f3c5a98)


![image](https://github.com/user-attachments/assets/161788cf-6563-4b1c-9047-3e3889e05f4f)


![image](https://github.com/user-attachments/assets/bae09952-2abc-4723-94ea-5c576ab66321)


![image](https://github.com/user-attachments/assets/5ec7b2c8-90a1-4dba-b79e-db3b06be7529)












