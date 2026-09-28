# ansci_4040_project_1
ANSCI 4040 Data in Ag Project 1 repo
# Mini Project Plan

## Project Goal

The goal of this mini project is to develop a method for addressing **missing or unassigned cow-level data** in a dairy dataset. Some records are incomplete, meaning that information about the cow, lactation, reproduction, or milking session may be missing.

The variables with potentially missing information include:

* `AnimalNumber`
* `LactationNumber`
* `DaysInMilk`
* `ReproductionStatus`
* `AvgmilkflowFlow`
* `30_60Session`
* `YieldFirst2Min_SessionYield`
* `SessionDuration`
* `Session_secmilking`

The main objective is to determine whether the information that is still available in an incomplete record can be used to **identify the correct cow and recover or estimate the missing information**. The project will focus on making these assignments as accurately as possible rather than simply removing incomplete observations.

## Development Environment

The project will be completed **locally using Visual Studio Code (VS Code)**.

* **IDE:** Visual Studio Code
* **Analysis environment:** Jupyter Notebook within VS Code
* **Programming language:** Python
* **Version control:** Git and GitHub
* **Location:** Local computer

The Jupyter Notebook will be used for data exploration, cleaning, matching, modeling, testing, and visualization. The original dataset will remain unchanged so that all modifications can be reproduced through code.

## Project Strategy

### 1. Explore the Dataset

The first step will be to determine the amount and type of missing information.

Using Python in the Jupyter Notebook, I will identify:

* How many values are missing from each variable.
* Which cows have incomplete records.
* Which records are missing `AnimalNumber`.
* Whether multiple variables tend to be missing together.
* Whether missing data occur during particular lactations or stages of lactation.
* Whether there are patterns in when or where missing observations occur.

Data Cleaning and Preprocessing:

Before modeling, the dataset will be examined to identify data-quality problems that could interfere with the analysis.

The cleaning process will include:

Missing values (N/As)
Observations containing N/A values will initially be identified and excluded from the clean dataset used to train models. The original data will be preserved so that models can later be tested for their ability to predict missing values.

Zero values
Zero values will be examined to determine whether they represent legitimate measurements or missing/invalid observations. Invalid zeros will be excluded from the training dataset.

Repeated observations
Exact or inappropriate duplicate observations will be identified and removed so that repeated records do not artificially influence the models.

Outlier detection using Z-scores
Numerical variables will be standardized using Z-scores to identify unusually large or small observations. A starting threshold such as |Z| > 3 will be used to flag potential outliers. Flagged observations will be examined before exclusion so that biologically plausible extreme values are not automatically removed.

The result will be a clean dataset containing observations that can be used as reliable examples during model training.

This will help determine whether the missing information can be recovered directly or needs to be predicted.

### 2. Separate Identification and Prediction Problems

Not every missing variable should be handled in the same way.

Variables such as `AnimalNumber`, `LactationNumber`, and `DaysInMilk` may help establish **which cow and point in time an observation belongs to**.

Variables such as `AvgmilkflowFlow`, `YieldFirst2Min_SessionYield`, `SessionDuration`, and `Session_secmilking` describe the cow's milking session and may be candidates for prediction when the original value cannot be recovered.

`ReproductionStatus` may require using the cow's surrounding records and timeline to determine the most likely status.

Therefore, the project may require more than one method rather than using a single model for every missing value.

### 3. Matching Records to Cows

I will first investigate whether incomplete observations can be connected to known cows using the information that remains available.

Potential matching variables include:

* Lactation number
* Days in milk
* Reproduction status
* Milk flow
* Session yield
* Session duration
* Milking time
* Previous and following observations

I will begin with **rule-based matching** and similarity between records. If multiple cows could match an observation, I will investigate statistical or machine-learning approaches that calculate which cow is the most likely match.

Assignments should also include a measure of confidence so that uncertain records are not automatically assigned to a cow.

### 4. Filling Missing Values

Once the cow associated with a record is known, I will investigate methods for filling individual missing variables.

For values that change predictably over time, surrounding observations from the **same cow and lactation** may provide useful information. For example, Days in Milk should follow the cow's lactation timeline, while milk production and milking characteristics may be estimated using nearby sessions.

Potential methods include:

* Using previous and following records
* Interpolation
* Cow-specific averages
* Lactation-stage averages
* Regression
* Nearest-neighbor methods
* Other predictive models

The method used will depend on the variable being recovered.

### 5. Model Choice

I will begin with simpler and more interpretable approaches before testing more complicated models.

