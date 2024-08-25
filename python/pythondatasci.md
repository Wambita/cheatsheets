# **Data Science with Python Cheatsheet**

## **1. Introduction to Data Science**

### **1.1. What is Data Science?**
- **Description:** Data Science involves extracting insights and knowledge from data using various techniques, including statistical analysis, machine learning, and data visualization.

### **1.2. Key Libraries and Tools**
- **Pandas:** Data manipulation and analysis.
- **NumPy:** Numerical computing.
- **Matplotlib / Seaborn:** Data visualization.
- **Scikit-Learn:** Machine learning.
- **Jupyter Notebook:** Interactive development environment.

## **2. Data Manipulation with Pandas**

### **2.1. Loading Data**
- **Description:** Import data from various formats.
  ```python
  import pandas as pd

  # Load CSV file
  data = pd.read_csv('data.csv')

  # Load Excel file
  data = pd.read_excel('data.xlsx')
  ```

### **2.2. Data Inspection**
- **Description:** Inspect and understand the structure of the data.
  ```python
  # Display the first few rows
  print(data.head())

  # Summary statistics
  print(data.describe())

  # Data types of columns
  print(data.dtypes)
  ```

### **2.3. Data Cleaning**
- **Description:** Handle missing values and outliers.
  ```python
  # Fill missing values
  data.fillna(value=0, inplace=True)

  # Drop missing values
  data.dropna(inplace=True)

  # Remove duplicates
  data.drop_duplicates(inplace=True)
  ```

### **2.4. Data Transformation**
- **Description:** Transform data for analysis.
  ```python
  # Filter data
  filtered_data = data[data['column'] > value]

  # Group data
  grouped_data = data.groupby('column').mean()

  # Apply function to column
  data['new_column'] = data['column'].apply(lambda x: x * 2)
  ```

## **3. Data Visualization**

### **3.1. Basic Plotting with Matplotlib**
- **Description:** Create basic plots like line graphs and bar charts.
  ```python
  import matplotlib.pyplot as plt

  # Line plot
  plt.plot(data['x'], data['y'])
  plt.xlabel('X-axis')
  plt.ylabel('Y-axis')
  plt.title('Line Plot')
  plt.show()

  # Bar plot
  plt.bar(data['x'], data['y'])
  plt.xlabel('X-axis')
  plt.ylabel('Y-axis')
  plt.title('Bar Plot')
  plt.show()
  ```

### **3.2. Advanced Plotting with Seaborn**
- **Description:** Create more complex plots and statistical visualizations.
  ```python
  import seaborn as sns

  # Scatter plot
  sns.scatterplot(x='x', y='y', data=data)
  plt.title('Scatter Plot')
  plt.show()

  # Heatmap
  sns.heatmap(data.corr(), annot=True)
  plt.title('Heatmap')
  plt.show()
  ```

## **4. Exploratory Data Analysis (EDA)**

### **4.1. Summary Statistics**
- **Description:** Compute statistical summaries to understand the data.
  ```python
  print(data.describe())
  print(data['column'].value_counts())
  ```

### **4.2. Correlation Analysis**
- **Description:** Analyze relationships between variables.
  ```python
  correlation_matrix = data.corr()
  print(correlation_matrix)
  ```

### **4.3. Distribution Analysis**
- **Description:** Understand the distribution of variables.
  ```python
  sns.histplot(data['column'], kde=True)
  plt.title('Distribution of Column')
  plt.show()
  ```

## **5. Machine Learning with Scikit-Learn**

### **5.1. Model Building**
- **Description:** Build and train machine learning models.
  ```python
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LogisticRegression

  # Split data
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

  # Initialize model
  model = LogisticRegression()

  # Train model
  model.fit(X_train, y_train)
  ```

### **5.2. Model Evaluation**
- **Description:** Evaluate the performance of machine learning models.
  ```python
  from sklearn.metrics import accuracy_score, classification_report

  # Make predictions
  y_pred = model.predict(X_test)

  # Evaluate model
  accuracy = accuracy_score(y_test, y_pred)
  print(f"Accuracy: {accuracy}")
  print(classification_report(y_test, y_pred))
  ```

### **5.3. Hyperparameter Tuning**
- **Description:** Optimize model parameters for better performance.
  ```python
  from sklearn.model_selection import GridSearchCV

  param_grid = {
      'C': [0.1, 1, 10],
      'solver': ['liblinear', 'saga']
  }

  grid_search = GridSearchCV(LogisticRegression(), param_grid, cv=5)
  grid_search.fit(X_train, y_train)
  print(f"Best parameters: {grid_search.best_params_}")
  ```

## **6. Advanced Data Science Concepts**

### **6.1. Feature Engineering**
- **Description:** Create and select features to improve model performance.
  ```python
  from sklearn.preprocessing import StandardScaler

  scaler = StandardScaler()
  X_scaled = scaler.fit_transform(X)
  ```

### **6.2. Dimensionality Reduction**
- **Description:** Reduce the number of features while retaining important information.
  - **Principal Component Analysis (PCA):**
    ```python
    from sklearn.decomposition import PCA

    pca = PCA(n_components=2)
    X_pca = pca.fit_transform(X)
    ```

### **6.3. Time Series Analysis**
- **Description:** Analyze and forecast time-dependent data.
  ```python
  import statsmodels.api as sm

  # Fit ARIMA model
  model = sm.tsa.ARIMA(data['value'], order=(1, 1, 1))
  results = model.fit()
  ```

### **6.4. Big Data Tools**
- **Description:** Handle large-scale data processing.
  - **Dask:**
    ```python
    import dask.dataframe as dd

    dask_df = dd.read_csv('large_data.csv')
    result = dask_df.groupby('column').mean().compute()
    ```

## **7. Data Science Workflow**

### **7.1. Data Collection**
- **Description:** Gather data from various sources, including APIs and databases.
  ```python
  import requests

  response = requests.get('https://api.example.com/data')
  data = response.json()
  ```

### **7.2. Data Cleaning**
- **Description:** Prepare and clean data for analysis.
  ```python
  data.dropna(inplace=True)
  ```

### **7.3. Data Analysis**
- **Description:** Perform exploratory data analysis and derive insights.
  ```python
  print(data.groupby('category').mean())
  ```

### **7.4. Model Development**
- **Description:** Build and evaluate predictive models.
  ```python
  model = RandomForestClassifier()
  model.fit(X_train, y_train)
  ```

### **7.5. Reporting**
- **Description:** Communicate findings and results using reports and visualizations.
  ```python
  import matplotlib.pyplot as plt

  plt.bar(data['category'], data['value'])
  plt.show()
  ```