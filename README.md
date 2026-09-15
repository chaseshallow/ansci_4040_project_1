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

### 6. Testing and Validation

To test the methods, I will use complete observations where the true values are already known.

For example, I can intentionally hide `AnimalNumber` from a sample of complete records:

`Complete Record → Hide AnimalNumber → Run Model → Predicted AnimalNumber → Compare with True AnimalNumber`

The same process can be performed for other variables:

`Known Value → Artificially Make it Missing → Predict Value → Compare Prediction with Known Value`

This will allow me to calculate how accurately each method recovers missing information before using it on records where the true answer is unknown.

For cow identification and categorical variables, performance could be evaluated using measures such as **percent correctly classified**. For continuous variables such as milk flow or session duration, prediction error can be measured by comparing predicted and actual values.

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
