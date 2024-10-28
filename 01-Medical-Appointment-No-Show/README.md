# **Medical Appointment No-Show Dataset Analysis**

| Contents                                    |
| ------------------------------------------- |
| [Dataset Description](#Dataset-Description) |
| [Column Descriptions](#Column-Descriptions) |
| [EDA Questions](#EDA-Questions)             |
| [Data Wrangling](#Data-Wrangling)           |
| [Data Cleaning](#Data-Cleaning)             |
| [Data Visualization](#Data-Visualization)   |
| [Conclusion](#Conclusion)                   |
| [Built With](#Built-with)                   |

## Dataset Description
This dataset compiles data from 100,000 medical appointments in Brazil, focusing on the crucial question: do patients show up for their appointments? Each row encapsulates a range of patient characteristics, providing a foundation to identify patterns and predictors of appointment attendance. This analysis will utilize the available demographic and health-related variables to offer insights into patient behavior and appointment adherence.

## Column Descriptions
Each record includes several key details:
1. `PatientId`: Unique patient identifier.
2. `AppointmentID`: Unique appointment identifier.
3. `Gender`: Patient's gender, either Male or Female.
4. `AppointmentDay`: The actual day of the appointment when the patient visits the doctor.
5. `ScheduledDay`: The day the appointment was booked.
6. `Age`: Patient's age.
7. `Neighbourhood`: Location of the appointment.
8. `Scholarship`: Indicates enrollment in the Brazilian welfare program Bolsa Família (True or False).
9. `Hypertension`: Indicates if the patient has hypertension (True or False).
10. `Diabetes`: Indicates if the patient has diabetes (True or False).
11. `Alcoholism`: Indicates if the patient suffers from alcoholism (True or False).
12. `Handicap`: Indicates any disabilities (True or False).
13. `SMS_received`: Number of reminder SMS messages sent to the patient.
14. `No-show`: Indicates if the patient missed the appointment (True) or attended (False).

## EDA Questions
- Q1: How often do men go to hospitals/doctors appointments compared to women? Which of them is more likely to show up?
- Q2: Does receiving an SMS reminder affect whether a patient will show up? Is it correlated with the number of days before the appointment?
- Q3: Does having a scholarship influence attendance at hospital appointments? What are the age groups affected by this?
- Q4: Does having certain diseases/disabilities/medical conditions affect whether or not a patient may show up to their appointment?

## Data Wrangling
Our data can be found in the `noshowappointments-kagglev2-may-2016.csv` file provided in this repository, downloaded from [Kaggle](https://www.kaggle.com/datasets/joniarroba/noshowappointments).

## Data Cleaning
Data Exploration Summary
- The dataset consists of 110,519 entries, spanning 14 columns, with no missing or duplicated values, ensuring data quality for analysis.
- The `PatientId` and `AppointmentId` columns, serving solely as identifiers, will be excluded from the analysis to concentrate on more impactful predictors.

Inconsistencies in Data:
- The `Handcap` column exhibits values ranging from 0 to 4, suggesting varied levels of disability rather than a simple binary classification. This column will be simplified, with any value greater than 0 indicating the presence of a handicap.
- The `Age` column contains values beyond typical human lifespan, such as ages below 0 or as high as 115, indicating potential data entry errors. These entries will be corrected or removed to maintain data integrity.

Data Type Conversions and Feature Engineering:
- `ScheduledDay` and `AppointmentDay` will be converted to datetime data types, enabling precise time-based calculations.
- A new feature, `DaysUntilAppointment`, will be created to measure the interval between the scheduling date and the appointment date, providing insights into patient commitment and planning behaviors.
- The `Gender` column will be converted into a categorical data type to optimize processing efficiency.
- Boolean conversions will be applied to `Scholarship`, `Hipertension`, `Diabetes`, `Alcoholism`, and `SMS_received`, reflecting their true/false nature more accurately.
- The `No-show` column will be parsed and converted to a boolean format where 'No' (patient attended) is False and 'Yes' (patient missed) is True. This will simplify analyses focusing on patient attendance.

Exploratory Data Analysis Enhancements:
- A deeper review of what each category in the `Handcap` column represents might be necessary to decide if a more detailed classification could be beneficial for certain types of analysis.
- The transformation of the `SMS_received` column to a boolean reflects the receipt of SMS as a True/False condition, simplifying the investigation of its impact on patient no-show rates.


## Data Visualization
Using `Plotly`, we have created several informative charts to help analyze correlations between dataset attributes.

## Conclusion
Q1: How often do men go to doctors' appointments compared to women? Which one is more likely to show up?
- More than half of our dataset consists of women, who exhibit a wider age distribution with some outliers. They achieve a higher attendance rate than men.
- It is apparent that 79.8% of our patients attended their appointments while only 20.1% did not.
- Women are more likely to show up for their appointments than men, but this may be influenced by the higher percentage of women in this dataset.

Q2: Does receiving an SMS as a reminder affect whether or not a patient may show up? Is it correlated with the number of days before the appointment?
- 67.8% of our patients did not receive an SMS reminder for their appointments, yet they showed up.
- There is a clear positive correlation between the number of days before an appointment and attendance.
- Patients with appointments scheduled from 0 to 30 days tend to show up more consistently, while those with longer wait times are more likely to miss their appointments.
- Gender does not significantly impact the number of days due before an appointment or attendance rates.

Q3: Does having a scholarship affect showing up for a hospital appointment? What are the age groups affected by this?
- Having a scholarship does not significantly influence attendance at doctor appointments.
- A large age group is enrolled in the scholarship program, which also includes their children.

Q4: Does having certain medical conditions affect whether or not a patient may show up for their appointment?
- We can conclude that the vast majority of our dataset does not have chronic diseases; however, these conditions are present in many young people.
- Having a chronic disease may influence a patient's likelihood of attending a hospital appointment.

## Built With
- Jupyter Notebook
- Python3
- Pandas
- Numpy
- Plotly