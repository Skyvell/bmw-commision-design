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
The parsing lambda will ta an in

Psueducode:
1. File gets uploaded to s3 bucket.
2. This triggers the parsing lambda.

Lambda:
1. Identify if this file is a matrix or sales volume target file. This could be done by checking the name of the file. The file-naming convention needs to be agree to in advance.

If the file is a matrix file:
1. Load the data file with Pandas.

For every matrix in file:
- Extract penetration ranges and put in a list: [[lower_bound, upper_bound], [lower_bound_n, upper bound]]. A range is on the form [lower_bound, upper_bound).
- Extract the matrix as a list of lists.
- Construct item and insert into DynamoDB.


## Database design
Volume targets will be parsed into the VolumeTargets table. Commission matrixes will be parseed into the CommissionMatrixes table. Since the partition key does not uniquely identify an item, a composite key will be used. 


![Initial draft of architecture](database.svg)

The PenetrationRanges and VolumeTargetRanges attributes will be on the form: 
```python
[[lower_bound_1, upper_bound_1],
[lower_bound_2, upper_bound_2],
              .
              .
[lower_bound_n, upper_bound_n]]
```
These are needed to find the right indexes for each range, in order to lockup the right element in the matrix.


## Questions
- Will there be multiple markets in volume targets?
- In the Matrix dummy data, will the penetration rate and volume targets be uploaded with it? This will allow for arbitrary commission matrix to be uploaded. Otherwise I need to know the percentages in advance. --> 
- Will the target volume be in USD?