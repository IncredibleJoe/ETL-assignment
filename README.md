# DTSE Data Engineer (ETL) assignment

Data preparation takes place in the prepare_data function, whose argument is the path to a csv file with the required input data and starts by reading the file and creating a dataframe from it. The loading is followed by removing a column ("AGENCY") from the input file that the model does not interact with in any way and removing rows that have missing values. This is followed by checking that all the columns expected by the model are present in the input csv file. If they are not, the program exits and the event is logged. If the necessary columns are present, they are renamed so that their new names match the names of the columns expected by the model. Renaming is followed by converting the categorical variable ("ocean_proximity") to indicator variables and checking that all indicator variables are available. If not, the program populates these columns with all values equal to 0 and changes the data type of the column to make it less memory intensive. It then removes rows where the value "Null" occurs. From the dataframe prepared in this way, a new dataframe (df_features, y) is created, which contains only the columns needed to train the model - the input data and the expected value for a given row. These 2 dataframes are then the input for the train_test_split function. The prepare data function returns the output of the train_test_split function and the df_features dataframe.

The insert_dataframe_to_db function, whose input is the database name, table name, and dataframe. It has the task of inserting this dataframe into the database. If the insert operation is not successful the event is logged. In our particular case the sqlite module was used for demonstration reasons due to its simplicity.

The function demonstrate, whose inputs are the trained model, a dataframe with input data, the database name and the table name, calls the function predict (input is the model and the dataframe), which results in model-generated predictions. These predictions are added to the dataframe as a new column and the insert_dataframe_to_db function is called.



### Files
* `main.py` - sample script that generates and uses the model, prepares the data for model and insert them as well as the model predicitions to database
* `housing.db` - database
* `model.joblib` - the computed model 
* `housing.csv` - data file to process and apply a model to it for creating predictions
* `requirements.txt` - pip dependencies
