# Time Series Datasets for CBOR Templates.

This repository shows the performance evaluation for Static-based Time-Series (STS), Measurements-based TS (MTS) and Variable-based TS (VTS) templates with various use-cases in different datasets.


## Performance evaluation.


The first 5 use-cases are based on datasets downloaded from [https://www.kaggle.com/datasets]. This datasets are presented in CSV files with raw data separated by comma. Thus, it is required to transform from raw data to a JSON format (This process was made manually). Finally to compare the data the following steps are needed:   


- Transform the JSON format into CBOR and review the amount of bytes required [https://cbor.me/].
- Transform to STS representation and review the amount of bytes required.
- Transform to MTS representation and review the amount of bytes required.
- Transform to VTS representation and review the amount of bytes required.

Furthermore, each folder of the repository contains 8 files:

- JSON_Format.txt : This is the JSON structure to perform the comparison.
- STS_Template.txt : This is the CBOR template (STS) to represent the JSON structure provided in JSON_Format.txt.
- STS_ArrayRequired.txt : This is the CBOR data item (Array) required to obtain the JSON_Format using STS_Template.
- MTS_Template.txt : This is the CBOR template (MTS) to represent the JSON structure provided in JSON_Format.txt.
- MTS_ArrayRequired.txt : This is the CBOR data item (Array) required to obtain the JSON_Format using MTS_Template.
- VTS_Template.txt : This is the CBOR template (VTS) to represent the JSON structure provided in JSON_Format.txt.
- VTS_ArrayRequired.txt : This is the CBOR data item (Array) required to obtain the JSON_Format using VTS_Template.
- PerformanceEvaluation.pdf : This is the image with the size in bytes of each payload (JSON transformed to CBOR, STS, MTS and VTS).

The following datasets are used in order to evaluate STS, MTS and VTS templates. To evaluate the amount of data reduced, and adaptability by each template the data sets where modified to represent less data, or different time where each measurement was taken.

### Data Set 1
This dataset corresponds to the first 1000 records of a IoT device sensing 5 variables (oxigen, humidity, light, and temperature) each 5 seconds. Taken from [https://www.kaggle.com/datasets/ranakrc/smart-building-system]

### Data Set 2
This dataset corresponds to the first 120 records of a IoT device sensing temperature of an entreprise building room each second. Taken from [https://www.kaggle.com/datasets/atulanandjha/temperature-readings-iot-devices]

### Data Set 3
This dataset correspond to the first 100 measurements of a electrophoresis painting plant with 7 sensor devices sensing every 10 seconds. Taken from [https://www.kaggle.com/datasets/boyangs444/process-data-for-predictive-maintenance, IIoT sensor readings]

### Data Set 4
This dataset correspond a variation of the data set #3. In this case, we modify the data set to only represent 2 sensor devices, and the measurements of each sensor devices are not at the same time ( the first variable only is sent half of the times than the second variable ). Moreover, use the same template as in data set #3 is required to evaluate the adaptability of each template. 

### Data Set 5
This dataset correspond a variation of the data set #3. In this case, we modify the data set to only represent the first measurement and only sent this value. Moreover, use the same template as in data set #3 is required to evaluate the adaptability of each template. 

### Data Set 6
This dataset correspond to dummy measures of an IoT sensor device sending two variables (temperature and humidity) 5 times.

### Data Set 7
This dataset correspond a variation of the data set #6. In this case, we modify the data set to only send one measurement of temperature. Moreover, use the same template as in data set #6 is required to evaluate the adaptability of each template. 

### Data Set 8
This dataset correspond a variation of the data set #6. In this case, we modify the data set to only send one measurement of humidity. Moreover, use the same template as in data set #6 is required to evaluate the adaptability of each template.

### Data Set 9
This dataset correspond a variation of the data set #6. In this case, we modify the data set to only send two measurements (2 values for humidity and 1 value for temperature). Moreover, use the same template as in data set #6 is required to evaluate the adaptability of each template. 

### Data Set 10
This dataset correspond a variation of the data set #6. In this case, we modify the data set to only send one measurement with both variables (temperature and humidity). Moreover, use the same template as in data set #6 is required to evaluate the adaptability of each template.

### Data Set 11
This dataset consists of the first 300 observations obtained from a GPS placed on a bicycle to promote cyclist safety in smart cities. The GPS system includes latitude, longitude, and velocity information, resulting in a total of 900 measurements. Taken from [[https://www.kaggle.com/datasets/boyangs444/process-data-for-predictive-maintenance](https://data.mendeley.com/datasets/3j9yh8znj4), First Route]
