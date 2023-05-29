# Model-for-Predictive-Maintenance-using-Spark-DataFrame
The aim of the project is to classify whether there is a fault with a machine based on the readings from vibration sensors. The project utilizes the MLlib library in Spark to train four classification models while also using MLflow to track the experiment and monitor the model's performance
# **Dataset**
The dataset used in this project is called FaultDataset.csv. Each row in the dataset represents twenty vibration sensor readings, and the last column identifies whether there was a fault with the machine at the time of the readings. A value of 0 indicates no fault, while a value of 1 indicates a fault.

# **Note:** The dataset should be uploaded to the following location: `/FileStore/tables/FaultDataset.csv` on Databricks.

# **Project Steps**
The project follows these steps:

**1. Set Up:** The project was completed on Databricks Community Edition. A cluster and Python notebook were created to run the code. The cluster allows working with large data by distributing the work among nodes, improving performance. The notebook provides an interactive environment to execute the code. The dataset was uploaded into the Databricks File System (DBFS) to persist the file after the cluster termination. The Databricks runtime version was set at 12.1 ML to ensure access to the required libraries.

**2. Loading the Dataset:**  MLflow was imported, and auto logging was enabled to track experiments and automatically log metrics for different input parameters and outputs. The dataset, FaultDataset, was read into a Spark DataFrame called 'FaultsDF'. The header and inferSchema were set to 'true' to consider the first row as the header and automatically infer the data types. A quick check was performed to ensure the correctness of the inferred data types.

**3. Exploratory Analysis:**  The vibration data from the various sensors were visualized to understand their distribution. The majority of the values are less than 0.2.

   The correlation heat map indicates a positive correlation between vibrations in the production line, possibly due to vibration transmission or mechanical connections. Scatter plot matrices also align with the heat map observation.
   
   For better visualization, the vibrations were put into bins. Data from sensors 1, 8, and 14 were visualized to gain insights. Results show that vibrations above 0.4 have a 97% chance of indicating a fault in the machine. More specifically, 97.5% of instances with vibrations between 0.447 and 0.658 indicate a fault, while 99.48% of vibrations between 0.658 and 0.87 indicate a fault.
   
   The box plot of the target variables using sensors 1, 8, and 14 shows some outliers in cases where there was no fault. This suggests that for machines without a fault, vibrations are usually less than 0.4. However, there were a few instances of vibrations up to 0.8 with no fault, and some instances of readings below 0.4 with a fault detected.

**4. Data Preparation and Pre-processing:**  Pre-processing steps were performed to identify missing values, duplicated values, class imbalance, outliers, etc. Analysis showed no missing values, and the classes were balanced. A total of 324 duplicated records were identified and removed during pre-processing before splitting the data for training and testing.

**5. Splitting the Data:** The dataset was split using a 75% and 25% ratio for training and testing, respectively.

**6. Training the Model and Selection of Hyperparameters:**  Four classifiers were initially used to train and make predictions. Due to size, only two were selected.  Default parameters were initially used, followed by tuning hyperparameters to improve the accuracy of the models.

**7. Model Evaluation:**  The model was evaluated using accuracy as the metric. However, other metrics such as precision, recall, and F1-score can be used to assess the model's effectiveness.

**8. MLflow Experiment Tracking:**  MLflow was used to track experiments and monitor the model's performance. Relevant parameters, metrics, and artifacts were logged to maintain a record of the experiments.

**9. Running the Code:** To run the code, follow these steps:
   -Create an account on databricks
   - Upload the FaultDataset.csv file to the location `/FileStore/tables/` on Databricks.
   - Open the IPython Notebook.
   - Click 'Run All' or Execute the notebook cells sequentially to load the dataset, perform exploratory analysis, pre-process the data, train the model, and evaluate its performance.
   - Import the necessary libraries and ensure that the Databricks environment has all the required dependencies installed.
   - Use appropriate Markdown cells and comments throughout the notebook to provide explanations and document the code.
   - A PDF file of the codes is also added for quick access.

# **Discussion of Result**
Results from the exploratory data analysis using vibration data from sensors 1 , 8 and 14 suggest that vibration readings above 0.4 have a 97% likelihood of indicating a fault in the machine. As vibrations increase above 0.6, the likelihood of fault detection approaches 100%.

In addition to the exploratory data analysis, four classification models were developed to analyze vibration data from the sensors and predict machine faults. MLflow was used to track experiments and identify the best model based on accuracy. The Random Forest model achieved the highest accuracy of 98.4% compared to other models.

It is important to note that the choice of the best model should consider evaluation metrics beyond accuracy, such as precision, recall, and F1-score. For example, a model with high accuracy but poor recall may fail to detect actual faults, leading to frequent breakdowns. Similarly, a model with poor precision may result in unnecessary maintenance costs and lost production opportunities.

To implement this predictive maintenance model, it needs to be integrated into the production line to continuously monitor vibrations and detect faults. This integration would provide several benefits to the company, including:
- Proactively fixing machines before they are damaged beyond repair.
- Sufficient time for maintenance planning, especially for machines with hard-to-find replacement parts.
- Optimized production and increased revenue by maintaining machines in better condition.
- Ensuring machines operate within recommended conditions, increasing their lifespan and reliability.
- Reducing costs associated with frequent breakdowns due to poor maintenance.
- Prioritizing maintenance schedules based on the severity of detected faults, avoiding multiple failures of critical machines.

Furthermore, periodic retraining of the model is essential to maintain its efficiency and accuracy over time.

