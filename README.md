# bmw_analysis_and_design


## Database Design
A file containing montly volume targets for each agent will be uploaded and parsed into the VolumeTargets table once a year. In addition, a file containing a commission matrix for each market will be uploaded and parsed into the CommissionMatrixes table, yearly.

![Initial draft of architecture](database.svg)



Questions:
- Will there be multiple markets in volume targets?
- In the Matrix dummy data, will the penetration rate and volume targets be uploaded with it? This will allow for arbitrary commission matrix to be uploaded. Otherwise I need to know the percentages in advance. --> 
- Will the target volume be in USD?