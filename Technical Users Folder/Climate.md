# AKWarm Weather Data

AKWarm stores climate data for nearly 300 Alaskan communities.  For the 20 Main Weather Cities, the following data is stored and used in AKWarm calculations:

- Monthly Data
	- Solar irradiation
	- Wind speed
	- Average dry bulb temperature
- Annual Data
	- Heating degree days
	- Dry bulb temperature
	- Ground temperature
	- Wind speed
	- Design temperature

For the additional 253 communities the following data is stored and used in AKWarm calculations:

- Annual Data
	- Heating degree days
	- Dry bulb temperature
	- Wind speed
	- Design temperature

## Monthly Average Dry Bulb Temperature and Annual Heating Degree Day Data
It is important to understand how AKWarm determines the temperature data to use in its energy calculation for a city. Average dry bulb monthly temperature data is provided in the Energy Library for each of the approximately 20 Main Weather Cities, but not for the 253 other cities. For each of these other cities, annual average temperature or annual degree days may be present in the Energy Library. If annual average temperature is present, AKWarm compares it to the annual average temperature of the Main Weather City to come up with a temperature adjustment. That temperature adjustment is then applied to the monthly temperature from the Main Weather City to create a monthly temperature for the actual location. The adjusted monthly temperatures are used in the energy calculation.

In the few cities that do not have annual average temperature data, AKWarm looks to see if degree days are present. If so, it compares the city’s degree days to main Weather City’s degree days to come up with a temperature adjustment to apply to the monthly temperature data. If annual average temperature data and degree days are not available, AKWarm makes no adjustment to the monthly temperature data from the main Weather City.

In a perfect world, both degree day comparisons and annual average temperature comparisons should produce nearly the same information. Alaska weather data is not perfect. Inconsistencies exist between degree day information and annual average temperature information, even when it comes from the same source. AKWarm’s built-in validity checking routine of its Energy Library includes a test that checks for inconsistencies. Minor inconsistencies (0.6 degrees F or less) are left in the data, but any larger discrepancies are screened out.

## Wind Speed Data

#### Wind Speed Adjustment

An adjustment similar to the temperature adjustment process is used to adjust the monthly wind speeds of the Main Weather City. The monthly wind speeds are adjusted to more closely match the annual average wind speed of the actual city where the home is located (if the city’s annual average wind speed is available).

AKWarm converts wind speed at airport weather station to site wind speed (measured at a height equal to the ceiling of the top floor).

#### Site Wind Speed

AKWarm converts weather station wind speed to site wind speed, measured at the top floor ceiling. It uses the wind conversion model found in the Lawrence Berkeley Laboratory infiltration model. The degree of wind shielding selected by the user of AKWarm is what is considered "WindShield ID" in the discussion below. House ht is the height of the top floor ceiling of the house in feet.

A number of assumptions are made, since they are not provided as inputs:

weather station wind measurement height = 20 ft;
weather station terrain class = 2, shielding class = 1;
assumptions for each windshield ID are:

Site wind multiplier = coefficient \* (house height/32.8) ^ exponent

The coefficient and exponent vary depending on the terrain and shielding assumed for each windshield ID and depending on the assumptions about the weather station. See the details in the LBL infiltration model to determine how to calculate coefficient and exponent from these assumptions: “The Prediction of Air Infiltration”, M. Sherman and B. Dickinson, July 1985, LBL-19040.

AKWarm Category	LBL-defined Classes	Site Wind Multiplier
Shielded	Terrain Class 4, shielding class 4	.412 * (house height/32.8) ^.25
Average	terrain class 3, shielding class 3	.678 * (house height/32.8) ^.2
Exposed	Terrain class 3, shielding class 2	.805 * (house height/32.8) ^.2

## Solar Irradiation Data

AKWarm has detailed solar irradiation data for the Main Weather Cities.  Solar irradiation is the total amount of solar radiation energy received on a given surface area for a period of time.  The values used by AKWarm are hourly irradiation averages, with units in Btus / square foot / hour.   

## Ground Temperature

*Need to look into calculations as Alan has updated this recently*

## Design Temperature

The design temperature is used by AKWarm to determine the design heat load.  The design temperature is not the absolute minimum temperature for the location . Rather it is the  dry bulb temperature the outside air is at or above during 97.5% of the year. Although outside temperatures do occasionally go below this design temperature, the duration of these low temperature periods is so short that buildings tend to “coast” through them using heat stored in their thermal mass. When outside temperatures are above the design temperature, the rate of heat flow from the building will be less. If heating systems were designed for maximum weather conditions, excess capacity would exist during most of the system’s operating life.