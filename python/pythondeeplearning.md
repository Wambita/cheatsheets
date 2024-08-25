# **Deep Learning with Python Cheatsheet**

## **1. Introduction to Deep Learning**

### **1.1. What is Deep Learning?**
- **Description:** Deep Learning is a subset of machine learning that uses neural networks with many layers to model complex patterns and data representations.

### **1.2. Key Libraries**
- **TensorFlow / Keras:** High-level libraries for building and training deep learning models.
- **PyTorch:** A deep learning library that provides flexibility and control for model development.

## **2. Neural Networks**

### **2.1. Basic Concepts**
- **Neural Network:** Composed of layers of neurons (nodes) where each neuron is connected to the next layer.
- **Activation Function:** Determines whether a neuron should be activated or not (e.g., ReLU, Sigmoid).

### **2.2. Building a Neural Network with Keras**
- **Description:** Create a simple feedforward neural network.
  ```python
  from tensorflow.keras.models import Sequential
  from tensorflow.keras.layers import Dense

  # Create a neural network model
  model = Sequential([
      Dense(64, activation='relu', input_shape=(X_train.shape[1],)),
      Dense(32, activation='relu'),
      Dense(1, activation='sigmoid')
  ])

  # Compile the model
  model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])

  # Train the model
  model.fit(X_train, y_train, epochs=10, batch_size=32, validation_split=0.2)
  ```

### **2.3. Building a Neural Network with PyTorch**
- **Description:** Create a simple feedforward neural network.
  ```python
  import torch
  import torch.nn as nn
  import torch.optim as optim

  class SimpleNN(nn.Module):
      def __init__(self):
          super(SimpleNN, self).__init__()
          self.fc1 = nn.Linear(input_size, 64)
          self.fc2 = nn.Linear(64, 32)
          self.fc3 = nn.Linear(32, 1)
          self.relu = nn.ReLU()
          self.sigmoid = nn.Sigmoid()

      def forward(self, x):
          x = self.relu(self.fc1(x))
          x = self.relu(self.fc2(x))
          x = self.sigmoid(self.fc3(x))
          return x

  model = SimpleNN()
  criterion = nn.BCELoss()
  optimizer = optim.Adam(model.parameters(), lr=0.001)

  # Training loop
  for epoch in range(num_epochs):
      model.train()
      optimizer.zero_grad()
      outputs = model(X_train)
      loss = criterion(outputs, y_train)
      loss.backward()
      optimizer.step()
  ```

## **3. Advanced Neural Networks**

### **3.1. Convolutional Neural Networks (CNNs)**
- **Description:** Specialized for processing grid-like data (e.g., images).
  ```python
  from tensorflow.keras.layers import Conv2D, MaxPooling2D, Flatten

  model = Sequential([
      Conv2D(32, (3, 3), activation='relu', input_shape=(64, 64, 3)),
      MaxPooling2D(pool_size=(2, 2)),
      Flatten(),
      Dense(128, activation='relu'),
      Dense(10, activation='softmax')
  ])
  ```

### **3.2. Recurrent Neural Networks (RNNs)**
- **Description:** Specialized for sequential data (e.g., time series, text).
  ```python
  from tensorflow.keras.layers import SimpleRNN, Embedding

  model = Sequential([
      Embedding(input_dim=vocab_size, output_dim=128),
      SimpleRNN(64),
      Dense(1, activation='sigmoid')
  ])
  ```

### **3.3. Long Short-Term Memory (LSTM)**
- **Description:** A type of RNN that can learn long-term dependencies.
  ```python
  from tensorflow.keras.layers import LSTM

  model = Sequential([
      Embedding(input_dim=vocab_size, output_dim=128),
      LSTM(64),
      Dense(1, activation='sigmoid')
  ])
  ```

## **4. Model Evaluation and Optimization**

### **4.1. Model Evaluation**
- **Description:** Assess model performance using metrics like accuracy, precision, recall, and F1 score.
  ```python
  from sklearn.metrics import classification_report

  y_pred = model.predict(X_test)
  print(classification_report(y_test, y_pred))
  ```

### **4.2. Hyperparameter Tuning**
- **Description:** Optimize model parameters to improve performance.
  - **Grid Search:**
    ```python
    from sklearn.model_selection import GridSearchCV

    param_grid = {
        'batch_size': [16, 32],
        'epochs': [10, 20]
    }

    grid_search = GridSearchCV(estimator=model, param_grid=param_grid, cv=3)
    grid_search.fit(X_train, y_train)
    ```

### **4.3. Regularization**
- **Description:** Techniques to prevent overfitting.
  - **Dropout:**
    ```python
    from tensorflow.keras.layers import Dropout

    model = Sequential([
        Dense(64, activation='relu', input_shape=(input_dim,)),
        Dropout(0.5),
        Dense(1, activation='sigmoid')
    ])
    ```

## **5. Deep Learning Workflow**

### **5.1. Data Preprocessing**
- **Description:** Prepare data for training by scaling, normalization, and augmentation.
  ```python
  from sklearn.preprocessing import StandardScaler
  from tensorflow.keras.preprocessing.image import ImageDataGenerator

  # Standardize features
  scaler = StandardScaler()
  X_scaled = scaler.fit_transform(X)

  # Image augmentation
  datagen = ImageDataGenerator(rotation_range=20, width_shift_range=0.2)
  datagen.fit(X_train)
  ```

### **5.2. Training and Evaluation**
- **Description:** Train the model on the training set and evaluate on the test set.
  ```python
  model.fit(X_train, y_train, epochs=10, batch_size=32, validation_split=0.2)
  score = model.evaluate(X_test, y_test)
  ```

### **5.3. Saving and Loading Models**
- **Description:** Save the trained model for future use and load it when needed.
  ```python
  # Save the model
  model.save('model.h5')

  # Load the model
  from tensorflow.keras.models import load_model
  model = load_model('model.h5')
  ```