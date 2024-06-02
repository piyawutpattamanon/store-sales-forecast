Thank you for your time spending with us. We are happy to move you forward to the Take Home Assignment stage. 

Please check the file as attached in this email and select either problem #1 or #2 to complete the assignment. You can follow the instruction as stated in the file.

After completing your assignment, please submit your work using the following format: 
1. Please use Jupyter notebook for all the code 
2. Make sure they are clean, well-structured, well-documented and are able to run without errors from start to finish 
3. If you need to output some additional files such as visualization videos, please package the notebook and other files together in a zip.

Submission deadline: within 7 days after you receive this email, and submit in the link at the bottom of this email called "Please submit here".

Enjoy doing the project!

=======


Problem #2 DATA SCIENCE: You’re a Data Scientist and a client from Ecuador has requested
you to build a predictive model that accurately forecasts product sales. They currently rely on
subjective forecasting methods with very little data to back them up and very little automation to execute plans. They’re excited to see how machine learning could better ensure that they
please customers by having just enough of the right products at the right time. For this task, you
are expected to predict the unit sales for thousands of items sold at different client-owned stores
located in Ecuador. The training data in the sample dataset, provided by the client, includes
dates, store and item information, whether that item was being promoted, as well as the unit
sales. The client has also provided you with additional files containing the details of the stores,
items, sales transactions, oil price and holiday events in Ecuador that might be helpful in
building the predictive model. The sample dataset can be downloaded from here. Please refer
to the README file, attached within, for detailed information on the dataset. For evaluating your
model, consider the approach of splitting the given dataset into a training and a testing period.
You can use the testing period to evaluate the performance of your model.

Evaluation Criteria
For the assignment that you choose, you will be tested on:
1. EDA and Conclusions: Conduct an in-depth EDA on the chosen dataset and draw
actionable insights. Reflect these insights in your feature engineering and modeling choices.
2. Development: Develop an appropriate algorithm/model using the chosen dataset. Justify
your choices for your model/algorithm of choice, data splitting, and hyperparameter tuning.
Discuss the trade-offs involved.
3. Evaluation: Clearly explain your evaluation criteria and the metrics of choice to gauge your
algorithm/model's performance using these metrics. Discuss any issues encountered, such as
overfitting or underfitting, lack of data, and how you mitigated them.
4. Documentation: Maintain thorough code documentation, including docstrings and inline
comments. Good documentation includes not just what the code does, but why it does it.
5. Reasoning: As you work through your chosen problem, articulate your thought process.
Explain the rationale behind your actions, your interpretations of the results, and your future
steps.
Submission Format
After completing your assignment, please submit your work using the following format:
● Please use Jupyter notebook for all the code
● Make sure they are clean, well-structured, well-documented and are able to run without
errors from start to finish
● If you need to output some additional files such as visualization videos, please package
the notebook and other files together in a zip.



# Dataset Description

In this assignment, you will be predicting the unit sales for thousands of items sold at different client-owned stores located in Equador. The training data includes dates, store and item information, whether that item was being promoted, as well as the unit sales. Additional files include supplementary information that may be useful in building your models.

## File Descriptions and Data Field Information

### train.csv

* Training data, which includes the target `unit_sales` by date, `store_nbr`, and `item_nbr` and a unique `id` to label rows.
* The target `unit_sales` can be integer (e.g., a bag of chips) or float (e.g., 1.5 kg of cheese).
* Negative values of `unit_sales` represent returns of that particular item.
* The `onpromotion` column tells whether that `item_nbr` was on promotion for a specified `date` and `store_nbr`.
* Approximately 16% of the `onpromotion` values in this file are `NaN`.

* Example Rows
```json
[{
  "id": "7031428",
  "date": "2013-06-16",
  "store_nbr": "11",
  "item_nbr": "1047703",
  "unit_sales": "29.0",
  "onpromotion": null
}, {
  "id": "7053621",
  "date": "2013-06-16",
  "store_nbr": "41",
  "item_nbr": "819206",
  "unit_sales": "0.538",
  "onpromotion": null
}, {
  "id": "34912861",
  "date": "2014-11-10",
  "store_nbr": "13",
  "item_nbr": "807493",
  "unit_sales": "41.0",
  "onpromotion": "False"
}, {
  "id": "34942212",
  "date": "2014-11-10",
  "store_nbr": "40",
  "item_nbr": "1239862",
  "unit_sales": "2.265",
  "onpromotion": "True"
}]
```

### stores.csv

* Store metadata, including `city`, `state`, `type`, and `cluster`.
* `cluster` is a grouping of similar stores.

* Example Rwos
```csv
item_nbr,family,class,perishable
96995,GROCERY I,1093,0
99197,GROCERY I,1067,0
103501,CLEANING,3008,0
103520,GROCERY I,1028,0
103665,BREAD/BAKERY,2712,1
```

### items.csv

* Item metadata, including `family`, `class`, and `perishable`.
* **NOTE**: Items marked as `perishable` have a score weight of `1.25`; otherwise, the weight is `1.0`.

### transactions.csv

* The count of sales transactions for each `date`, `store_nbr` combination. Only included for the training data timeframe.

* Example Rows
```csv
date,store_nbr,transactions
2013-01-01,25,770
2013-01-02,1,2111
2013-01-02,2,2358
2013-01-02,3,3487
2013-01-02,4,1922
```

### oil.csv

* Daily oil price.

* Example Rows
```csv
date,dcoilwtico
2013-01-01,
2013-01-02,93.14
2013-01-03,92.97
2013-01-04,93.12
2013-01-07,93.2
2013-01-08,93.21
```

### holidays_events.csv

* Holidays and Events, with metadata
* **NOTE**: Pay special attention to the transferred column. A holiday that is transferred officially falls on that calendar day, but was moved to another date by the government. A transferred day is more like a normal day than a holiday. To find the day that it was actually celebrated, look for the corresponding row where type is Transfer. For example, the holiday Independencia de Guayaquil was transferred from 2012-10-09 to 2012-10-12, which means it was celebrated on 2012-10-12. Days that are type Bridge are extra days that are added to a holiday (e.g., to extend the break across a long weekend). These are frequently made up by the type Work Day which is a day not normally scheduled for work (e.g., Saturday) that is meant to payback the Bridge.
* Additional holidays are days added a regular calendar holiday, for example, as typically happens around Christmas (making Christmas Eve a holiday).

### Additional Notes

* Wages in the public sector are paid every two weeks on the 15 th and on the last day of the month. Supermarket sales could be affected by this.
* A magnitude 7.8 earthquake struck Ecuador on April 16, 2016. People rallied in relief efforts donating water and other first need products which greatly affected supermarket sales for several weeks after the earthquake.

* Example Rwos
```csv
date,type,locale,locale_name,description,transferred
2012-03-02,Holiday,Local,Manta,Fundacion de Manta,False
2012-04-01,Holiday,Regional,Cotopaxi,Provincializacion de Cotopaxi,False
2012-04-12,Holiday,Local,Cuenca,Fundacion de Cuenca,False
2012-04-14,Holiday,Local,Libertad,Cantonizacion de Libertad,False
```
