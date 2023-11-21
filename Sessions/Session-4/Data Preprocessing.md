# Data Preprocessing :

`Encode categorical variables:`

There are plenty of methods to encode categorical variables into numeric and each method comes with its own advantages and disadvantages.

To discover them, we will see the following ways to encode categorical variables:

1. One-hot/dummy encoding
2. Label / Ordinal encoding
3. Target encoding
4. Frequency / count encoding
5. Binary encoding
6. Feature Hashing

**In machine learning, there are two main types of categorical data:**

**Nominal(label) Categorical Data:** Nominal variables represent categories without any specific order or ranking between them. The categories are simply distinct groups. Examples of nominal categorical data include gender (e.g., “Male” and “Female”), country of origin (e.g., “USA,” “UK,” “Germany”), or product categories (e.g., “Electronics,” “Clothing,” “Books”). Nominal variables are often represented using one-hot encoding.

**Ordinal Categorical Data:** Ordinal variables represent categories that have a natural order or ranking between them. The categories can be ranked based on some criteria or scale. Examples of ordinal categorical data include education level (e.g., “High School,” “Bachelor’s Degree,” “Master’s Degree”), customer satisfaction rating (e.g., “Very Satisfied,” “Satisfied,” “Neutral,” “Dissatisfied,” “Very Dissatisfied”), or economic status (e.g., “Low Income,” “Middle Income,” “High Income”).

![Untitled](Data%20Preprocessing%20185ff11628fc4c2da7b96d7b73d0b527/Untitled.png)

**Ordinal Encoding:**

Ordinal encoding assigns each unique value to a different integer.

![https://miro.medium.com/v2/resize:fit:563/1*LcFOqopX2KRFt3f4pGHM_g.png](https://miro.medium.com/v2/resize:fit:563/1*LcFOqopX2KRFt3f4pGHM_g.png)

This approach assumes an ordering of the categories: “ lowerlevel” (0) < “ MiddleSchool” (1) < “ HighSchool” (2).

### **Example For Limitation of Label Encoding**

An attribute having output classes **Mexico, Paris, Dubai**. On Label Encoding, this column lets **Mexico** is replaced with *0*, **Paris** is replaced with *1*, and **Dubai** is replaced with 2.

With this, it can be interpreted that **Dubai** has high priority than **Mexico** and **Paris** while training the model, But actually, there is no such priority relation between these cities here.

**One-Hot Encoding:**

One-Hot Encoding is a technique used to transform categorical variables into a binary representation, where each category is converted into a binary column. It creates new columns for each unique category and assigns a value of 1 or 0 to indicate the presence or absence of that category in a particular row.

Here’s an example code snippet that demonstrates how to perform one-hot encoding using both pandas and scikit-learn libraries in Python

**get_dummies (pandas) vs OneHotEncoder (scikit-learn)  :** 

Saving exploded categories is extremely useful when I want to apply the same data pre-processing on my test set. If the total number of unique values in a categorical column is not the same for my train set vs test set, I’m going to have problems.

For example on the training dataframe, when I apply get_dummies() on the ‘Call_Me?’ column; I return 3 new columns because there are 3 unique values. However, on the testing dataframe, I only have 2 unique values under the ‘Call_Me?’ column and therefore get_dummies() returns only 2 new columns.

![https://miro.medium.com/v2/resize:fit:700/1*jsz9HJS8TW6DadZKEXOAhA.png](https://miro.medium.com/v2/resize:fit:700/1*jsz9HJS8TW6DadZKEXOAhA.png)

Moreover, I’ll have errors when I fit a model on the training set and predict on my test features of different shape.

![https://miro.medium.com/v2/resize:fit:700/1*BLE-GN9fu1AehjLI69UZPg.png](https://miro.medium.com/v2/resize:fit:700/1*BLE-GN9fu1AehjLI69UZPg.png)

OneHotEncoder can transform the test dataframe from the saved exploded categories I fit on the training set.

![https://miro.medium.com/v2/resize:fit:700/1*WeFzWwmeAyRqXuBY4h5OLw.png](https://miro.medium.com/v2/resize:fit:700/1*WeFzWwmeAyRqXuBY4h5OLw.png)

Moreover, the ohe object has attributes to look for the saved exploded categories.

![https://miro.medium.com/v2/resize:fit:431/1*TxVmqRb9fyVL0wJAzkYGaQ.png](https://miro.medium.com/v2/resize:fit:431/1*TxVmqRb9fyVL0wJAzkYGaQ.png)

# **Conclusion**

For quick data cleaning and EDA, it makes a lot of sense to use pandas get dummies. However, if I plan to transform a categorical column to multiple binary columns for machine learning, it’s better to use OneHotEncoder().

**`NaN values Missingvalues :`**

Handling missing data: Decide how to deal with missing values, whether by imputation or removal.

## **Data Imputation Techniques**

Moving on to the main highlight of this article – techniques used in data imputation.

![https://editor.analyticsvidhya.com/uploads/30381Imputation%20Techniques%20types.JPG](https://editor.analyticsvidhya.com/uploads/30381Imputation%20Techniques%20types.JPG)

- **Z-Score:** Calculate the Z-score for each data point. Z-score measures how many standard deviations a data point is from the mean. Typically, a Z-score above a certain threshold (e.g., 2 or 3) indicates an outlier.

[![Untitled](Data%20Preprocessing%20185ff11628fc4c2da7b96d7b73d0b527/Untitled%201.png)
](https://github.com/wissemkarous/Machine_Learning-Documentation-GDSC/blob/f654b309f71c955b8aca6a3b0f0734e49815eab9/Sessions/Session-4/Data%20Preprocessing/Untitled%201.png)
[https://www.notion.so](https://www.notion.so)

- **IQR (Interquartile Range):** Calculate the IQR (the range between the first quartile Q1 and the third quartile Q3). Data points beyond a certain range outside of Q1 and Q3 can be considered outliers.
1. **Normalization:**
    - **Objective:** The goal of normalization is to scale the input features to a standard range, typically between 0 and 1.
    - **Method:** For each feature, the minimum value is subtracted, and then the result is divided by the range (difference between the maximum and minimum values).
    
    **Formula:** 
    
    ![Untitled](Data%20Preprocessing%20185ff11628fc4c2da7b96d7b73d0b527/Untitled%202.png)
    
    - **Benefits:**
        - Ensures that all features have the same scale.
        - Helps the optimization algorithm converge faster.
        - Reduces sensitivity to the scale of input features.
2. **Standardization:**
    - **Objective:** The goal of standardization is to transform the data to have zero mean and a standard deviation of 1.
    - **Method:** For each feature, the mean is subtracted, and then the result is divided by the standard deviation.
    
    **Formula:**
    
    ![Untitled](Data%20Preprocessing%20185ff11628fc4c2da7b96d7b73d0b527/Untitled%203.png)
    
    - **Benefits:**
        - Centers the data around zero, making it easier to learn the weights.
        - Helps when features have different units or magnitudes.
        - Generally, works well when the data follows a Gaussian distribution.
