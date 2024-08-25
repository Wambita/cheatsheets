# **Machine Learning with Python Cheatsheet**

## **1. Basics of Machine Learning**

### **1.1. What is Machine Learning?**
- **Description:** Machine Learning (ML) is a subset of artificial intelligence (AI) that enables systems to learn and make decisions from data without explicit programming.

### **1.2. Libraries and Tools**
- **Description:** Essential libraries and tools for ML in Python.
  - **Scikit-Learn:** A library for traditional ML algorithms.
  - **Pandas:** Data manipulation and analysis.
  - **NumPy:** Numerical computing.
  - **Matplotlib / Seaborn:** Data visualization.
  - **TensorFlow / Keras / PyTorch:** Libraries for deep learning.

### **1.3. Data Preparation**
- **Description:** Preparing data for ML models, including cleaning, normalization, and splitting.
  ```python
  import pandas as pd
  from sklearn.model_selection import train_test_split

  # Load dataset
  data = pd.read_csv('data.csv')

  # Split into features and target
  X = data.drop('target', axis=1)
  y = data['target']

  # Split data into training and test sets
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
  ```

## **2. Machine Learning Models**

### **2.1. Linear Regression**
- **Description:** Predict a continuous target variable based on one or more features.
  ```python
  from sklearn.linear_model import LinearRegression
  from sklearn.metrics import mean_squared_error

  model = LinearRegression()
  model.fit(X_train, y_train)

  predictions = model.predict(X_test)
  mse = mean_squared_error(y_test, predictions)
  print(f"Mean Squared Error: {mse}")
  ```

### **2.2. Logistic Regression**
- **Description:** Predict a binary target variable.
  ```python
  from sklearn.linear_model import LogisticRegression
  from sklearn.metrics import accuracy_score

  model = LogisticRegression()
  model.fit(X_train, y_train)

  predictions = model.predict(X_test)
  accuracy = accuracy_score(y_test, predictions)
  print(f"Accuracy: {accuracy}")
  ```

### **2.3. Decision Trees**
- **Description:** Model that makes decisions based on feature values by creating a tree-like model.
  ```python
  from sklearn.tree import DecisionTreeClassifier
  from sklearn.metrics import accuracy_score

  model = DecisionTreeClassifier()
  model.fit(X_train, y_train)

  predictions = model.predict(X_test)
  accuracy = accuracy_score(y_test, predictions)
  print(f"Accuracy: {accuracy}")
  ```

### **2.4. Random Forests**
- **Description:** An ensemble method using multiple decision trees to improve performance.
  ```python
  from sklearn.ensemble import RandomForestClassifier
  from sklearn.metrics import accuracy_score

  model = RandomForestClassifier()
  model.fit(X_train, y_train)

  predictions = model.predict(X_test)
  accuracy = accuracy_score(y_test, predictions)
  print(f"Accuracy: {accuracy}")
  ```

### **2.5. Support Vector Machines (SVM)**
- **Description:** Classification algorithm that finds the optimal hyperplane to separate data points.
  ```python
  from sklearn.svm import SVC
  from sklearn.metrics import accuracy_score

  model = SVC()
  model.fit(X_train, y_train)

  predictions = model.predict(X_test)
  accuracy = accuracy_score(y_test, predictions)
  print(f"Accuracy: {accuracy}")
  ```

### **2.6. K-Nearest Neighbors (KNN)**
- **Description:** Classifies data based on the majority vote of its k-nearest neighbors.
  ```python
  from sklearn.neighbors import KNeighborsClassifier
  from sklearn.metrics import accuracy_score

  model = KNeighborsClassifier(n_neighbors=3)
  model.fit(X_train, y_train)

  predictions = model.predict(X_test)
  accuracy = accuracy_score(y_test, predictions)
  print(f"Accuracy: {accuracy}")
  ```

## **3. Advanced Machine Learning Concepts**

### **3.1. Feature Engineering**
- **Description:** Creating new features or modifying existing ones to improve model performance.
  ```python
  import pandas as pd
  from sklearn.preprocessing import StandardScaler

  # Feature scaling
  scaler = StandardScaler()
  X_scaled = scaler.fit_transform(X)
  ```

### **3.2. Hyperparameter Tuning**
- **Description:** Optimizing model parameters to improve performance.
  ```python
  from sklearn.model_selection import GridSearchCV

  param_grid = {
      'n_estimators': [10, 50, 100],
      'max_depth': [None, 10, 20]
  }

  grid_search = GridSearchCV(RandomForestClassifier(), param_grid, cv=5)
  grid_search.fit(X_train, y_train)
  print(f"Best parameters: {grid_search.best_params_}")
  ```

### **3.3. Cross-Validation**
- **Description:** Technique for assessing how the results of a statistical analysis will generalize to an independent data set.
  ```python
  from sklearn.model_selection import cross_val_score

  model = RandomForestClassifier()
  scores = cross_val_score(model, X, y, cv=5)
  print(f"Cross-validation scores: {scores}")
  ```

### **3.4. Ensemble Methods**
- **Description:** Combine predictions from multiple models to improve performance.
  - **Bagging:**
    ```python
    from sklearn.ensemble import BaggingClassifier

    model = BaggingClassifier(base_estimator=DecisionTreeClassifier(), n_estimators=50)
    model.fit(X_train, y_train)
    ```
  - **Boosting:**
    ```python
    from sklearn.ensemble import GradientBoostingClassifier

    model = GradientBoostingClassifier(n_estimators=100)
    model.fit(X_train, y_train)
    ```

### **3.5. Deep Learning**
- **Description:** Using neural networks with multiple layers to model complex patterns.
  - **Using TensorFlow/Keras:**
    ```python
    from tensorflow.keras.models import Sequential
    from tensorflow.keras.layers import Dense

    model = Sequential([
        Dense(64, activation='relu', input_shape=(X_train.shape[1],)),
        Dense(32, activation='relu'),
        Dense(1, activation='sigmoid')
    ])

    model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
    model.fit(X_train, y_train, epochs=10, batch_size=32)
    ```

### **3.6. Model Evaluation**
- **Description:** Assessing the performance of models using metrics like accuracy, precision, recall, and F1 score.
  ```python
  from sklearn.metrics import classification_report

  predictions = model.predict(X_test)
  print(classification_report(y_test, predictions))
  ```

### **3.7. Handling Imbalanced Data**
- **Description:** Techniques to handle datasets where classes are not equally represented.
  - **Resampling:**
    ```python
    from sklearn.utils import resample

    # Upsample minority class
    X_upsampled, y_upsampled = resample(X_minority, y_minority, replace=True, n_samples=len(y_majority), random_state=42)
    ```
  - **SMOTE (Synthetic Minority Over-sampling Technique):**
    ```python
    from imblearn.over_sampling import SMOTE

    smote = SMOTE()
    X_resampled, y_resampled = smote.fit_resample(X, y)
    ```