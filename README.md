# bmw_analysis_and_design


## Architecture overview 

![Initial draft of architecture](architecture.svg)

## Calculation lambda

## Midas API

## Core View integration

## Commission matrix file structure

## Sales volume targets file structure

## Parsing lambda

## Database design
Volume targets will be parsed into the VolumeTargets table. Commission matrixes will be parseed into the CommissionMatrixes table. Since the partition key does not uniquely identify an item, a composite key will be used.

![Initial draft of architecture](database.svg)


## Questions
- Will there be multiple markets in volume targets?
- In the Matrix dummy data, will the penetration rate and volume targets be uploaded with it? This will allow for arbitrary commission matrix to be uploaded. Otherwise I need to know the percentages in advance. --> 
- Will the target volume be in USD?