# bmw_analysis_and_design

## Projects score
- Commission paid retroactively for the previous month based on penetration rate and volume sales target achievement.
- Clawback of mentioned commission if the contract was canceled within a 6 month period.
- The new commissions should be paid out for FSM contracts (excluding Staff & Service Loaner contracts (product), Internal BMW Group Staff contracts, Prolongation andTransfer of Contract).


## Architecture overview 

![Initial draft of architecture](architecture.svg)

## Calculation lambda

## Midas API

## Core View integration

## Commission matrix file structure

## Sales volume targets file structure

## Parsing lambda
The parsing lambda will be triggered via an S3 Event Notificationm which occurs when a file is uploaded to the S3 bucket.

The lambda will:
- Identify if this file is a Comission Matrix file or a Target Sales Volum file. This will be done by checking the name of the file. It will follow a certain pattern depending on which file it is.
- Parse the data into DynamoDB.

**If it is an Comission Matrix file**:**
1. Load the data from the file with Pandas.

For every Matrix in the data:
2. Extract PenetrationRate ranges, put them in a list and reverse the list (alternatively it is reversed after reading from DynamoDB by the calculation lambda).
3. Extract AgentSalesTargetRate ranges and put them in a list.
4. Extract the matrix as a list of lists.
5. Construct a DynamoDB item according to the database schema.
6. Write the item to DynamoDB.

**If it is an Target Sales Volum file**:
1. Load the data from the file with Pandas.

For every record/row in the data:
2. Construct an item for every montly target of the agent in that record.
3. Write those items to DynamoDB using BatchWriteItem.

## Database design
Volume targets will be parsed into the VolumeTargets table. Commission matrixes will be parseed into the CommissionMatrixes table. Since the partition key does not uniquely identify an item, a composite key will be used. 

![Initial draft of architecture](database.svg)

The PenetrationRanges and VolumeTargetRanges attributes will be on the form
```python
ranges = [
    ["lower_bound_1", "upper_bound_1"],
    ["lower_bound_2", "upper_bound_2"],
    ["lower_bound_n", "upper_bound_n"],
]
```
Each range in the list representing a index to the right row or column in the matrix. The PenetrationRanges list will need to be reversed in order for the index or each range to represent the correct row in the matrix.


## Questions
- Will there be multiple markets in volume targets?
- In the Matrix dummy data, will the penetration rate and volume targets be uploaded with it? This will allow for arbitrary commission matrix to be uploaded. Otherwise I need to know the percentages in advance. --> 
- Will the target volume be in USD?