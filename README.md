## Image Caption Generator

By -
1. Mayank kumar
2. Mehul sinha
3. Asif nawaz
4. Pranita kaity

Colab link of Machine learning model - https://colab.research.google.com/drive/1pt17ikirVHNBavTvZoRrAhnNJyGNP8BS
Colab link of Backend - https://colab.research.google.com/drive/1XbJKW1d3MhrrVoK1ivi_5KcIsS0duqQC

A neural network mobile app to generate captions for an image using React native.


Follow the [React Native Getting Started Guide](https://facebook.github.io/react-native/docs/getting-started.html) for detailed instructions on setting up your local machine for development.

## How to run
- Clone repository and install dependencies:
    ```bash
    $ git clone https://github.com/mayank1307/imageCaption.git
    or download the zip & extract
    $ cd imageCaption
    $ npm install
    ```

- Run application
    ```bash
    $ npx react-native run-ios
    ```
    ```bash
    $ npx react-native run-android
    ```


## Table of Contents

1. [Requirements](#1-requirements)
2. [Training parameters and results](#2-training-parameters-and-results)
3. [Generated Captions on Test Images](#3-generated-captions-on-test-images)
4. [Procedure to Train Model](#4-procedure-to-train-model)
5. [Procedure to Test on new images](#5-procedure-to-test-on-new-images)
6. [Configurations (config.py)](#6-configurations-configpy)

## 1. Requirements

Recommended System Requirements to train model.

<ul type="square">
	<li>A good CPU and a GPU with atleast 8GB memory</li>
	<li>Atleast 8GB of RAM</li>
	<li>Active internet connection so that keras can download inceptionv3/vgg16 model weights</li>
</ul>

Required libraries for Python along with their version numbers used while making & testing of this project

<ul type="square">
	<li>Python - 3.6.7</li>
	<li>Numpy - 1.16.4</li>
	<li>Tensorflow - 1.13.1</li>
	<li>Keras - 2.2.4</li>
	<li>nltk - 3.2.5</li>
	<li>PIL - 4.3.0</li>
	<li>Matplotlib - 3.0.3</li>
	<li>tqdm - 4.28.1</li>
</ul>

<strong>Flickr8k Dataset:</strong> <a href="https://forms.illinois.edu/sec/1713398">Dataset Request Form</a>

<strong>UPDATE (April/2019):</strong> The official site seems to have been taken down (although the form still works). Here are some direct download links:

<ul type="square">
	<li><a href="https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_Dataset.zip">Flickr8k_Dataset</a></li>
	<li><a href="https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_text.zip">Flickr8k_text</a></li>
	Download Link Credits:<a href="https://machinelearningmastery.com/develop-a-deep-learning-caption-generation-model-in-python/"> Jason Brownlee</a>
</ul>

<strong>Important:</strong> After downloading the dataset, put the reqired files in train_val_data folder

## 2. Training parameters and results

#### NOTE

- `batch_size=64` took ~14GB GPU memory in case of *InceptionV3 + AlternativeRNN* and *VGG16 + AlternativeRNN*
- `batch_size=64` took ~8GB GPU memory in case of *InceptionV3 + RNN* and *VGG16 + RNN*
- **If you're low on memory**, use google colab or reduce batch size
- In case of BEAM Search, `loss` and `val_loss` are same as in case of argmax since the model is same

![image](https://user-images.githubusercontent.com/49157639/124943102-d367ac80-e029-11eb-9e10-911b8a4e405b.png)

## 3. Generated Captions on Test Images

| Image | Caption |
| :---: | :--- |
| <img width="50%" src="https://github.com/dabasajay/Image-Caption-Generator/raw/master/test_data/bikestunt.jpg" alt="Image 1"> | <ul><li><strong>Argmax:</strong> A man in a blue shirt is riding a bike on a dirt path.</li><li><strong>BEAM Search, k=3:</strong> A man is riding a bicycle on a dirt path.</li></ul>|
| <img src="https://github.com/dabasajay/Image-Caption-Generator/raw/master/test_data/surfing.jpeg" alt="Image 2"> | <ul><li><strong>Argmax:</strong> A man in a red kayak is riding down a waterfall.</li><li><strong>BEAM Search, k=3:</strong> A man on a surfboard is riding a wave.</li></ul>|

## 4. Procedure to Train Model

1. Clone the repository to preserve directory structure.<br>
`git clone https://github.com/mayank1307/imageCaption.git`
2. Put the required dataset files in `train_val_data` folder (files mentioned in readme there).
3. Review `config.py` for paths and other configurations (explained below).
4. Run `train_val.py`.

## 5. Procedure to Test on new images

1. Clone the repository to preserve directory structure.<br>
`git clone https://github.com/mayank1307/imageCaption.git`
2. Train the model to generate required files in `model_data` folder (steps given above).
3. Put the test images in `test_data` folder.
4. Review `config.py` for paths and other configurations (explained below).
5. Run `test.py`.

## 6. Configurations (config.py)

**config**

1. **`images_path`** :- Folder path containing flickr dataset images
2. `train_data_path` :- .txt file path containing images ids for training
3. `val_data_path` :- .txt file path containing imgage ids for validation
4. `captions_path` :- .txt file path containing captions
5. `tokenizer_path` :- path for saving tokenizer
6. `model_data_path` :- path for saving files related to model
7. **`model_load_path`** :- path for loading trained model
8. **`num_of_epochs`** :- Number of epochs
9. **`max_length`** :- Maximum length of captions. This is set manually after training of model and required for test.py
10. **`batch_size`** :- Batch size for training (larger will consume more GPU & CPU memory)
11. **`beam_search_k`** :- BEAM search parameter which tells the algorithm how many words to consider at a time.
11. `test_data_path` :- Folder path containing images for testing/inference
12. **`model_type`** :- CNN Model type to use -> inceptionv3 or vgg16
13. **`random_seed`** :- Random seed for reproducibility of results

**rnnConfig**

1. **`embedding_size`** :- Embedding size used in Decoder(RNN) Model
2. **`LSTM_units`** :- Number of LSTM units in Decoder(RNN) Model
3. **`dense_units`** :- Number of Dense units in Decoder(RNN) Model
4. **`dropout`** :- Dropout probability used in Dropout layer in Decoder(RNN) Model