Potential approaches include:

* **Rule-based matching** for identifying cows using known characteristics.
* **Nearest-neighbor methods** for finding similar complete observations.
* **Regression models** for continuous variables such as milk flow, yield, or session duration.
* **Classification models** for categorical information such as reproduction status or cow identity.

Different approaches will be compared based on their ability to recover information that is already known in complete records.

Modeling Strategy for late stage project:

Multiple approaches will be tested rather than relying on a single method.

 Clustering

A clustering approach will be used to determine whether cows or milking sessions naturally separate into groups based on characteristics such as:

Lactation number

Days in Milk

Milk yield

Milk flow

Session duration

Reproduction status

Clusters may help identify cows with similar production patterns. If an observation has missing information, its cluster membership and similarity to other cows within that cluster may provide useful information for estimating the missing value.

 Model Tree

A tree-based model will be tested to determine whether combinations of known cow characteristics can predict variables that are missing or unassigned.

Tree-based approaches may be useful because relationships among lactation, Days in Milk, milk production, reproduction status, and milking characteristics may be nonlinear.

Model performance and interpretability will be evaluated to determine whether the resulting decision structure provides biologically meaningful predictions.

Missing-Data Prediction Model

The primary modeling objective will be to determine whether known information about a cow can be used to predict information that is missing.

For example, complete observations can be used to simulate the missing-data problem by intentionally hiding a known value. The model will then attempt to predict that value using the remaining variables.

This allows model predictions to be compared against the true known values, providing a direct way to measure whether the approach is accurate enough to use on genuinely missing observations.

Different algorithms can be compared depending on whether the missing variable is numerical or categorical.

### 6. Testing and Validation

The cleaned, complete observations will be divided using a 70/20/10 split:

70% Training Set — Used to train the models.

20% Validation Set — Used to compare models, tune parameters, select variables, and make modeling decisions.

10% Test Set — Held completely separate until the final model has been selected and used to estimate how well the approach performs on unseen data.

The split should be performed before model development to reduce the risk of data leakage.

If multiple observations come from the same cow, splitting individual rows randomly could place records from one cow in both the training and test sets. Therefore, when possible, the split will be performed at the cow level using AnimalNumber, so that all observations from a particular cow remain in only one partition. This will provide a more realistic test of whether the model generalizes to cows it has not previously seen.

### 7. Data Lineage

The original data will never be overwritten. All changes will be performed through Python in the Jupyter Notebook.

The workflow will follow:

`Raw Data → Identify Missing Values → Determine Missing Variable → Match Cow if Needed → Estimate/Recover Value → Validate → Final Dataset`

The final dataset should include information showing where each value came from. For example, values could be labeled as:

* `Original`
* `Recovered`
* `Predicted`
* `Unresolved`

This will preserve data lineage and make it possible to distinguish original measurements from values generated by the project.

## Timeline

| Date                | Goal                                                                                                                                                                              |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sept. 15–17**     | Set up the project in VS Code and GitHub. Load the dataset into the Jupyter Notebook and investigate the variables and structure.                                                 |
| **Sept. 18–22**     | Quantify missing values for `AnimalNumber`, `LactationNumber`, `DaysInMilk`, reproduction status, milk flow, yield, and session variables. Identify patterns in the missing data. |
| **Sept. 23–27**     | Develop initial methods for matching incomplete observations to cows and filling individual missing variables. Create test datasets by intentionally removing known values.       |
| **Sept. 28–Oct. 1** | Compare rule-based, nearest-neighbor, regression, and/or classification approaches. Evaluate how accurately each method recovers known values.                                    |
| **Oct. 2–4**        | Select the best methods and apply them to the actual missing data. Evaluate confidence, investigate questionable predictions, and document data lineage.                          |
| **Oct. 5–6**        | Run the entire Jupyter Notebook from beginning to end, finalize results and visualizations, update the README, and prepare the GitHub repository for submission.                  |

## Final Deliverable

By **October 6**, the GitHub repository will contain a reproducible Jupyter Notebook demonstrating a method for recovering missing or unassigned cow data.

The final project will show:

* Which variables contain missing information.
* How missing records were identified.
* How observations were matched to individual cows.
* How missing values were recovered or predicted.
* How prediction accuracy was tested.
* How confident the model is in its assignments.
* Which values are original versus predicted.

The overall goal is to recover as much useful cow-level information as possible while minimizing incorrect assignments and maintaining a clear record of how the final dataset was created.
