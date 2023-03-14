# Time Series Datasets for CBOR Templates.

This repository shows the performance evaluation for Static-based Time-Series (STS), Measurements-based TS (MTS) and Variable-based TS (VTS) templates with various use-cases in different datasets.


# Table of Contents

- [Introduction](#introduction)
- [Performance Evaluation](#performance-evaluation)
- [Concise Data Definition Language](#concise-data-definition-language)


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



## Concise Data Definition Language


CDDL is a data definition language that was developed by the IETF to define data structures. The main purpose of CDDL is to provide a simple and expressive way to define data structures that are readable by humans and machines for protocol messages and data formats that use CBOR or JSON structures. One of the key features of CDDL is its expressiveness, which allows the definition of complex data structures with minimal code. Moreover, it supports various data types, such as integers, strings, and arrays, which makes it suitable for different applications. 

Furthermore, CDDL is designed to be extensible, allowing the addition of custom data types as needed. Additionally, CDDL allows to indicate the occurrence of a field, for example, whether it is required or optional. CDDL is used to define the data structures in CBOR or JSON. This enables a compact and efficient representation of sensor data, which facilitates its processing and interpretation. For instance, the following CDDL code defines a sensor measurement with a name, unit, and value, and indicates that the name field is required and the value field is optional.


```
Measurement = {
    + name: tstr,
    unit: tstr,
    ? value: float,
}
```

CDDL tools are capable of check a CDDL specifications for syntax problems, validate a data item instance against the CDDL specification created, generate a random data item from a specification created or generate random data items to verify the correct building of the specification.

Then in order to install one of the CDDL tools, first is necessary to install ruby:

- Please go to: https://stackify.com/install-ruby-on-ubuntu-everything-you-need-to-get-going/ as an example on how to install ruby on linux.

 If you are familiar with linux use the command:
```
sudo apt install ruby
```

Once you have installed ruby, use the following command to install the cddl tool
```
gem install cddl
```
Once you have installed the tool you can create a file with the specification of the data structure you want to validate and save it as a .cddl file.

For example to generate 10 data items with a file with the name foo.cddl it is necessary the next command:
```
cddl foo.cddl generate 10
```
If you need to validate a data structure in json format again your .cddl file:
```
cddl foo.cddl validate dataformat.json
```
or validate a CBOR data item would be
```
cddl foo.cddl validate dataformat.cbor
```

Once a cddl tool is installed, we are able to build the structure proposed in "Development of a Standardized Representation for IoT Time Series Data using CBOR Templates". The file is named "CBOR_Template_VTS.cddl" and contains the following code

```
; Definition of general array
template-array-vts = [
                          template-context, ; General Metadata
                        + data-values, ; Data values - One or more
                    ]

; Definition of template context
template-context = {
        0 : uint, ; Context per message
      ? general_metadata
    }

; Definition of general metadata
general_metadata = (
      0*1 1 : epoch, ; Epoch Time, If not present take as now()
      0*1 2 : uint, ; Difference in time in seconds, If not present default 60 seconds.
      0*1 3 : precision, ; Precision, If not present default 2
      0*1 4 : delta ; Difference with the subsequent value, If not present default 1: active and horizontal
)

; Definition of specific metadata
specific_metadata = (
      general_metadata,
      0*1 5 : unit ; Change of unit
)

; Definition of Data Values (Measurements)
data-values  = [
      0*1 {specific_metadata},
      + values: int
]

; Variable types definition
epoch = #6.1(number)

precision =  vp1 / vp2 / vp3 / vp4 / vp5 / vp6 / vp7 / vp8 / vp9 / vp10
vp1=1       ; Precision of 1  0,1 
vp2=2       ; Precision of 2  0,01
vp3=3       ; Precision of 3  0,001
vp4=4       ; Precision of 4  0,0001
vp5=5       ; Precision of 5  0,00001
vp6=6       ; Precision of 6  0,000001
vp7=7       ; Precision of 7  0,0000001
vp8=8       ; Precision of 8  0,00000001
vp9=9       ; Precision of 9  0,000000001
vp10=10     ; Precision of 10 0,0000000001

delta = vd1 / vd2 / vd3
vd1 = 1     ; difference with the subsequent value only horizontal
vd2 = 2     ; difference with the subsequent value horizontal and vertical
vd3 = 10    ; NO DELTA - Delta deactivated

unit = vu1 / vu2 / vu3 / vu4 / vu5 / vu6 / vu7 / vu8 / vu9 / vu10 / vu11 / vu12 / vu13 / vu14 / vu15 / vu16 / vu17 / vu18 / vu19 / vu20 / vu21 / vu22 / vu23 / vu24 / vu25 / vu26 / vu27 / vu28 / vu29 / vu30 / vu31 / vu32 / vu33 / vu34 / vu35 / vu36 / vu37 / vu38 / vu39 / vu40 / vu41 / vu42 / vu43 / vu44 / vu45 / vu46 / vu47 / vu48 / vu49 / vu50 / vu51 / vu52 / vu53 / vu54 / vu55 / vu56 / vu57 / vu58 / vu59 / vu60 / vu61 / vu62 / vu63 / vu64 / vu65 / vu66 / vu67 / vu68 / vu69 / vu70 / vu71 / vu72 / vu73 / vu74 / vu75 / vu76 / vu77 / vu78 / vu79 / vu80 / vu81 / vu82 / vu83 / vu84 / vu85 / vu86 / vu87 / vu88 / vu89 / vu90 / vu91 / vu92 / vu93 / vu94 / vu95 / vu96 / vu97 / vu98 / vu99 / vu100 / vu101 / vu102 / vu103 / vu104 / vu105 / vu106
vu1='m'           ;     change of unit to meter
vu2='kg'          ;     change of unit to kilogram
vu3='g'           ;     change of unit to gram*
vu4='s'           ;     change of unit to second
vu5='A'           ;     change of unit to ampere
vu6='K'           ;     change of unit to kelvin
vu7='cd'          ;     change of unit to candela
vu8='mol'         ;     change of unit to mole
vu9='Hz'          ;     change of unit to hertz
vu10='rad'        ;     change of unit to radian
vu11='sr'         ;     change of unit to steradian
vu12='N'          ;     change of unit to newton
vu13='Pa'         ;     change of unit to pascal
vu14='J'          ;     change of unit to joule
vu15='W'          ;     change of unit to watt
vu16='C'          ;     change of unit to coulomb
vu17='V'          ;     change of unit to volt
vu18='F'          ;     change of unit to farad
vu19='Ohm'        ;     change of unit to ohm
vu20='S'          ;     change of unit to siemens
vu21='Wb'         ;     change of unit to weber
vu22='T'          ;     change of unit to tesla
vu23='H'          ;     change of unit to henry
vu24='Cel'        ;     change of unit to degrees Celsius
vu25='lm'         ;     change of unit to lumen
vu26='lx'         ;     change of unit to lux
vu27='Bq'         ;     change of unit to becquerel
vu28='Gy'         ;     change of unit to gray
vu29='Sv'         ;     change of unit to sievert
vu30='kat'        ;     change of unit to katal
vu31='m2'         ;     change of unit to square meter (area)
vu32='m3'         ;     change of unit to cubic meter (volume)
vu33='l'          ;     change of unit to liter (volume)*
vu34='m/s'        ;     change of unit to meter per second (velocity)
vu35='m/s2'       ;     change of unit to meter per square second (acceleration)
vu36='m3/s'       ;     change of unit to cubic meter per second (flow rate)
vu37='l/s'        ;     change of unit to liter per second (flow rate)*
vu38='W/m2'       ;     change of unit to watt per square meter (irradiance)
vu39='cd/m2'      ;     change of unit to candela per square meter (luminance)
vu40='bit'        ;     change of unit to bit (information content)
vu41='bit/s'      ;     change of unit to bit per second (data rate)
vu42='lat'        ;     change of unit to degrees latitude[1]
vu43='lon'        ;     change of unit to degrees longitude[1]
vu44='pH'         ;     change of unit to pH value (acidity; logarithmic quantity)
vu45='dB'         ;     change of unit to decibel (logarithmic quantity)
vu46='dBW'        ;     change of unit to decibel relative to 1 W (power level)
vu47='Bspl'       ;     change of unit to bel (sound pressure level; logarithmic quantity)*
vu48='count'      ;     change of unit to 1 (counter value)
vu49='/'          ;     change of unit to 1 (ratio e.g., value of a switch; [2])
vu50='%'          ;     change of unit to 1 (ratio e.g., value of a switch; [2])*
vu51='%RH'        ;     change of unit to Percentage (Relative Humidity)
vu52='%EL'        ;     change of unit to Percentage (remaining battery energy level)
vu53='EL'         ;     change of unit to seconds (remaining battery energy level)
vu54='1/s'        ;     change of unit to 1 per second (event rate)
vu55='1/min'      ;     change of unit to 1 per minute (event rate, "rpm")*
vu56='beat/min'   ;     change of unit to 1 per minute (heart rate in beats per minute)*
vu57='beats'      ;     change of unit to 1 (Cumulative number of heart beats)*
vu58='S/m'        ;     change of unit to Siemens per meter (conductivity)
vu59='B'          ;     change of unit to Byte (information content)
vu60='VA'         ;     change of unit to volt-ampere (Apparent Power)
vu61='VAs'        ;     change of unit to volt-ampere second (Apparent Energy)
vu62='var'        ;     change of unit to volt-ampere reactive (Reactive Power)
vu63='vars'       ;     change of unit to volt-ampere-reactive second (Reactive Energy)
vu64='J/m'        ;     change of unit to joule per meter (Energy per distance)
vu65='kg/m3'      ;     change of unit to kilogram per cubic meter (mass density, mass concentration)
vu66='deg'        ;     change of unit to degree (angle)*
vu67='NTU'        ;     change of unit to Nephelometric Turbidity Unit
vu68='ms'         ;     change of unit to millisecond
vu69='min'        ;     change of unit to minute
vu70='h'          ;     change of unit to hour
vu71='MHz'        ;     change of unit to megahertz
vu72='kW'         ;     change of unit to kilowatt
vu73='kVA'        ;     change of unit to kilovolt-ampere
vu74='kvar'       ;     change of unit to kilovar
vu75='Ah'         ;     change of unit to ampere-hour
vu76='Wh'         ;     change of unit to watt-hour
vu77='kWh'        ;     change of unit to kilowatt-hour
vu78='varh'       ;     change of unit to var-hour
vu79='kvarh'      ;     change of unit to kilovar-hour
vu80='kVAh'       ;     change of unit to kilovolt-ampere-hour
vu81='Wh/km'      ;     change of unit to watt-hour per kilometer
vu82='KiB'        ;     change of unit to kibibyte
vu83='GB'         ;     change of unit to gigabyte
vu84='Mbit/s'     ;     change of unit to megabit per second
vu85='B/s'        ;     change of unit to byte per second
vu86='MB/s'       ;     change of unit to megabyte per second
vu87='mV'         ;     change of unit to millivolt
vu88='mA'         ;     change of unit to milliampere
vu89='dBm'        ;     change of unit to decibel (milliwatt)
vu90='ug/m3'      ;     change of unit to microgram per cubic meter
vu91='mm/h'       ;     change of unit to millimeter per hour
vu92='m/h'        ;     change of unit to meter per hour
vu93='ppm'        ;     change of unit to parts per million
vu94='/100'       ;     change of unit to percent
vu95='/1000'      ;     change of unit to permille
vu96='hPa'        ;     change of unit to hectopascal
vu97='mm'         ;     change of unit to millimeter
vu98='cm'         ;     change of unit to centimeter
vu99='km'         ;     change of unit to kilometer
vu100='km/h'      ;     change of unit to kilometer per hour
vu101='ppb'       ;     change of unit to parts per billion
vu102='ppt'       ;     change of unit to parts per trillion
vu103='VAh'       ;     change of unit to volt-ampere-hour
vu104='mg/l'      ;     change of unit to milligram per liter
vu105='ug/l'      ;     change of unit to microgram per liter
vu106='g/l'       ;     change of unit to gram per liter
```

With that code is possible to validate cbor structures.
```
cddl CBOR_Template_VTS.cddl validate output2.cbor > validation_cddl.txt
```


