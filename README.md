# Implementation-of-CNN

## AIM

To Develop a convolutional deep neural network for digit classification.

## Problem Statement and Dataset
Develop a model that can classify images of handwritten digits (0-9) from the MNIST dataset with high accuracy. The model should use a convolutional neural network architecture and be optimized using early stopping to avoid overfitting.
## Neural Network Model

![image](https://github.com/user-attachments/assets/34a0ff25-ab1b-434b-8f9f-ca7e3a791ba4)


## DESIGN STEPS

### STEP 1:
Import the necessary libraries and Load the data set.

### STEP 2:
Reshape and normalize the data.
### STEP 3:
In the EarlyStoppingCallback change define the on_epoch_end funtion and define the necessary condition for accuracy
### STEP 4:
Train the model
### PROGRAM:

### Name:A.ARUVI.
### Register Number:212222230014.
### Importing Libraries:
```
import os
import base64
import numpy as np
import tensorflow as tf
```
### Loading and Inspecting the MNIST dataset:
```

# Get current working directory
current_dir = os.getcwd()

# Append data/mnist.npz to the previous path to get the full path
data_path = os.path.join(current_dir, "/content/DL2.html")

# Load data (discard test set)
(training_images, training_labels), _ = tf.keras.datasets.mnist.load_data(path=data_path)

print(f"training_images is of type {type(training_images)}.\ntraining_labels is of type {type(training_labels)}\n")

# Inspect shape of the data
data_shape = training_images.shape

print(f"There are {data_shape[0]} examples with shape ({data_shape[1]}, {data_shape[2]})")
```
### Resizing and Reshaping Function:

FUNCTION: reshape_and_normalize
```
def reshape_and_normalize(images):
    """Reshapes the array of images and normalizes pixel values.

    Args:
        images (numpy.ndarray): The images encoded as numpy arrays

    Returns:
        numpy.ndarray: The reshaped and normalized images.
    """

    ### START CODE HERE ###

    # Reshape the images to add an extra dimension (at the right-most side of the array)
    images = np.expand_dims(images, axis=-1)

    # Normalize pixel values
    images = images/255.0

    ### END CODE HERE ###

    return images
```
```
# Reload the images in case you run this cell multiple times
(training_images, _), _ = tf.keras.datasets.mnist.load_data(path=data_path)

# Apply your function
training_images = reshape_and_normalize(training_images)

print('Name: A.ARUVI.          RegisterNumber: 212222230014.         \n')
print(f"Maximum pixel value after normalization: {np.max(training_images)}\n")
print(f"Shape of training set after reshaping: {training_images.shape}\n")
print(f"Shape of one image after reshaping: {training_images[0].shape}")
```
### CallBack Function:
```

# GRADED CLASS: EarlyStoppingCallback

### START CODE HERE ###

# Remember to inherit from the correct class
class EarlyStoppingCallback(tf.keras.callbacks.Callback):

    # Define the correct function signature for on_epoch_end method
    def on_epoch_end(self,epoch, logs={}):

        # Check if the accuracy is greater or equal to 0.98
        if (logs.get('accuracy')>=0.995):

            # Stop training once the above condition is met
            self.model.stop_training=True
            print("\nReached 98% accuracy so cancelling training!")
print('Name: A.ARUVI.            Register Number: 212222230014.        \n')
### END CODE HERE ###
```
### GRADED FUNCTION: convolutional_model:

### Network Model:

```
def convolutional_model():
    """Returns the compiled (but untrained) convolutional model.

    Returns:
        tf.keras.Model: The model which should implement convolutions.
    """

    ## START CODE HERE ###

    # Define the model
    model = tf.keras.models.Sequential([

    # Add convolutions and max pooling
    tf.keras.Input(shape=(28,28,1)),
    tf.keras.layers.Conv2D(64, (3,3), activation='relu'),
    tf.keras.layers.MaxPooling2D(2, 2),
    tf.keras.layers.Conv2D(64, (3,3), activation='relu'),
    tf.keras.layers.MaxPooling2D(2,2),

    # Add the same layers as before
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])

    ### END CODE HERE ###

    # Compile the model
    model.compile(
		optimizer='adam',
		loss='sparse_categorical_crossentropy',
		metrics=['accuracy']
	)
    return model
```
### Model Summary:
```
model.summary()
```
```
### Model compiling and Training

# Define your compiled (but untrained) model
model = convolutional_model()

# Train your model (this can take up to 5 minutes)
training_history = model.fit(training_images, training_labels, epochs=10, callbacks=[EarlyStoppingCallback()])
```

## OUTPUT

### Reshape and Normalize output:

![image](https://github.com/user-attachments/assets/cf3a5ba1-e70b-4a03-ab32-4745172ccd96)

### Model Summary:

![image](https://github.com/user-attachments/assets/d46a4f40-1d21-4c5f-ade2-03adc2a08b53)

### Training the model output:

![image](https://github.com/user-attachments/assets/51951ed1-1617-4f45-97c7-bd1c5f2d9ab4)

## RESULT:
Thus the program to create a Convolution Neural Network to classify images is successfully implemented.
