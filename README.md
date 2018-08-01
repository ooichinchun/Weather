## Weather From Met Stations Across Singapore (Jan 2017 - April 2018) 

Weather prediction is not a new problem, and is primarily solved by climate models currently, which rely on physics-based numerical solvers for accurate computation. At the same time, these models are typically meant for large-scale predictions, and do not resolve local conditions very well, especially at levels relevant to urban residents such as us. A way to get around this is to utilize public met station data in conjunction with spatio-temporal modeling techniques to get a better estimate for local weather conditions.

Public records for weather from various meterological stations across Singapore have been downloaded and post-processed for the following plots via repeated calls to the APIs at data.gov.sg. 

The location and period of operation for the various stations are available at this [location](http://www.weather.gov.sg/wp-content/uploads/2016/12/Station_Records.pdf "MSS Station Location").

| ![Station Locations](https://raw.githubusercontent.com/ooichinchun/Weather/master/Stn_Location.png "Station Locations") | 
|:--:| 
| **Stations with temperature, wind and rain data (2017-2018)** |

### Temporal Patterns

The data is plotted for individual stations for the 12 months in a year. There are clear temporal differences due to the local monsoon patterns despite the commonly heard refrain "Singapore's weather forecasters have it easy. It's the same year-round." It should be noted that the relatively short time-span of the data available means that analysis here will not be able to identify long-term trends beyond a year or a single season.

In the data for Jurong Island presented below, we can see the dominant North wind between December and March, and strong South-easterly winds around July and August.

| ![Jurong Island Wind Rose](https://raw.githubusercontent.com/ooichinchun/Weather/master/JI_12Months.png "Jurong Island Wind Rose") | 
|:--:| 
| **Wind Rose for Jurong Island across 12 Months** |

Additionally, if one were to look at the mean wind speeds across each month for the same station, one would notice a clear shift in the mean and standard deviations through the year.

| ![Jurong Island Mean Wind Speeds](https://raw.githubusercontent.com/ooichinchun/Weather/master/JI_Barplot_12Months.png "Jurong Island Mean Wind Speeds") | 
|:--:| 
| **Wind Speeds for Jurong Island across 12 Months** |

Qualitatively though, there appear to be some differences between the stations at different locations even for the same time periods. For example, in the data for the Marina Barrage station presented below, we can see a similar dominant wind direction (NE) between January and March but no corresponding South-East winds in the middle of the year. 

| ![Marina Barrage Wind Rose](https://raw.githubusercontent.com/ooichinchun/Weather/master/MarinaBarrage_12Mths.png "Marina Barrage Wind Rose") | 
|:--:| 
| **Wind Rose for Marina Barrage across 12 Months** |

The question then is whether we can analyze the weather (wind/temperature/rain) across the island at a sufficient resolution to inform our residential design since it is clear that there is significant variation on a micro-climate level.

### Correlation Between Stations

| ![Correlation in Wind Speeds between Stations](https://raw.githubusercontent.com/ooichinchun/Weather/master/ns_correlation.png "Inter-Station Wind Speed Correlation") | 
|:--:| 
| **Inter-Station Wind Speed Correlation** |

Correlation in wind speeds between stations does not appear to be visually correlated to distance between stations, which is somewhat surprising. The data is for all wind speed data for one month, but values don't seem to be significantly changing month to month.

There is a baseline level of correlation between 0.6 and 0.8 though, as is clear from the graph (analyzed with Siqi Li).

### Single Station Prediction

As a initial test, we set out to predict the wind speed for a single station (Pulau Ubin was selected) from current temperature, relative humidity, amount of rainfall and time of day. The data was fit with a Gaussian Process framework with a combination of a radial basis function with a periodic kernel, and a Rational Quadratic Kernel.

| ![Prediction Error](https://raw.githubusercontent.com/ooichinchun/Weather/master/S106_Gpy.png "Pulau Ubin Prediction") | 
|:--:| 
| **Pulau Ubin Prediction** <br/> Wind speed prediction for Pulau Ubin via Gaussian Process Regression |

Various public residential zones show up quite clearly, with local districts such as Woodlands, Bishan, Toa Payoh and Tampines being very apparent.

### Other interesting datasets for Analysis

Other data sets of interest include [health related](http://www.hospitals.sg/polyclinics "Polyclinic Locations") (community polyclinic distribution and infectious disease logs) and traffic/pollutant related information.

Examples of things we could do include image analysis of the traffic data to obtain an estimate for the most/least polluted areas by traffic density.

| ![Vehicular Traffic Identification](https://raw.githubusercontent.com/ooichinchun/Weather/master/image6.png "Vehicle ID") | 
|:--:| 
| **IDing Vehicles** <br/> Vehicles are identified with Google's [Tensorflow Objection Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection "Object Detection API"). |

By using the Tensorflow Objection Detection API, we can estimate vehicular density and makeup for a  better estimate of traffic pollution around the city, which is reported to contribute to a quarter of total urban PM<sub>2.5</sub> pollution.
