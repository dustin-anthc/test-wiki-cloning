<H1>AKWarm Technical Manual - 1998 </H1>

<H2>Contents</H2>
-   Chapter 1: How AKWarm Calculates Energy Use
    -   1.1 Overview
        -   1.1.1 Basic Functions
    -   1.2 AKWarm Inputs
        -   1.2.1 AKWarm Libraries
        -   1.2.2 User Inputs
    -   1.3 AKWarm’s Internal Computer - House Heat Balance
        -   1.3.1 AKWarm Weather Data
        -   1.3.2 ENERGY ALGORITHMS
        -   1.3.3 Results of monthly calculations
        -   1.3.4 Annual energy totals
    -   1.4 AKWarm Outputs
        -   1.4.1 Heat Loss and Heat Load Report
        -   1.4.2 Energy Rating and Report
        -   1.4.3 Improvement Options Report
-  Chapter 2: Residential Heat Loss
    -   2.1 Conduction Heat Losses
        -   2.1.1 Building Conduction Heat Loss Calculations
        -   2.2.2 Above Grade Walls
        -   2.2.3 Above Grade Floors
        -   2.2.4 Ceiling With Attic
        -   2.2.5 Vaulted Ceiling
        -   2.2.6 Window/Glazing Components
    -   2.3 Below Ground Building Heat Loss Coefficients
        -   2.3.1 Below Grade Wall
        -   2.3.2 On-Grade or Below Grade Floors
        -   2.3.3 Summary
    -   2.4 Heat Loss From Air Infiltration & Mechanical Ventilation
        -   2.4.1 AKWarm calculates natural infiltration (cfm).
        -   2.4.2 AKWarm Assesses Mechanical Ventilation
        -   2.4.3 Net Ventilation Heat Loss
        -   2.4.4 Gross Heat Loss
-   Chapter 3 Building Heat Gains
    -   3.1 AKWarm calculates internal gains
        -   3.1.1 Internal gains from occupants
        -   3.1.2 Internal gains from lights and appliances
        -   3.1.3 Fuel use and internal gains associated with the domestic hot water heater.
    -   3.2 AKWarm Calculates Passive Solar Heat Gains
        -   3.2.1 Solar Area
        -   3.2.2 Gross Solar Gain
        -   3.2.3 Estimate of Building Thermal Mass
    -   3.3 Heating System Performance
        -   3.3.1 Primary or secondary Heating System Energy Use
-   Chapter 4 Putting It All Together
    -   4.1 Heating Load
        -   4.1.1 Why an “estimate”?
        -   4.1.2 Why “rate”?
        -   4.1.3 Why “near minimum”?
    -   4.2 Useful solar and internal gains
        -   4.2.1 Calculate the useable portion of the gross internal gains
        -   4.2.2 Calculate the useable portion of the gross solar gains
    -   4.3 AKWarm calculates the net load on the heating systems.
        -   4.3.1. Net out Useable internal and solar gains
        -   4.3.2. Partition the net load across the primary and secondary heating systems.
        -   4.3.3 Calculate the impact of a setback thermostat
    -   4.4 Annual Fuel Use and Fuel Costs
        -   4.4.1 Annual Fuel Use
        -   4.4.2 Energy Cost By Source
        -   4.4.3 Energy Cost By End Use
-   Chapter 5 The AKWarm Rating
    -   5.1 Introduction
    -   5.2 Rating Procedure
        -   5.2.1 Standardization of Operating Conditions
        -   5.2.2 Reference House
        -   5.2.3 Source BTUs
    -   5.3 Rating Calculations
        -   5.3.1 Actual Energy Cost
        -   5.3.2 How AKWarm Calculates Avoided Air Pollution Through Energy Efficiency
        -   5.3.3 Rating Point Calculation
        -   5.3.4 Rating Star Levels
        -   5.3.5 Messages Printed on Rating Certificate
        -   5.3.6 Rating Calibration Parameters (as defined in Energy Library, and in use 3/98)
-   Chapter 6: AKWarm Home Improvement Reports
    -   6.1 Introduction
        -   6.1.1 Improvement Measure Categories
        -   6.1.2 Improvement Calculations


***
***
#         Chapter 1: How AKWarm Calculates Energy Use
##        1.1 Overview

**AKWarm** is an easy-to-use computerized home energy <span id="D2HBEnergy_Ratin1" class="anchor"></span>analysis tool designed specifically for new and existing residential buildings in Alaska. It was developed under the direction of the Alaska Housing Finance Corporation (AHFC) for use in assisting home energy raters, weatherization assessors and home builders in evaluating the energy performance of homes on a consistent basis. **AKWarm** provides a prediction of the energy use of individual buildings operated under standard conditions, calculates an equivalent energy rating and recommends cost-effective energy improvements based on actual conditions in the building.

###       1.1.1 Basic Functions

 The basic functions of **AKWarm** allow you to:

  1.  Create a house data file. A description of the building and its energy related characteristics, including shell components, heating system, and geographical location, are entered as data into **AKWarm**, and stored in a house data file. Data is gathered in the field or from construction plans. Creating and editing of house data files is described in Chapter 4.

  2.  Analyze energy use. Using the information in a house data file, **AKWarm** computes heat loss, heat gain, and energy required to keep the house at a comfortable thermostatic set point, during a full year of operation. Energy use calculations are discussed in Chapter 6.

  3.  Show compliance with the Alaska Building Energy Efficiency Standard (BEES) for new construction.

  4.  Generate a Home Energy Rating. **AKWarm** uses AHFC's energy rating program to predict a home's energy score.

  5.  Compute the savings of individual energy conservation measures. **AKWarm** reviews possible efficiency improvement measures, calculates savings for each measure, evaluates the interaction between measures, and ranks the measures in order of their cost-effectiveness.

  6.  Produce rating certificates and reports. As part of the energy calculation process, **AKWarm** generates a number of performance reports that can be viewed on-screen and printed.

  7.  Save house data files.

##        1.2 AKWarm Inputs </H3>
###       1.2.1 AKWarm Libraries </H4>
####      *1.2.1.1. Information for 281 Alaska Communities*
#####     1.2.1.1.1 Weather Information:
  20 Prime Locations: <BR>
  1.  Monthly solar, wind speed, average dry bulb temperature <BR>
  2.  Annual heating degree days, dry bulb temperature, ground temperature, wind speed, design temperature

  All Other Locations<BR>
  1.  Annual heating degree days, dry bulb temperature, wind speed, design temperature

#####     1.2.1.1.2. Fuel Costs: 
  1.  Oil, gas, propane, wood, coal (if not available, user input allowed)

#####     1.2.1.1.3. Gas & Electric Utility Costs: 
  1.  Block rate, customer service charge, fuel surcharge, PCE

####      *1.2.1.2. Thermal & Energy Efficient Properties*
#####     1.2.1.2.1. Building and Insulation Materials
  1.  Description, R-value (From ASHRAE 1993 Fundamentals)

#####     1.2.1.2.2. Windows and Doors
  1.  Glazing shading coefficient (From ASHRAE Fundamentals)
  2.  U-value of glass, frame, air gap, gas fill (From ASHRAE Fundamentals)
  3.  Door U-values (From ASHRAE Fundamentals)

#####     1.2.1.2.3. Heating Systems, Hot Water Systems
  1.  Heating System description, AFUE, Steady State-AFUE adjustment, Auxiliary Power/heat output; upgrade devices - reduction in part-load losses, increase in steady state efficiency
  2.  Hot Water Systems: Energy factor, Recovery efficiency, insulation R-value

####      *1.2.1.3. Economic Factors*
#####     1.2.1.3.1. Building and Insulation: Materials and Labor Costs
The costs of materials for energy efficient improvement options were gathered from building materials suppliers and contractors around the state. Weatherization contractors have the greatest knowledge of costs in areas outside of the road system. Their bid lists were used to estimate labor times and costs for each improvement option. In most cases, the material and labor costs are only for replacement or addition of the energy efficient improvement, not for additional modifications that may be necessary to accommodate the task.

#####     1.2.1.3.2. Fuel Cost Escalation Factors
The US Department of Energy has developed “fuel cost escalation factors” to account for the fact that fuel will not cost the same in twenty years as it does today, and therefore estimates of energy savings should take into account these projected changes in cost. AKWarm uses DOE’s projected escalation factors.

#####     1.2.1.3.3. Community Cost Multipliers
Material and labor costs were gathered for two areas of the state: the lowest cost, on-the road system communities, and the highest cost communities where material and labor are flown in (or equivalent). Then each of the 281 communities in the database was assigned a cost multiplier, with 1 being the road-system low cost, 5 being the highest cost, and 2,3, and 4 being intermediary, based on data collected by the State Dept. of Labor and the Dept. of Community and Regional Affairs, and other economic data.

###       1.2.2 User Inputs
####      *1.2.2.1. House Site<*
  1.  Location: City, Prime Weather City, Utility(s),

####      *1.2.2.2. House Characteristics*
  1.  Occupancy; House-type; Wind-Shielding; Heated Floor Area; \# Bedrooms

####      *1.2.2.3. Shell Components*
  1.  Location; area; insulation type and amount

####      *1.2.2.4. Air Leakage and Mechanical Ventilation*
  1.  Air Leakage in air changes per hour or cubic feet per minute<BR>
  2.  Description of mechanical ventilation system (from list)

####      *1.2.2.5. Heating System*
  1.  Description (from list); AFUE or Steady State Efficiency; Distribution type, location, quality

####      *1.2.2.6. Other Appliances*
  1.  Domestic hot water system: type, energy factor, location, insulation<BR>
  2.  Fuel type for clothes dryer and range<BR>
  3.  Estimate of range of electricity use: average, low, high

##        1.3 AKWarm’s Internal Computer - House Heat Balance
**AKWarm** conducts a monthly energy balance on a house design to determine potential energy requirements. The monthly energy balance includes monthly bin analyses of specific building components and mechanical systems. It evaluates the effects of solar and internal gains and determines space heating, water heating, appliances needs, based on monthly modeling of both above-grade and below grade building envelope components

1.  AKWarm uses the user-supplied information for house size, location, occupant level (number of bedrooms plus one), and energy component descriptions.

2.  From the Energy Library, AKWarm gets the weather information (temperature, wind speed and design temperature) and fuel and electric prices for the city where the home is located.

3.  For each energy use, AKWarm does monthly calculations: each routine internally loops through each month’s weather information.

###       1.3.1 AKWarm Weather Data
It is important to understand how AKWarm determines the temperature data to use in its energy calculation for a city. Average dry bulb monthly temperature data is provided in the Energy Library for each of the approximately 20 Main Weather Cities, but not for the 253 other cities. For each of these other cities, annual average temperature or annual degree days may be present in the Energy Library. If annual average temperature is present, AKWarm compares it to the annual average temperature of the Main Weather City to come up with a temperature adjustment. That temperature adjustment is then applied to the monthly temperature from the Main Weather City to create a monthly temperature for the actual location. The adjusted monthly temperatures are used in the energy calculation..

In the few cities that do not have annual average temperature data, AKWarm looks to see if degree days are present. If so, it compares the city’s degree days to main Weather City’s degree days to come up with a temperature adjustment to apply to the monthly temperature data. If annual average temperature data and degree days are not available, AKWarm makes no adjustment to the monthly temperature data from the main Weather City.

In a perfect world, both degree day comparisons and annual average temperature comparisons should produce nearly the same information. Alaska weather data is not perfect. Inconsistencies exist between degree day information and annual average temperature information, even when it comes from the same source. AKWarm’s built-in validity checking routine of its Energy Library includes a test that checks for inconsistencies. Minor inconsistencies (0.6 degrees F or less) are left in the data, but any larger discrepancies are screened out.

####      *1.3.1.1 Wind Speed*
An adjustment similar to the temperature adjustment process is used to adjust the monthly wind speeds of the Main Weather City. The monthly wind speeds are adjusted to more closely match the annual average wind speed of the actual city where the home is located (if the city’s annual average wind speed is available).

AKWarm converts wind speed at airport weather station to site wind speed (measured at a height equal to the ceiling of the top floor)

#####     1.3.1.1.1. Site Wind Speed
AKWarm converts weather station wind speed to site wind speed, measured at the top floor ceiling. It uses the wind conversion model found in the Lawrence Berkeley Laboratory infiltration model. The degree of wind shielding selected by the user of AKWarm is what is considered "WindShield ID" in the discussion below . House ht is the height of the top floor ceiling of the house in feet.

A number of assumptions are made, since they are not provided as inputs:

    weather station wind measurement height = 20 ft;
    weather station terrain class = 2, shielding class = 1;

assumptions for each windshield ID are:

    Site wind multiplier = coefficient \* (house height/32.8) ^ exponent

The coefficient and exponent vary depending on the terrain and shielding assumed for each windshield ID and depending on the assumptions about the weather station. See the details in the LBL infiltration model to determine how to calculate coefficient and exponent from these assumptions: “The Prediction of Air Infiltration”, M. Sherman and B. Dickinson, July 1985, LBL-19040.


| AKWarm Category | LBL-defined Classes                | Site Wind Multiplier             |
|:----------------|:-----------------------------------|:---------------------------------|
| Shielded        | Terrain Class 4, shielding class 4 | .412 \* (house height/32.8) ^.25 |
| Average         | terrain class 3, shielding class 3 | .678 \* (house height/32.8) ^.2  |
| Exposed         | Terrain class 3, shielding class 2 | .805 \* (house height/32.8) ^.2  |


<H4>1.3.2 ENERGY ALGORITHMS</h4>

1.  Above Grade Heat Loss
2.  Below Grade/Foundation Heat Loss
3.  Air Infiltration & Mechanical Ventilation Heat Loss
4.  Solar and Internal Heat Gains
5.  Space Heating System Performance
6.  Domestic Hot Water Heating Performance

### 1.3.3 Results of monthly calculations

1.  Natural infiltration in cubic feet/minute
2.  Mechanical ventilation in cubic feet/minute
3.  Apparent Sensible Effectieness of the mechanical ventilation system
4.  UA values for natural and mechanical ventilation by month and temperature of exfiltrating air, Btu/hr/deg F.
5.  Amount that the setback thermostat lowers the daily average indoor temperature in the living space, degrees F.
6.  Gross heat losses by month and temperature of indoor space, Btu/hr
7.  Gross solar gains by month and orientation
8.  Utilized fraction of gross solar gains
9.  Useable solar gains by month
10.  Gross internal gains by month, But/hr
11.  Useable internal gains by month, But/hr
12.  Net space heating load by month, But/hr
13.  Net load on primary and secondary heating system by month, Btu/hr
14.  Heating system loss for primary and secondary systems by month, Btu/hr (includes both distribution loss and heating plant loss)
15.  Fuel use for all end uses, split by month and fuel type, Btu/hr for all fuel types

### 1.3.4 Annual energy totals

After making the above-cited calculations for each month, AKWarm creates annual summaries which are included in the output reports:

1.  Space heating fuel use in MMBtu
2.  Domestic hot water heating fuel use in MMBtu
3.  Lights and Appliance fuel use in MMBtu
4.  Total fuel use of all end uses in MMBtu
5.  Total annual fuel cost by fuel type in $

## 1.4 AKWarm Outputs
### 1.4.1 Heat Loss and Heat Load Report
#### What AKWarm Does With Heat Loss Calculations

1.  **Determines Design Heat Load**: AKWarm provides an estimate of the overall heat loss *rate* of a building through its individual components (BTUs/hr). This can be summed in order to estimate the amount of heat which will flow from the building for each degree of temperature difference between the inside and outside of the building. This building heat loss rate can then be used to determine the amount of heat that needs to be supplied to the house under peak conditions, and the equipment which will need to be installed to heat the house under this condition can be sized accordingly. This allows engineers and mechanical system designers to economically size heating systems which can be relied upon to give comfort to the building occupants under all reasonable conditions, within a particular climate.

2.  **Predicts Annual Fuel Requirements**: The second purpose of the heat loss calculation is to provide a basis for estimating the long term performance of the dwelling in the context of the range of weather conditions which occur on average in a particular climate zone. The heat loss rate is combined with weather data to predict the fueling requirements for heating a home over a long period of time.

3.  **Shows Compliance with Building Energy Efficiency Standards**: Heat loss calculations can be use to establish the overall compliance of a building with the state’s building energy standards. Heat loss rates of individual components can be summed to establish an effective overall heat loss rate that is compared with BEES requirements for that location, to establish if the building meets those requirements.

### 1.4.2 Energy Rating and Report

The AKWarm Energy Rating process involves analyzing the energy use of the actual building, normalized for standard occupancy conditions, and analyzing the energy use of two reference case buildings: a house that would meet the State Building Energy Efficiency Standards (currently set at 83 points) and a very efficient house (100 points). The task is performed by standardizing the building description and then calculating the energy use of the standardized building.

In the rating system, the rating on a house is given as a score on a scale of 0 to 100 points, with a corresponding star rating, from 1 Star to 5 Star Plus. 100 points indicates that the house is potentially saving as much energy as it reasonably could in a given climate. The points are based exclusively on energy savings (MMBTUs of source fuel) and have nothing to do with the cost of the measure or cost of fuel.

The AKWarm energy rating, includes the number of points earned and the Star rating. A line graph indicates how the rated home compares to the average home in the region and to the Alaska Building Energy Efficiency Standard (BEES) for new construction.

### 1.4.3 Improvement Options Report

The AKWarm Improvement Options Report contains a cost evaluation of major improvements. Major improvements pertain to the more expensive improvements, such as adding insulation to an attic or replacing a heating system. Low cost recommendations are provided on a separate checklist. Low cost measures range in cost from requiring no materials and little time to install to improvements that may cost a few hundred dollars.

The improvement options report is generated after AKWarm analyzes possible energy efficiency improvements. It analyzes each improvement by “applying” the improvement to the building (i.e. modifying the home description to reflect installation of the improvement), and then re-calculating the energy use of the building to determine the energy saved. Because interaction between energy efficiency improvements is accounted for, many energy calculations are initiated by this module. All remaining measures are re-analyzed. This process continues until all recommended measures have been applied to the building.

The improvement options that were evaluated and determined to be cost effective are listed at the top of the page. These are measures that show a savings to cost ratio of 1 or more. This table includes a description of the improvement measure and the location for which it is recommended, as well as an estimate of the average cost of installation, the annual savings, and the rating points gained from installation.

Chapter 2 Residential Heat Loss
===

2.1 Conduction Heat Losses 
---

The rate at which heat moves through a solid material depends on its thermal conductivity and on the temperature difference across the material. The fundamental relationship between these quantities is given as:

Equation 1:

> where:
>
> Q = rate of heat transfer through the material (Btu/hr)
>
> k = thermal conductivity of the material (Btu/°F\*hr\*ft)
>
> Δx = thickness of the material in the direction of heat flow (ft)
>
> ΔT = temperature difference across the material (°F)
>
> A = area heat flows across (ft2)

Since building designers are usually interested in reducing the rate of heat flow from a building, it is more convenient to think of a material’s resistance to heat flow rather than its thermal conductivity. A material’s thermal resistance or R-value can be defined as its thickness in the direction of heat flow divided by its thermal conductivity.

Equation 2:

These two equations can be combined to yield an equation that is convenient for use in estimating heating loads:

*Equation 3:*

where:

Q = rate of heat transfer through the material (Btu/hr)

ΔT = temperature difference across the material (°F)

R = R-value of the material (°F \* ft2 hr/Btu)

A = area heat flows across (ft2)

### 2.1.1 Building Conduction Heat Loss Calculations 

The standard heat loss calculation procedure is to develop a thermal conductivity for each component of the building, which is then used in parallel with the other building components to establish the heat loss rate of the entire building. This procedure is area weighted, that is, the calculation procedure assumes that heat flows through materials as a function of their overall area and thermal properties independent of all other components contained in the building. Thus the sum of all the wall areas times the heat loss rate (U-value) of all the wall areas will describe the total amount of heat that will flow through those walls under particular temperature conditions. This amount of heat, in so far as the building is maintained at a given temperature, will be completely independent of the amount of heat that flows through the windows or the ceiling, or any other building component.

For the sake of simplicity in calculation, one dimensional heat flow is assumed, with heat traveling perpendicular to the inside surface, for all calculations except earth contact where two dimensional heat flow is considered to be significant.

Heat flow is usually calculated by using the overall thermal resistance method as described in ASHRAE Fundamentals 1993. The total resistance to heat flow through building constructions is the sum of the resistances (R-values) of all parts of the construction from inside surface to outside surface. This includes an air film resistances for both inside and outside surfaces, as shown in Table 2.1.

**Heat Loss Calculations**

The resistance to heat flow through building components, such as flat ceilings, floors, or walls, is equal to the numerical sum of the resistances of all parts of the component added in series:

R = R1 + R2 + R3 + R4 +...Rn

where R is the resistance of the component from inside surface to outside surface and R1, R2,....Rn are the individual resistances of the parts. These resistances are commonly known as “R-values” and have units of Hr x °F x ft2/Btu.. To obtain that total resistance of the building component RT add the surface-to-surface resistance R and the resistances of the inside and outside air films Ri and Ro: Rt = Ri + R + Ro

The overall coefficient of heat transmission or U-value is equal to the reciprocal of the total resistance (U = 1/RT) . U-value has units of Btu/hr x °F x ft2.

In most installations, components are arranged so that parallel heat flow paths of different conductances result. For example in a standard insulated frame wall one heat flow path passes through the insulated section of the wall while another heat flow path passes through the studs. The R-value of the insulation is obviously much greater than the R-value of the studs, so heat passes more quickly through the studs, however the relative area of the insulated section is greater so it tends to dominate the heat loss rate. If we assume that there is negligible lateral heat flow between paths, each path can be considered to extend from inside to outside, and the transmissivity of each path can be calculated. The average transmissivity or U-value is then calculated by determining what percentage of the total component is *insulation* and what percentage is *stud*, calculating the heat loss through each assembly

Using the descriptions supplied by the user, and the R-values of those materials from the AKWarm Energy Library database, AKWarm uses these procedures to determine the total-R-value and then the total U-value for each building shell component.

AKWarm uses standard, industry approved constants for air film resistances and effect of framing members (see below), and assumes 1/2” drywall as the inside surface of walls and ceilings and 5/8” plywood as the inside surface of above grade floors and the outside surface of above grade walls and ceilings, unless otherwise described. The insulating effect of carpeting on above- and below-grade floors is also included as a default.

The following conditions are assumed in calculating the design R-values:

1.  Equilibrium or steady-state heat transfer, disregarding effects of heat storage

2.  Surrounding surfaces at ambient air temperature

3.  Exterior wind velocity of 15 mph (surface with R = 0.17°F\*ft2\*h/Btu)

4.  Surface emittance of ordinary building materials is 0.90

#### ΔT (Temperature Difference Across The Material)

The standard inside temperature used by AKWarm is 70°F for conditioned space and 55°F for semi-conditioned space.

The revised outdoor mean monthly temperature is based on the number of hours in the month below the interior setpoint temperature. Calculating this revised monthly temperature involves an analysis of the mean monthly ambient dry bulb temperature taken from the weather file in the Energy Library and the standard deviation of this temperature.

The formula used for calculation of this temperature is described most clearly in “Solar Engineering of Thermal Processes”, 1991, page 417-419. Further information is in a more detailed article in the ASHRAE Journal, June 1983, “Estimation of Degree Days and Ambient Temperature Bin Data from Monthly Average Temperatures, pages 60-65. There are some simplifications implemented in this routine to speed up calculations under conditions where revising the outdoor temperature results in a very small adjustment. The simplifications made do keep the revised temperature vs. the average temperature curve continuous so problems won’t be encountered when estimating energy savings, where small changes in energy use need to be measured by the model.

#### Air Film Resistances

In addition to the thermal resistances of the solid materials that make up an assembly there are two invisible, but not insignificant, thermal resistances. These are called the inside and outside air film resistances. They represent the insulating effects of thin layers of air that cling to all building surfaces. The R-values of these air films are dependent on surface orientation, air movement along the surface and reflective qualities of the surface.

AKWarm uses air film R-values for nonreflective surfaces typical of most building surfaces:


| TABLE 2.1 THERMAL RESISTANCES FOR AIR FILMS |
|:--------------------------------------------|
| POSITION                                    |
| INSIDE AIR FILM                             |
| Horizontal                                  |
| Sloping 45 Degrees                          |
| Vertical                                    |
| Horizontal                                  |
|---------------------------------------------|
| OUTSIDE AIR FILM                            |
| 15 mph wind on any surface                  |

#### Effect of Framing Members

Wood-framed buildings with wall studs, ceiling joists, window headers and other framing members must take into account the fact that these framing members spanning across the insulation cavity tend to reduce its effective total R-value. This is because the thermal resistance of wood is usually less than the thermal resistance of insulation materials used to fill the wall cavity. AKWarm adjusts the R-value of an assembly to include the thermal effects of framing. This requires that the assembly’s total R-value be calculated both between the framing and at the framing. The resulting total R-values are then weighted according to the percentage of solid framing in the assembly.

#### Insulation Quality multipliers

These are the multipliers used to adjust the overall component R-value for the effects of insulation damage, as described by the user.

| Insulation Quality | Multiplier |
|:-------------------|-----------:|
| OK                 | 1          |
| Damaged            | .95        |
| Very Damaged       | .67        |

#### Buffer Spaces

Buffer spaces are intermediate, not intentionally heated spaces between the living zone and the outside, separating insulated shell components from the outdoors. Buffer spaces providing some additional effective R-value for the shell component by decreasing the temperature difference between the inside and outside of the insulated layer, and thus reducing the heat loss rate. In residential construction, crawl spaces, attics, garages, enclosed porches are typical buffer spaces. Buffer space issues are particularly important for insulated floors that are above closed crawl spaces.

The procedure AKWarm uses to calculate the effect of buffer zones establishes the heat loss rate from the building to the buffer, then from the buffer space to the outside, neglecting thermal storage. These two heat flows are added together in series.

| **Buffer Zone Effective R-values Used By AKWarm ** |
| **Buffer Zone**                                    |
|----------------------------------------------------|
| Ceiling With Attic                                 |
| Cathedral Ceiling                                  |
| Floor over Leaky Crawl                             |
| Floor over Tight Crawl                             |
| Floor over Tight Insulated Crawl                   |

### 2.2.2 Above Grade Walls

The average overall R-values of wood frame walls are calculated by assuming parallel heat flow paths through areas with different thermal resistances. These different paths are represented by:

1.  The insulation value of the wood members themselves (studs, plates, frames)
2.  The insulation value of the headers, which span the wall areas above windows and doors to carry structural loads.
3.  The insulation value of the cavity, or the area between the studs where insulation material is placed.

All walls are assumed to be finished on the inside with 1/2 inch gypsum wall board and on the outside with either 1/2 inch plywood sheathing and beveled wood siding, or with T-111 5/8 inch siding.

For each type of above grade wall described, AKWarm uses Equation 2 to calculates the R-values and then the U-values of the individual sections (insulated sections and framing sections) and then calculates the composite U-value from the U-values of the individual sections, weighting each U-value by its fraction of the overall component. Finally, it makes any indicated adjustments for insulation quality.

To determine framing fraction, AKWarm takes into account the characteristics of the framing type being analyzed, including framing member spacing and framing member thickness. Using these methods, AKWarm provides framing factors equivalent to those listed in the table below for stud walls. *If framing members have thicknesses other than 1.5 inches, different framing factors will be calculated*.


| *Wall Type* PATHS| Single Stud Wall   | Strapped Wall           | Double Wall  | Curtain/Standoff Wall | Stressed Skin Panel |
|                  | 16 “o.c. | 24” o.c.| 16 “o.c.   | 24” o.c.   |              |                       |                     |
|------------------|----------|---------|-------------------------|--------------|-----------------------|---------------------|
| Header           | .03      | .03     | .03        | .03        | .03          | .03                   |                     |
| Framing Fraction | .18      | .13     | Main:.18   | Main:.144  | Main:.126    | Main:.126             | Frame:.061          |
|                  |          |         | Other:.09  | Other:.09  | Other:.112   | Other:.099            | Spline:.076         |
|                  |          |         | Overlap:.5 | Overlap:.5 | Plywood:.015 | Plywood:.007          |                     |

**Assumptions used:**

> Shell material thickness:
>
> Wall sheetrock = .5 inches
>
> Wall plywood = .5 inches
>
> Window and Door Headers = 3 inches
>
> Fraction of wall that is door and window headers =.03 (based on 11.3% window/gross wall ratio, 4ft high windows, and 2 doors per home)
>
> Assumes that walls with spacing greater than 16 “ o.c. utilize some optimal value framing (total framing length per ft2 of wall is about 1.27 for standard framing, 1.04 for optimal value framing.
>
> Plywood Fraction: Assumes plywood wraps window and door openings and also factors in the plywood subflooring that bridges the two walls of double stud wall; assumes 5/8” plywood for subfloor

In addition to these general features of an above-grade frame wall, specific variations can be introduced using alternative construction techniques which change the amount of lumber in the wall and add additional cavities for purposes of added insulation. It may also include the use of rigid foam insulated sheathing, which can cover the entire exterior or interior of the wall and add additional R-value over all components. Besides single stud wall construction, AKWarm models strapped walls, double walls, stand-off (curtain) walls, log walls, and strapped log walls. Table xx. details the typical framing factors calculated by AKWarm.

1.  **Single Stud Wall**

As described above, the parallel heat paths modeled are: Section (1): Insulated Cavity, Section (2) Framing , and Section (3) Headers. The table below describes how these paths are modeled. Framing fractions for each section are calculated

|-----------------------------------|--------------------------------------|-------------------------|------------------------|
| Element                           | R-value Section 1 (Insulated Cavity) | R-value Section 2       
                                                                                                     
                                                                            (Studs, plates)          | R-value Section 3      
                                                                                                                              
                                                                                                      (Headers)               |
| 1. Inside surface, still air      | 0.68                                 | 0.68                    | 0.68                   |
| 2. Gypsum Wallboard, 0.5 in.      | 0.45                                 | 0.45                    | 0.45                   |
| 3. Wood stud                      | ---------------                      | User described          | User described         |
| 4. Cavity Insulation              | User described                       | ------------            | ------------           |
| 5. Insulated Sheathing            | User described                       | User described          | User described         |
| 6. Siding                         | 0.81                                 | 0.81                    | 0.81                   |
| 7. Outside surface, 15 mph wind   | 0.17                                 | 0.17                    | 0.17                   |
| TOTAL                             | Total R-value of insulated cavity    | Total R-value , framing | Total R-value , header |
| Framing Fraction                  | 0                                    | .125 (if 24”o.c. stud)  | .03                    |

1.  **Log Wall:**

> Ratio of the average thickness of a log wall to the log diameter = .9

1.  **Strapped Log Wall:**

AKWarm calculates the R-value of sections described by logs, strapping framing, strapping cavity, and section covering all sections.

1.  **Standoff (Curtain) Wall: **

2.  **Strapped Stud Wall**:

3.  Stress Skin Panel Wall:

4.  Other Walls:

> Walls that are included in this category use pre-established composite R-values that are listed in the Energy Library database. These above grade walls include metal stud walls, masonry walls and straw bale walls.

### <span id="_Toc371140056" class="anchor"><span id="_Toc371140183" class="anchor"></span></span>2.2.3 Above Grade Floors

The calculation of R-value of the above grade floor assembly separately addresses the two different floor sections: the insulation section and the framing section. It accounts for the buffering effect of a closed crawl space, if one is beneath the floor.

Framing Fraction : uses 15% more than simply evenly spaced floor joists, to account for overlap over support beams, some penetrations, and extra joists to support partition walls; doesn’t consider the framing around the perimeter of the floor because it sits under an insulated wall and thus is not much of a short circuit; assumes floor joists are spaced 16” o.c.. Slightly more than the evenly-spaced joists are sensitive to spacing, since some of the extra joist length is due to overlap of joists at support beams. All of the framing is sensitive to the thickness of the main framing member, i.e. if TJI’s are used they reduce the thickness of all framing members in this calculation.

R-value includes inner air film, carpeting/pad, 1/2” plywood floor and 5/8” plywood subfloor, any insulating sheathing.

Framing member width is assumed to be that of a 2 x 10 unless total insulation thickness is greater than that.

#### Effective R-value of a crawl space beneath the floor:

1. Exposed floor on pilings: assumes 5/8 inch plywood floor, and calculates the R-value of plywood cap, outer air film, and trapped air space between the top of the insulation and the flooring layers (or between the plywood cap and the insulation, depending on how the insulation is installed.

2. Floor over crawl space: calculates the R-value of the air film between the floor assembly and the crawl space and the total R-value of the insulation cavity section (assumes there is no trapped air gap, insulation is installed against the subfloor), the R-value of the framing section.

The effective R-value of the crawl space as a buffer space is also added to the composite R-value. The AKWarm spreadsheet “Buffers” calculated the following buffer space R-values:

Leaky crawl R= 2.83

Tight crawl R = 3.74

Insulated Crawl R = 7.56

### <span id="_Toc371140057" class="anchor"><span id="_Toc371140184" class="anchor"></span></span>2.2.4 Ceiling With Attic

The R-value of the ceiling with attic accounts for buffering effect of the attic space, as well as the insulating value of the insulated ceiling component.

AKWarm addresses the attic as having four parallel paths of heat flow: center insulation, center framing, edge insulation, edge framing. The edge section is addressed because with standard framing (no raised heel truss), the insulation diminishes in thickness near the long edge of the attic, because the height of the attic diminishes. See “Volume I: Heat Loss Assumptions and Calculations” Super Good Cents Heat Loss Reference, 24 Oct. 88, Ecotope, Inc., p. 10-14 for additional information. This document was the basis for some of the calculations in this routine although these calculations do differ somewhat from the techniques described in the Super Good Cents document. As in the Ecotope document the attic is assumed to be 30’ by 45’, a non-standard size, but the dimensions are a reasonable average for the cross-section of standard-sized attics. The roof pitch is assumed to be 4/12. The ceiling framing is assumed to be 2x4 (e.g. the bottom chord of a truss).

### <span id="_Toc371140058" class="anchor"><span id="_Toc371140185" class="anchor"></span></span>2.2.5 Vaulted Ceiling

The vaulted ceiling is defined as a frame ceiling in which the roof structure and the ceiling structure are composed of the same members. Typically this construction is used in providing cathedral ceilings in living rooms, family rooms, or other rooms where a high ceiling is desirable. The ceiling construction is usually 2x12’s or 2x14’s insulated with fiberglass batt.

It is assumed that the vaulted ceiling is vented between the top of the insulation and the roof deck. If there is no insulation in the cavity, it is assumed that the roof is an exposed beam room (no closed framing cavity), with no ventilation. AKWarm does not address any insulating value of snow on the roof.

Again AKWarm uses the parallel method of calculating heat flow. The two parallel paths of heat flow are through the insulated cavity section and through the framing section.

### <span id="_Toc371140059" class="anchor"><span id="_Toc371140186" class="anchor"></span></span>2.2.6 Window/Glazing Components

The window/glazing heat-loss rate is calculated from the area and composite thermal resistance of frame and glazing, based on user-input. For each window/glazing component described AKWarm uses either the certified u-value that is input or creates a composite u-value and R-value based on the frame type and glazing description, and using standard u-values derived from ASHRAE. Since AKWarm does not ask the user to distinguish between fixed and operable windows, it uses a single default u-value that is listed in the ASHRAE 1993 Fundamentals Handbook , pp 27.7-27.8 as operable with a metal spacer type .

<span id="_Toc371140060" class="anchor"><span id="_Toc371140187" class="anchor"><span id="_Toc371146339" class="anchor"></span></span></span>2.3 Below Ground Building Heat Loss Coefficients
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Building components in direct contact with the earth have considerably different thermal characteristics than other building components because of the earth’s high heat capacity, which dampens seasonal temperature swings and eliminates daily swings. These effects cause ground heat loss to lag and be more constant than heat loss of above grade components. The extent of these effects is determined by the depth below grade, the thermal conductivity of the soil, and the R-values of the adjoining building components.

These effects have led most ground heat loss methods to use special ground temperature functions as driving terms. The basic ASHRAE method uses an average heating season ground temperature. More sophisticated methods use a sinusoidal ground temperature function. These ground temperatures are used with conductance terms which are calculated using finite difference or finite element models, or by integrating the conductance of concentric heat flow paths through the soil.

While these methods provide acceptable estimates of ground heat flow, several drawbacks exist within the context of use for AKWarm. The conductance factors from these methods are not suitable for use in existing models which use air temperature as the only driving term. Also, the factors are not comparable to above-grade conductance factors, making building heat loss rate trade offs between below and above-grade components problematic. The methods have also only been applied to a limited selection of insulation configurations and do not include many common construction techniques found in Alaska.

Comparisons between results of the most prominent methods show large differences in predicted heat loss. Uncertainty also revolves around soil conductivities, which vary drastically between sites and seasons.

The table below compares the heat loss through an uninsulated floor located 7 feet below grade for a number of different calculation methods.

A = AHSRAE Fundamentals 1993, Table 15 page 25.11

B = Ecotope Finite Element Analysis used in the Pacific Northwest (Described in “Heat Loss Coefficient Tables for Use with the Washington State Energy Code and the Super Good Cents Program”, December 1992)

C = HOT-2000 program used by Canadian R-2000 and Alaska Craftsman Home Programs

A ground conductivity of 0.75 Btu/hr-deg F-ft was assumed for each method.

A slab 30’ x 45’ (perimeter = 150’, area = 1340 sq. Ft) was assumed

An air film + floor covering + slab resistance of R-2.5 was assumed . No other insulation is included.

|--------------------|--------|---------|----------|
|                    | A      
                              
                      ASHRAE  | B       
                                        
                               Ecotope  | C        
                                                   
                                         Hot-2000  |
| Total UA           | 27.8   | 73.1    | 91.8     |
| Average U          | 0.021  | 0.054   | 0.068    |
| Average R          | 48.5   | 18.5    | 14.7     |
| Effective Ground R | 46.0   | 16.0    | 12.2     |

The material developed by Ecotope is the closest to meeting the needs of the AKWarm program, because it was developed to calculate losses to ambient air temperature rather than using more detailed ground temperature and characterization data. Ecotope used an hourly simulation program, SUNCODE-PC to model the ground contact situation. It modeled only certain types of construction systems. Without access to SUNCODE, we have derived algorithms for determining the effective R-value of the ground in relationship to the building components (e.g. slab-on-grade perimeter, slab-on-grade center, below-grade wall, below grade floor center, below-grade floor perimeter) by fitting the ground heat loss simulation data developed by Ecotope.

### <span id="_Toc371140061" class="anchor"><span id="_Toc371140188" class="anchor"></span></span>2.3.1 Below Grade Wall

For the below-grade portion of a wall, AKWarm calculations provide the heat loss coefficient per perimeter foot of each below-grade wall section that is uniformly insulated. The coefficient returned is given in Btu/ft-deg. F. The calculation assume that the heat flow paths are circular, as shown in 1993 ASHRAE Fundamentals, p. 25.10, Fig. 4.

An important factor affecting the heat loss of a basement wall is the height of soil against the outside of the wall. The deeper the wall is buried, the lower the rate of heat loss through the wall. Notice in the Figure above that the heat flow paths from the inside basement air to the outside air become longer for the lower portions of the wall. As the path length increases, so does the effective thermal resistance of the soil.

The method AKWarm uses for approximating the heat loss through the foundation wall divides the wall into horizontal strips based on the height of finish grade.

The function essentially evaluates the integral of the UA for each horizontal slice of wall at a depth x. The R-value of the slice is the R-value of the wall component + the R-value of the ground. The R-value of the ground is the path length times the R-value per foot of ground.

The routine input parameters are:

1.  R -value of the wall component itself, NOT including any outer film coefficient;

2.  Height of the wall section in feet

3.  Position of the top of the wall with respect to grade, measured in feet. This position is positive if the wall top is above grade, and negative if below grade.

The output of this function corresponds well with Table 14, p. 25.11 of ASHRAE Fundamentals when the R-value per foot of ground constant is R-1.25. The output also corresponds with the finite element analysis done by Ecotope.

R-value per foot of ground. R-1.33 corresponds to the conductivity of 0.75 Btu/hr-ft-deg. F used by Ecotope in their work for the Pacific NW. That value is implicitly assumed in the below-grade floor routines included in this program.

##### All Weather Wood Below Grade Wall

Sections include: Inner air film, R-value, insulating sheeting R-value, and a layer of 3/4” plywood (no interior wall covering is assumed)

Framing Fractions are calculated in the same way as as those for Above Grade stud walls.

##### Below Grade Masonry Wall

R-value sections include: inner air film, insulating sheathing and masonry R-value.

### <span id="_Toc371140062" class="anchor"><span id="_Toc371140189" class="anchor"></span></span>2.3.2 On-Grade or Below Grade Floors

In buildings with concrete floor slabs rather than crawl spaces, heat flows from the floor slab downward to the surrounding earth, and outward through any exposed edges of the slab. Of these two paths, the outward flow of heat through the slab edge tends to dominate. This is because the outer edge of the slab is exposed to either the outside air or to soil only slightly warmer than outside air. Soil under the slab tends to become thermally stable once the building is maintained at normal comfort temperatures, and hence downward heat losses are relatively small. Areas of the floor close to the exposed edges will have higher rates of heat loss compared to areas several feet in from the edge. It is therefore important to have higher R-value insulation under the slab near its edges. As with basement walls, the actual paths of heat flow from a slab to the soil and outside air are complex and not easily modeled. For this reason approximating methods have been developed to estimate the rate of heat loss from a floor slab.

AKWarm separately calculates heat loss from on/below grade floor perimeters and center areas. The perimeter area is considered the area within 4 feet of the edge of the slab, and can itself be described in 2 two-foot increments. Two different routines are used to perform the calculations: one for floors within one foot of grade (typically slab on grade floors) and one for deeper floors. The deep floor routine does not take into account the slab edge insulation.

The on/below grade floor R-value calculation includes a floor covering, even though some crawl space floors or slabs may not be covered. However, the energy impact of the floor covering is small for crawl space floors because the effective ground R-value is high; the energy impact of the floor covering on garage floors is not large because of the reduced delta T in the garage. The energy impact of a floor covering for a slab on-grade living space floor can be noticeable because of low effective ground R-value for the perimeter of the slab, and significant delta T because the floor is exposed to living space temperatures.

### <span id="_Toc371140063" class="anchor"><span id="_Toc371140190" class="anchor"></span></span>Summary

AKWarm calculates the UA (0verall u-value) information for each of the shell components, by component type and temperature-defined location of the component (i.e. conditioned space or semi-conditioned space). It also calculates the combined UA of all shell components.

The R-values for above-grade walls, doors, and windows are adjusted to reflect the proper R-value for a site wind speed, instead of the assumed wind speed.

<span id="_Toc371140064" class="anchor"><span id="_Toc371140191" class="anchor"><span id="_Toc371146340" class="anchor"></span></span></span>2.4 Heat Loss From Air Infiltration & Mechanical Ventilation
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### <span id="_Toc371140065" class="anchor"><span id="_Toc371140192" class="anchor"></span></span>2.4.1 AKWarm calculates natural infiltration (cfm).

In addition to conduction losses, heat is also carried out of the building by air leakage, often called air infiltration. The faster air leaks through a building the greater the amount of heat it carries away.

It would be impossible to assess the location and magnitude of all the air leakage paths in a typical house. Instead an estimate of air leakage can be made based on the air sealing quality of the building. The most cost-effective means of estimating this air leakage is by using a blower door test to determine air change at 50 Pa.

AKWarm uses the blower door test results for the home, the weather data for the house site, and the stack height of the building, to provide an estimate of the natural infiltration by month. The model used is the Lawrence Berkeley Laboratory infiltration model, see “The Prediction of Air Infiltration”, LBL-19040, M. Sherman and B Dickinson, July 1985, for details. Some fixed assumptions are utilized in the model, as these are not provided as inputs by the user.

This routine also includes calculating a weighted average of living space and cool space temperature; currently using above-grade area for the weighting. It does not account for temperature setback at night if present, or overheating during day. (This indoor temperature adjustment is not a significant issue in infiltration calculation.)

##### A. Input Parameters

> ACH50: Blower Door test results, in air changes per hour at 50 Pascals
>
> Volume: Conditioned house volume, cubic feet
>
> Stack Height: Difference in height between lowest leak and highest leak, in feet
>
> Indoor T: the average indoor temperature (deg. F) that drives the stack effect for the year. (The calculation does not account for monthly variations of this temperature). This temperature should account for the fact that some of the leakage occurs through components in the cool temperature locations.
>
> Outdoor temperature: outdoor dry bulb temperatures for each month.
>
> Wind speed: outdoor wind speeds (miles per hour) measured at the airport weather station for each month.
>
> Site Multiplier: a multiplicative factor that converts airport wind speeds to site wind speeds, measured at the height of the top floor ceiling.
>
> Stack Multiplier: the constant that when multiplied by (cfm50)2 \* Stack height \* ∇ T gives the square of the stack effect in units of cfm2 = .00000497899.
>
> Wind Multiplier: (the constant that when multiplied by (cfm50)2 \* (site wind)2gives the square of the wind effect in units of cfm2 = .000067228
>
> These two constants are derived from the LBL model using the following assumptions:
>
> R = 0.5, X = 0, and n (the flow exponent) = 0.67.
>
> Stack Coefficient = Stack Multiplier \* (cfm50) 2 \* stack height
>
> Wind Coefficient = Wind multiplier \* (cfm50)2 \* Site Multiplier

Combining the stack and wind multipliers with the other variables that don’t change by month, determines fixed coefficients for making monthly calculations.

##### B. Output Parameters

> For each month,
>
> Natural Infiltration =(Stack Coefficient \* (IndoorT - OutdoorT (mo)) + Wind Coefficient \* Wind (mo) )2

### <span id="_Toc371140066" class="anchor"><span id="_Toc371140193" class="anchor"></span></span>2.4.2 AKWarm Assesses Mechanical Ventilation 

AKWarm calculates mechanical ventilation flow rate (cfm), electrical use, and additional internal gains. It also calculates the sensible heat recovery efficiency for the system.

##### A. Input parameters are:

> Ventilation type: Type of mechanical ventilation system
>
> Volume: Total volume of living and garage spaces combined
>
> Living Volume Fraction: The fraction of the total volume that is in the living space, as opposed to in cool spaces, not requiring ventilation.
>
> Natural infiltration : monthly natural infiltration values in cfm, total for living and cool temperature spaces.
>
> Living Infiltration Fraction: Fraction of the total infiltration that is in living spaces as opposed to cool spaces
>
> Don’t Add Air: If non-zero, mechanical ventilation air is NOT added to a tight house without a ventilation system
>
> Ignore Fan Heat: if non-zero, the fan heat from hrvs in ignored; sensible efficiency is used as the heat recovery measure, not apparent sensible effectiveness

##### B. Output parameters are:

> Monthly cfm of mechanical ventilation
>
> Apparent Sensible Effectiveness of heat recovery ventilator
>
> Monthly electricity use of the ventilation system added to house total fuel component
>
> Annual electricity use is added to this array containing lights/appliances flue use.

##### Constants Used

Constants that indicate the total ventilation in ACH (natural + mechanical) for various types of ventilation systems. (*Values were policy decisions made by AKWarm committee.)*

> Total ventilation (ACH) in a house that is tight and has no mechanical ventilation system and necessary ventilation air is assumed to be added by opening windows = 0.39
>
> Total ventilation in a house with a ventilation system not having heat recovery = 0.35
>
> Total ventilation in a house with heat recovery ventilation = 0.35

Constants indicating electrical power per cfm of flow for different ventilation systems types

> No Mechanical Ventilation = 0
>
> Ventilation, No Heat Recovery = 2.15
>
> Heat Recovery Ventilation = 3.58

**Average Apparent Sensible Effectiveness of HRV system = 0.7** This model does not vary the effectiveness by month, nor does the model vary by type of HRV. Apparent sensible effectiveness (ASE) is used as the measure of heat recovery instead of sensible efficiency. By doing this internal gains from the unit’s power consumption do not need to be accounted for explicitly. The heat gains from the power are included in the effectiveness of the unit. Since the rating system does not penalize hrv’s for their electrical usage, and the program doesn’t ask for specific hrv specifications, AKWarm uses a conservative average of representative hrv apparent sensible effectiveness values. When fan heat is ignored, sensible efficiency is used as the heat recovery measure. This factor is then netted out of the ASE.

|--------------------------------------------------------------|
| Summary of Constants Used For Various Ventilation Strategies |
|                                                              |
| Total Ventilation (ACH)                                      |
| Electrical Power/cfm                                         |
| Apparent Sensible Effectiveness                              |
| Sensible Efficiency                                          |

For each ventilation type, AKWarm determines target total ventilation cfm (natural infiltration + mechanical ventilation), power use per cfm ((Btu/hr)/cfm), and apparent sensible effectiveness.

> 1. Determine living volume as a fraction of the total volume.
>
> 2. Determine Natural infiltration into living space for each month. (cfm)
>
> 3. Calculate mechanical ventilation for each month (cfm). Add only enough air to bring up to total cfm. Add no air if a month has natural infiltration \> Total cfm.
>
> 4. Assign the Apparent Sensible Effectiveness for each month.
>
> 5. Calculate power use from the ventilation system.

### <span id="_Toc371140067" class="anchor"><span id="_Toc371140194" class="anchor"></span></span>2.4.3 Net Ventilation Heat Loss 

AKWarm calculates the UA values (by month) associated with natural infiltration and mechanical ventilation. Separate calculations are made based on the temperature of the space where the exfiltration is occurring (living, semi-conditioned).

##### A. Input parameters

> Natural infiltration, cfm, by month
>
> Mechanical ventilation, cfm, by month
>
> Sensible heat recovery efficiency of the ventilation system by month, decimal fraction
>
> Fraction of natural infiltration that exfiltrates from cool spaces
>
> Heat Cap60 + Heat capacity of air, Btu/deg. F/ft3 \* 60 minutes/hr

##### B. Output parameters

> UA Air: Effective UA by month and by temperature; *two values: living and cool*
>
> All of the mechanical ventilation air is assumed to leave from living temperature spaces

Looping through the months:

UA Air = Heat Capacity60 \* (Natural Infiltration \* (1 - cool fraction) + vent cfm + Vent ASE))<span id="_Toc371140068" class="anchor"><span id="_Toc371140195" class="anchor"></span></span>

### 2.4.4 Gross Heat Loss

AKWarm combines these results and calculates the gross heat loss for the home, including shell losses, infiltration losses and mechanical ventilation.

<span id="_Toc371140069" class="anchor"><span id="_Toc371140196" class="anchor"><span id="_Toc371146341" class="anchor"></span></span></span>Chapter 3 Building Heat Gains
==========================================================================================================================================================================

<span id="_Toc371140070" class="anchor"><span id="_Toc371140197" class="anchor"><span id="_Toc371146342" class="anchor"></span></span></span>3.1 AKWarm calculates internal gains 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### <span id="_Toc371140071" class="anchor"><span id="_Toc371140198" class="anchor"></span></span>3.1.1 Internal gains from occupants

This routine calculates the average Btu/hour of internal gains produced within the home for each month. “Occupants” is the number of occupants that live in the home. The figure below assumes that the average sensible heat gain from the average person (mix of female adults and children) is 62 watts. This is deduced from EEDO’s “Energy Economics of Design Options”: 66 watts for 8am-8pm, and 58 watts for 8pm-8 am. ASHRAE Seated at Theatre is 66 watts for mix of adults and children. Further, calculation assumes that people are not in a residential building for 18% of the day on average (at work, at school, in other buildings, outside). Thus, average sensible heat gain released into residential buildings per person is 62 watts \* 3.413 Btu/hr/watt \* 0.82 = 174 Btu/hr.

### <span id="_Toc371140072" class="anchor"><span id="_Toc371140199" class="anchor"></span></span>3.1.2 Internal gains from lights and appliances

AKWarm calculates fuel (including electric) use and internal gains associated with lights and appliances, not including DHW, the mechanical ventilation system, and the auxiliary electricity use of the space heating system. The gains and electric use from these other appliances are treated separately.

#### Clothes Dryer

Determine the internal gains and fuel use of the dryer. (per living unit). Electricity values are taken from analysis of ISER Railbelt End Use survey, Gas values are estimated from the electric values by ratios determined from EEDO program Reference Manual, ver, 1.0; ratio of internal gains to fuel use are also determined from the EEDO program Reference manual.

|-------------|-------------------|------------------------|
| Fuel        | Fuel Use (Btu/hr) | Internal Gain (Btu/hr) |
| Electricity | 425               | 127                    |
| Gas         | 585               | 116                    |
| propane     | 585               | 116                    |

#### Cooking Range

Determine the internal gains and fuel use of the cooking range. Electricity values are taken from analysis of ISER Railbelt End Use survey, Gas values are estimated from the electric values by ratios determined from EEDO program Reference Manual, ver, 1.0; ratio of internal gains to fuel use are also determined from the EEDO program Reference manual.

|-------------|-------------------|------------------------|
| Fuel        | Fuel Use (Btu/hr) | Internal Gain (Btu/hr) |
| Electricity | 294               | 238                    |
| Gas         | 585               | 421                    |
| propane     | 585               | 421                    |

#### Other Lights And Appliances

Determines the electricity use and internal gains form other lights and appliances (not counting domestic hot water heating, space heating and mechanical ventilation systems). Relationship of other electric use to floor area was determined through a statistical regression on ISER Railbelt End Use Data. The regression results were reduced 20% because of an inconsistency of the regression with average utility consumption data.

Other lights and Appliances = .8 \* (1354 + .7784 \* floor area)

##### Modifications of Use 

The user may choose to alter the default electrical use of the home if he is aware that usage is unusually low or high for a home of that size. For instance, in some rural locations the electric load is only lights, while in some urban areas the average load may be increased by the use of hot tubs, electronic equipment and other “add-ons”.

If the user chooses “Low”, AKWarm reduces the total electrical usage by 35%.

If the user chooses “High”, AKWarm increases the total electrical usage by 35%.

To determine internal gains, AKWarm assumes 95% of use is released in the insulated shell. (Some is outdoor lighting, outdoor use, and gain that causes some elevation in heat loss, e.g. hot light fixtures in the top floor ceiling) Hot-2000’s internal gain utilization curve tops out at 95%.

<a name="dhw"></a>
### <span id="_Toc371140073" class="anchor"><span id="_Toc371140200" class="anchor"></span></span>3.1.3 Fuel use and internal gains associated with the domestic hot water heater. 

#### A. Single family or multi-family, single unit buildings

AKWarm approaches this calculation by analyzing the system under GAMA operating conditions to derive a few important characteristics about the system. Then these characteristics are used in an energy calculation based on ACTUAL operating conditions of the DHW system.

The basic model of the hot water heater is as follows:

3 types of heat load are considered:

> 1. The heat required to raise the temperature of the water flowing through the how water heater (proportional to the amount of hot water consumption:
>
> 2. The conduction of heat out of the hot water storage tank, if one exists;
>
> 3. Other heat losses, which include, at a minimum, the lost energy caused by warm air rising up the flue of a gas/oil hot water heater during the off-cycle (NOT counting on cycle flue loss), thermosiphon heat loss from pipes connecting to the hot water heater (the kind remedied by heat traps), and pilot light loss.

These 3 forms of heat load are assumed to be supplied by a heating element or burner operating at a particular Recovery Efficiency or steady-state efficiency. Heat loads of type 1 and 2 vary from GAMA test conditions to actual operating conditions, and are adjusted in the actual operating condition calculation. The other heat loss, type 3 is assumed to be the same under GAMA conditions and actual conditions. Internal gains are calculated based on the amount of heat load in each category, the location of the water heater, and the water heater fuel type.

Note: Nothing is currently done with Heat Pump Type variable. In the future, the EF could be adjusted for climate in the case of a ground source heat pump.

**Constants used:**

> Air Film R-value = .68
>
> Surface Area = 30 sq. Ft (tank area)
>
> Ambient temperature (deg. F) in GAMA test = 75
>
> Inlet water temperature (deg. F) in GAMA test = 58
>
> Tank water temperature (deg. F) in GAMA test = 135
>
> Total gallows per day of consumption in GAMA = 64

**Assumptions about ACTUAL operating conditions:**

> Fraction of tank surface area covered by insulation = .9
>
> Assumed R-value of water heater blanket = 6
>
> Average annual temperature of conditioned space = 71
>
> Average annual temperature of semi-conditioned space = 57
>
> Average annual temperature of unconditioned space = 40
>
> Inlet water temperature = 45
>
> Tank water temperature = 135
>
> Gallons per person per day of hot water = 20
>
> Fraction of loss added to internal gains for heater location:
>
> conditioned space = 1
>
> semi-conditioned space = .65
>
> unconditioned space = 0

If the user supplies an energy factor AKWarm will use it, otherwise it uses the default value for the described water heater listed in the energy library.

**To evaluate domestic water heaters in multifamily buildings:**

A. Convert the recovery efficiency into a decimal fraction for use in the rest of the routine, making sure the recovery efficiency is at least 1% higher than the energy factor.

The main reason for analyzing the system under GAMA conditions is to estimate the “Other” heat loss. The second reason is to make sure that the Tank R-value and surface area estimates are consistent with the unit’s Energy Factor and Recovery Efficiency. If they are inconsistent with those ratings, they are adjusted in this calculation.

GAMA Water heat-up load in Btu/hr. Use a constant for speed

B. Assign the water heat-up load to a variable so calculation is similar in appearance to actual operating condition calculation.

1. Calculate the fuel consumption of water heater under GAMA conditions

1.  Calculate GAMA conduction load. If tankless, assume 0 conduction load.

2.  Derive the “Other” load from what’s left over after netting out water load and conduction load out of total load. Total Load is Fuel Use times the Recovery Efficiency (Steady state efficiency)

Other Load = Fuel use \* Recover Efficiency - Water Load - Conduction Load

2. Analyze under Actual Operating Conditions

Now we have the other Load, which is assumed to remain constant under actual operating conditions, and we have a surface area and R-value estimate that is consistent with the GAMA ratings.

Water Load = consumption per person \* Occupants/24\*8.33 \* (Tank temperature - Inlet temperature)

**Tank Conduction load**:

1.  If a tank exists:

2.  If it is a tankless water heater, the conduction load is of course 0.

Total fuel use is determined by the total load supplied through an efficiency of recovery efficiency:

Fuel Use = (Water Load + conduction Load + Other Load)/ Recovery Efficiency

3. Contribution to Internal Gains

For electric water heaters, there is no flue loss so all of the conduction loss and other loss generates heat at the water heater location: Internal Gain = conduction load + other load

If the recovery efficiency is less than 1 then :

Gain + Gain + (1-Recovery Efficiency) \* Fuel Use

For gas and oil heaters: most of the other load is warm air going up the flue. Some of this heat conducts through the flue pipe into space near the heater but most is lost. Some of the other load is thermosiphon heat loss in nearby pipes and does add to gain. Credit 20% of the other load as gain and all of the conduction load.

Internal gain = conduction load + other load \*.2

#### B. Multi-Family, When Rating Whole Building

When dealing with large systems, many of the above factors don’t apply, so a simpler energy factor calculation is acceptable here.

1. Calculate fuel use based on the water heating load and the overall energy factor of the unit:

> Water heat-up Load = consumption per person \* occupants/24\*8.33\* (tank temperature - ambient temperature)
>
> Fuel use = water heat-up load/EF

2. Apply a location effect to the gain because gain into semi and unconditioned space is not 100%.

> If electric, all loss goes into space (gain constant = 1).
>
> If fuel-fired, assume half of loss is gain into space around water heater (gain constant = .5). :
>
> Gain = (fuel use - water load) \* (gain constant)

4. As HOT-2000 does, add 3% of the water load as gain because some heat is lost from the DHW hot water pipes directly into conditioned space

Annual DHW fuel use in MMBTu = (Water Load / EF) \* 008766

<span id="_Toc371140074" class="anchor"><span id="_Toc371140201" class="anchor"><span id="_Toc371146343" class="anchor"></span></span></span>3.2 AKWarm Calculates Passive Solar Heat Gains 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### <span id="_Toc371140075" class="anchor"><span id="_Toc371140202" class="anchor"></span></span>3.2.1 Solar Area

First, AKWarm calculates, for each solar source (window or wall/door) and solar orientation: vertical, south, vertical non-south, and horizontal, the amount of area that actually contributes to passive solar heat gains. This is the sum of component’s area \* Solar Heat Gain Coefficient (SHGC) \* Shading Multiplier

##### A. Input Parameters

tShell = description of each shell component

Site Wind = the site wind speed, measured at the top-floor ceiling height, miles per hour.

##### B. Output Parameters

Solar Area = Sum of Area \* SHGC \* Shading Multiplier for each solar source window or wall/door) and orientation. For windows, the solar area is determined by “south” and “not-south” inputs. For walls and doors it is automatically split to 1/4 south and 3/4 non-south.

The Solar Heat Gain Coefficient (SHGC) is the ratio of solar heat admitted into the building to the solar energy incident on the surface. The SHGC is calculated for 1) a wall or door with a specific R-value and outer surface wind speed, and 2) for a window.

1. Wall or Door SHGC =

ABSORB \* FilmRActual/(R-Value - FilmR-assumed + FilmR-Actual)

where:

> ABSORB = a solar absorptance constant: the assumed solar absorptance of the outer surface of the wall or door. This value is assumed as .4 (consistent with HOT2000).
>
> Film R-actual = film R-value at actual wind speed
>
> Film R-assumed = film R-value at assumed wind speed

The average wind speed on the walls and doors of the home is less than the site wind speed because some walls are on the leeward side of the house, and wall surfaces are lower than top-floor ceiling height.

2. Window SHGC = sc \* GLASS SC MULT = WTD FRAME SHGC

where

> sc = shading coefficient of window glass, taken from AKWarm Energy Library for type of glass described. These values are from ASHRAE 1993 Fundamentals, p 27.19.
>
> The SHGC/sc ratio for normal incidence angles: 0.87
>
> Off normal incidence modifier: corrects for non-normal incidence. Because of low Alaskan sun angles AKWarm uses a value corresponding to approximately 25 degrees. This adjustment comes from ASHRAE 1993 Fundamentals, Figure 18 p 27.17.
>
> GLASS SC MULT = Window Covering Modifier that corrects for use of interior window coverings such as draperies. Data as to the amount of window covering typically found in Alaskan homes came from a brief survey conducted by Analysis North. Analysis of the survey data is performed on the AKWarm.XLS spreadsheet
>
> WTD FRAME SHGC = Effect of Window Frame on Solar Heat Gain. The window frame has a different SHGC than the window. The two sections must be averaged together. AKWarm assumes an NFRC size AA window with a wood frame and uses window dimensions given in ASHRAE Fundamentals

Shading external to the building is NOT accounted for in this function, but in the following shading multiplier. Dirt on the glazing is not accounted for.

#### Shading Multiplier

The shading multiplier is the multiplier used to adjust the solar incident on a window, wall, or door due to external shading. The constant is based on user input of the amount of external shading, and is as follows:

> Little External Shading = 0.9
>
> Moderate External Shading = 0.7
>
> Heavy External Shading = 0.5

### <span id="_Toc371140076" class="anchor"><span id="_Toc371140203" class="anchor"></span></span>3.2.2 Gross Solar Gain

Next, AKWarm calculates the *gross* solar gain admitted into the home.

##### A. Inputs

Solar Area: The Area \* SHGC \* Shading Multiplier\* ft2

Wx Solar: The solar incident on a surface by month and orientation, Btu/hr/ft2

##### B. Output

Solar Gain: The gross solar gain admitted into the building by month and by orientation, including the total across all orientations.

1. Loop through each month and calculate total gross solar gain by orientation.

Gross Solar Gain = Solar Area \* Solar Radiation per ft2.

### <span id="_Toc371140077" class="anchor"><span id="_Toc371140204" class="anchor"></span></span>3.2.3 Estimate of Building Thermal Mass

Next AKWarm calculates the living space thermal mass for purposes of estimating the utilization of solar gains. It ignores mass in cool temperature zones, based on the assumption that most solar gains are admitted to the living space, and mass in the cool zones is isolated from the living space.

> Thermal mass = Living space floor area \* Mass constant
>
> Mass Constant (per square foot) for Standard and Heavy Construction
>
> 3.5 Btu/deg. F/ft2 for standard frame construction
>
> 7 Btu/deg. F/ft2 for heavy construction

<span id="_Toc371140078" class="anchor"><span id="_Toc371140205" class="anchor"><span id="_Toc371146344" class="anchor"></span></span></span>3.3 Heating System Performance
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

AKWarm analyzes the primary and secondary heating systems to determine distribution system losses, heating plant losses, and fuel use (including auxiliary pump/fan electric use).

### <span id="_Toc371140079" class="anchor"><span id="_Toc371140206" class="anchor"></span></span>Primary or secondary Heating System Energy Use

This routine calculates the energy use of the primary and secondary heating systems.

##### A. Input Parameters

> Load on the heating systems, by month and by system, Btu/hr
>
> Description of the heating systems

##### B. Output Parameters

> Losses from the heating system, by month and by system, Btu/hr
>
> Efficiency of heating plant, distribution system, and combined efficiency for each system (decimal fraction)
>
> Fuel use (both main and auxiliary) of heating system are added to House total fuel use (by month and fuel type), Btu/hr
>
> Annual fuel use for space heating by fuel type, MMBtu/yr
>
> (Only the main fuel use (not auxiliary) is included)
>
> Annual Auxiliary electricity use of heating system is added to this total, MMBtu/yr

##### 3.3.1 Calculate the efficiency of the heating plant

Normally the (Steady state - AFUE) adjustment factor (expressed as decimal fraction) is taken from the energy library table. This may be overridden later if the user enters a very high AFUE

To determine AFUE, AKWarm’s first priority is to use the combustion efficiency test adjusted for (Steady State -AFUE) difference; its second priority is the user-supplied AFUE, and the third choice is the default AFUE from the Energy Library.

AKWarm adjusts the AFUE for the add-on devices present, using the following method.

Each device is characterized by three parameters that describe its impact on heating system efficiency:

1) the device can reduce the heating system part-load losses by a particular percentage;

2) the device can reduce the heating system part-load losses by an absolute amount e.g. 2%; and

3) the device can increase the steady-state efficiency of the system by some absolute percentage, e.g. 3%.

Any combination of the three parameters can be used to describe one device. When accounting for the total impact of multiple upgrade devices, the absolute effects (1 and 3) are added together without any account for interaction. The percentage reductions in part-load losses for multiple devices are accounted for by multiplying together (1 - Percentage reduction) for each device.

AKWarm loops through all the upgrade devices; if the device is present, it accounts for its effect and then adds all effects. Next, AKWarm adjusts the AFUE for the effects of the upgrade devices.

First the change in the part-load losses is calculated. Assume that all the difference between steady-state and AFUE is part-load loss. To get the new part-load losses, AKWarm nets out the absolute decrease and then apply the part-load multiplier. The AFUE is adjusted by increasing it by the steady-state efficiency increase and increasing it by the reduction in part-load losses. AFUE = AFUE + Ss-increase + (origPL - New PL)

##### 3.3.2 Calculate the efficiency of the distribution system

These calculations deal with the conduction loss fractions for ductwork and piping for various types of space and levels of insulation. Only two levels of insulation are currently supported: insulated and uninsulated. Loss fractions are losses/input to distribution system.

For each distribution type, determine: 1. conduction loss and 2. duct leakage loss and then 3. the fraction of these losses that is truly lost as far as offsetting any heating demand.

**A. Conduction Loss**

Start by determining conduction loss, based on user-defined descriptions of duct system

Conduction loss percentages,

> For direct distribution, efficiency is 100% , so conduction loss = 0

|-------------------------------------|--------------------------|------------------------|
|                                     | Ductwork conduction loss | Piping conduction loss |
| unconditioned space, insulated      | 0.087                    | 0.046                  |
| unconditioned space, uninsulated    | 0.506                    | 0.164                  |
| semi-conditioned space, insulated   | 0.067                    | 0.037                  |
| semi-conditioned space, uninsulated | 0.394                    | 0.121                  |
| conditioned space, insulated        | 0.057                    | 0.033                  |
| conditioned space, uninsulated      | 0.339                    | 0.11                   |

**B. Duct Leakage**

If distribution type is ductwork, it is necessary to adjust for duct leakage. This approach assumes that the leakage efficiency multiplies the conduction efficiency. As opposed to a method of adding conduction loss to leakage loss, this method protects against total losses exceeding 100%. It also more closely mimics reality.

Duct Leakage loss factors:

> Tightly sealed ducts = 0.05
>
> Moderately sealed ducts = 0.15
>
> Leaky ducts = 0.3

For each location and insulation level of ductwork:

> Duct Loss = 1- (1 - Conduction Loss)) \* (1 - Duct leakage loss factor)
>
> Convert the location percentages into decimal fractions and calculate the fraction of the distribution system in conditioned space.

**3.3.1.2.3. Useable Fraction of System Losses**

Depending on the location of the distribution system in relation to conditioned space, there may be some fraction of the distribution system loss that is truly lost and is unusable to offset heating demand. (Note that using 0 for distribution located in conditioned space results in 100% heating system efficiency for distribution located in conditioned space. This is not completely true. Leaky ductwork in conditioned space can pressurize spaces and accentuate air leakage, thus causing inefficiency.)

> Unusable Fraction for Distribution in unconditioned space = 1
>
> Unusable Fraction for Distribution in semi-conditioned space = 0.2
>
> Unusable Fraction for Distribution in conditioned space = 0 (says all loss is useable)

To determine the overall average loss fraction for the distribution system, account for the un-useability of loss in each space type and weight by the fraction of the system that is in each space type.

Overall average loss fraction = AvgLoss + Loss \* Unusable Fraction \* LocFrac

Distribution system efficiency is 1 - the loss fraction.

C. Calculate the combined efficiency

<span id="_Toc371140080" class="anchor"><span id="_Toc371140207" class="anchor"><span id="_Toc371146345" class="anchor"></span></span></span>Chapter 4 Putting It All Together
==============================================================================================================================================================================

<span id="_Toc371140081" class="anchor"><span id="_Toc371140208" class="anchor"><span id="_Toc371146346" class="anchor"></span></span></span>4.1 Heating Load
-------------------------------------------------------------------------------------------------------------------------------------------------------------

AKWarm calculates a residential heating load by *estimating* the maximum probable heat loss of each space to be heated and the simultaneous maximum loss for the building, while maintaining a selected indoor air temperature during periods of design outdoor weather conditions. Any useable solar and internal gains are subtracted from the gross heat loss calculation to determine the net load on the heating system. The design heat load is an estimate of the *rate* at which a building loses heat during the *near minimum* outdoor temperature.

### <span id="_Toc371140082" class="anchor"><span id="_Toc371140209" class="anchor"></span></span>4.1.1 Why an “estimate”?

It is not possible to fully account for the hundreds of construction details and thermal imperfections in an object as complex as a building. Among the factors that add uncertainty to the calculation are:

1.  Imperfect installation of insulation materials

2.  Variability in R-value of insulation materials

3.  Shrinkage of building materials leading to greater air leakage

4.  Complex heat transfer paths at wall corners and other intersecting surfaces

5.  Effect of wind direction on building air leakage

6.  Overall construction quality

7.  People traffic into and out of the building

### <span id="_Toc371140083" class="anchor"><span id="_Toc371140210" class="anchor"></span></span>4.1.2 Why “rate”?

Heat load is not the number of BTUs of heat loss, but the rate at which heat is lost given in BTUs per hour. When the rate at which the heat gains including solar gains, internal gains from people and appliances and the heating system injecting heat into the building - matches the rate at which the building loses heat, the indoor temperature will remain constant.

### <span id="_Toc371140084" class="anchor"><span id="_Toc371140211" class="anchor"></span></span>4.1.3 Why “near minimum”?

The design heating load is estimated assuming the outside temperature is near its minimum value. This temperature, specifically called the **97.5% design dry bulb temperature**, is not the absolute minimum temperature for the location. Rather it is the temperature the outside air is at or above during 97.5% of the year. Although outside temperatures do occasionally go below this design temperature, the duration of these low temperature periods is so short that buildings tend to “coast” through them using heat stored in their thermal mass. When outside temperatures are above the design temperature, the rate of heat flow from the building will be less. If heating systems were designed for maximum weather conditions, excess capacity would exist during most of the system’s operating life.

AKWarm calculates *building* heating load, rather than room by room heating load. It is useful for selecting the heating capacity of the heat source, and performing estimates for annual heating energy usage. However, this single number is not necessarily useful for designing the heating distribution system, because individual rooms often have heating loads that are not proportional to their floor area.

Heat flows through all building surfaces that separate heated space from unheated space. Together these surfaces (walls, windows, ceilings, doors, foundation etc.) are called the **thermal envelope** of the building. It is only necessary to calculate heat flow through the surfaces that together constitute this thermal envelope. Other walls, ceilings, etc. that have heated space on both sides and thus are not exposed surfaces are not included in these calculations.

<span id="_Toc371140085" class="anchor"><span id="_Toc371140212" class="anchor"><span id="_Toc371146347" class="anchor"></span></span></span>4.2 Useful solar and internal gains
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Solar and internal heat gains to a building are only useful when they offset the need for additional heating because of heat loss. AKWarm uses the monthly weather data for the building site to determine which are the useable portion of the gross internal and gross solar gains to the building.

### <span id="_Toc371140086" class="anchor"><span id="_Toc371140213" class="anchor"></span></span>4.2.1 Calculate the useable portion of the gross internal gains

This routine calculates the useable internal gains (i.e. those gains that offset the use of space heating fuel).

##### A. Inputs

IntGainGross = gross internal gains by month and space temperature, Btu/hr

LossGross = gross heat loss by month, Btu/hr

##### B. Output

IntGainNet = The useable internal gains by month, Btu/hr

The algorithm used is described in the Hot-2000 Technical manual, version 6, Ch.7, “Internal Heat Gains”. The Hot-2000 curve maximizes at 0.95, presumably to account for some gains that are not released within the insulated shell. In AKWarm these gains have already been netted out prior to this routine and do not appear in this calculation. An adjustment was made to the Hot-2000 algorithm to reconcile this difference.

##### Calculate ratio of gross internal gains to gross heat loss (GLR)

For each month, AKWarm calculates a gain-to-load ratio:

> GLR = IntGainGross(mo)/LossGross(mo)/0.95

If GLR \<=0.5, then internal gains fully utilized and IntGainNet (mo) = IntGainGross (mo)

If GLR \> 5, then gains are partially utilized, but gains don’t entirely satisfy load so

IntGainNet(mo) = (IntGainGross (mo)/0.95) \* Utilization multiplier

Utilization multiplier = (0.1999966 + 2.674634 \* GLR^0.9047617)/(1 + 2.674634 \* GLR^1.9047617)

If GLR between 0.5 and 5, then gains are partially utilized and entirely satisfy load, so IntGainNet(mo) = LossGross(mo)

##### Calculate thermal mass 

Next AKWarm calculates the living space thermal mass for purposes of estimating the utilization of solar gains. It ignores mass in cool temperature zones, based on the assumption that most solar gains are admitted to the living space, and mass in the cool zones is isolated from the living space.

Thermal mass = Living space floor area \* Mass constant

Mass Constant (per square foot) for Standard and Heavy Construction:

> 3.5 Btu/deg. F/ft2 for standard frame construction
>
> 7 Btu/deg. F/ft2 for heavy construction

### <span id="_Toc371140087" class="anchor"><span id="_Toc371140214" class="anchor"></span></span>4.2.2 Calculate the useable portion of the gross solar gains

Next AKWarm calculates the useable portion of the total solar gains admitted to the building. It uses the algorithm presented in the HOT-2000 Technical Manual, version 6, Chapter 6, “Passive Solar Gains”.

A. Input Parameters

> Gross solar gains by month, Btu/hr
>
> Gross heat loss from the building by month, Btu/hr
>
> Useable internal gains by month, Btu/hr
>
> Thermal mass of the living space (does not include mass in the cool temperature zones)

B. Output Parameters

> Solar utilization fraction for each month, dimensionless
>
> Utilized solar for each month, Btu/hr

The solar utilization factor is expressed as a function of 1) gain-to-load ratio(GLR) and 2) mass-to-gain ratio (MGR) for the living space, not counting cool temperature spaces. The routine implicitly assumes that the solar gain is primarily admitted to the living space, not the cool temperature space. This reduces the solar usability somewhat, but a compensating assumption made in the routine is that the occupants will allow a temperature swing of 5.5 degrees, which is somewhat high.

There are some anomalies in the 2.75 deg. C temperature swing curves, so the 5.5 deg. C curve was used instead. Also, the curve fit has problems beyond a GLR of 3, so usability was set to 1/GLR in that range.

Loop through each month

##### Calculate the gain to load ratio (GLR)

The gain-to-load ratio is the ratio of the solar gain to the net heating load. The net heating load is the amount of heating energy required, in the absence of solar gains and including useful internal heat gains, to maintain the house temperature at the thermostat setting. AKWarm assumes that the internal heat gains are used first to offset a portion of the space heating load, since they are uncontrollable gains resulting from the daily operation of the home.

To net out useable internal gains: Assume that useable internal gains offset the same percentage of the living space and cool space heat loss. Assume that all solar gains are admitted to the living space and none to the cool space.

Ratio of (loss with useable internal netted out) to (total loss). This ratio is calculated for whole building (living + cool), but is assumed to be the same in each separate zone.

Net Gross Loss Ratio = (LossGr (mo,TempTotal) - IntGainNet(mo)) / LossGr(mo, Temp Total)

##### Calculate Useable Solar For Month (SolarNet)

A. If GLR \< 3, then calculate mass to gain ratio (MGR)

MGR = Living Area Mass / SolarGross per month

Determine the correct curve fit coefficients for solar utilization. A temperature swing of 5.5 deg. C (9.9 deg. F) is assumed.

Light: If MGR\<= 1.2, then a = 1.112; b = -0.2334; c = 0.866; d = -0.2611

Med/heavy: If MGR \<=2.722, then a = 1.01; b = 0.4038; c = 0.5574; d = 0.3084

Heavy If MGR\<=6, then a = 0.995; b = 0.0822, c = 0.04319; d = 0.3084

Very Heavy If MGR\>6, then a = 0.9863; b = 0.07736; c = -0.05354; d =0.3437

SolarUtiliz (mo) = (a + b \* GLR) / (1 +c \* GLR + d \* GLR \* GLR)

Calculate Useable Solar for Month:

SolarNet (mo) = SolarGr (mo, total) \* SolarUtiliz (mo)

B. If GLR is \>=3, then Solar satisfies entire net living space load

SolarUtiliz (mo) = 1/GLR

SolarNet (mo) = NegGrossLossRatio \* LossGr (mo, Temp Living)

<span id="_Toc371140088" class="anchor"><span id="_Toc371140215" class="anchor"><span id="_Toc371146348" class="anchor"></span></span></span>4.3 AKWarm calculates the net load on the heating systems.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### <span id="_Toc371140089" class="anchor"><span id="_Toc371140216" class="anchor"></span></span>4.3.1. Net out Useable internal and solar gains

This routine calculates the net space heating load resulting after netting out useable internal and solar gains from total losses.

##### A. Inputs

> Total losses by month and temperature, Btu/hr
>
> Useable internal gains by month, Btu/hr
>
> Useable solar gains by month, Btu/hr

##### B. Output

> Net space heating load by month, Btu/hr

LoadNet (mo) = LossGr (mo, TempTotal) - IntGainNet (mo) - SolarNet (mo)

### <span id="_Toc371140090" class="anchor"><span id="_Toc371140217" class="anchor"></span></span>4.3.2. Partition the net load across the primary and secondary heating systems.

Next AKWarm splits the net heating load across the primary and secondary heating system, depending on the user’s estimate as to how much the secondary heating system is used.

##### A. Inputs

> Total net heating load by month, Btu/hr
>
> Description of the secondary heating system

##### B. Output Parameter

> Load on primary and secondary heating systems by month, Btu/hr

1. Determine fraction of load supplied by secondary system

|----------------------|--------------------|
| Secondary System Use | Secondary Fraction |
| None                 | 0                  |
| Low                  | 0.1                |
| Some                 | 0.25               |
| Moderate             | 0.4                |

2. Split the load by month

HtgSysLoad (mo, Htr Primary) = TotalLoad(mo) \* PriFrac

HtgSysLoad (mo, Htr Secondary) = TotalLoad (mo) \* SecFrac

### <span id="_Toc371140091" class="anchor"><span id="_Toc371140218" class="anchor"></span></span>4.3.3 Calculate the impact of a setback thermostat 

This routine calculates the amount that the average daily living space temperature is lowered due to the presence of a night setback thermostat (if one is present).

##### A. Input parameters

> Setback Coverage: Indicates presence of setback thermostat, and how much of home is controlled by it.
>
> Heating Setpoint: Daytime heating setpoint (deg. F).
>
> Outdoor temperature: Outdoor dry bulb temperatures for each month, (deg. F)
>
> Internal Gain: Average internal gains for each month, (Btu/hr)
>
> UAShell: Shell component UA values, Btu/hr/deg. F
>
> UA Air: Effective UA values for air flow from natural infiltration and mechanical ventilation , Btu/hr/deg. F
>
> Mass: Indicates the level of thermal mass in the home
>
> Estimate of Building Thermal mass
>
> (This function returns an estimate of the building’s thermal mass for purposes of estimating the utilization of solar gains. It ignores mass in cool temperature zones, based on the assumption that most solar gains are admitted to the living space, and mass in the cool zones is isolated from the living space. )
>
> Thermal mass = Living space floor area \* Mass constant
>
> Mass Constant (per square foot) for Standard and Heavy Construction
>
> 3.5 Btu/deg. F/ft2 for standard frame construction
>
> 7 Btu/deg. F/ft2 for heavy construction
>
> Floor Area: Square feet of living floor area (doesn’t include cool spaces)
>
> Setback Effect: monthly average indoor temperature depressions due to the setback thermostat
>
> Number of degrees F the temperature is assumed to be set back at night = 7°
>
> Number of hours the temperature is assumed to be set back at night = 8 hours

##### B. Output Parameters

> AKWarm loops through each month and calculates setback effect:

1.  Determine the total UA for the living space for the month

<!-- -->

1.  Total UA= UA Shell (living space) + UA Air (month, living space)

<!-- -->

1.  Estimate the night-time internal gains as 60% of the average value (assumes that gains are released into living space, not cool space)

<!-- -->

1.  Estimate the night-time outdoor temperature as 4.5 degrees below the daily average temperature (relationship displayed by Fairbanks weather data).

<!-- -->

1.  Calculate the setback effect, assuming entire home is setback.

> If the setback only controls half the home, reduce the effect by 60%. Warm space adjacent to setback space inhibits the ability of setback space to decrease in temperature; thus, the reduction should be more than 50%.

<span id="_Toc371140092" class="anchor"><span id="_Toc371140219" class="anchor"><span id="_Toc371146349" class="anchor"></span></span></span>4.4 Annual Fuel Use and Fuel Costs
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The AKWarm reports displayed on the screen and in print-out format list the results of energy use calculations in several ways. An estimate of annual fuel use and cost for each fuel type (electricity, gas, oil, coal, wood), and an estimate of fuel use and cost for each energy use (space heating, domestic water heating, and appliance fuel).

### <span id="_Toc371140093" class="anchor"><span id="_Toc371140220" class="anchor"></span></span>4.4.1 Annual Fuel Use

This routine calculates the total fuel use in MMBtu for each fuel type.

Total Fuel = Space Heating Fuel + DHW Fuel + Appliance Fuel

### <span id="_Toc371140094" class="anchor"><span id="_Toc371140221" class="anchor"></span></span>4.4.2 Energy Cost By Source

This final routine in the energy use calculations takes the monthly use values for electric and gas utility calculations and annual fuel use for other fuel types.

For electric and gas utilities, monthly cost is started at the customer charge and energy use is added by block of usage charge.

Remaining fuels are calculated as annual quantities since there are no customer charges and use blocks.

Total Fuel Cost = Total Cost for Electric + Total Cost For Each Fuel

### <span id="_Toc371140095" class="anchor"><span id="_Toc371140222" class="anchor"></span></span>4.4.3 Energy Cost By End Use

Energy cost for space heating, domestic hot water heating, and lights/appliances split into categories. Domestic hot water and lights/appliance each occupy one category; space heating is split by shell component type and heating system loss; all useable

<span id="_Toc371140096" class="anchor"><span id="_Toc371140223" class="anchor"><span id="_Toc371146350" class="anchor"></span></span></span>Chapter 5 The AKWarm Rating
========================================================================================================================================================================

<span id="_Toc371140097" class="anchor"><span id="_Toc371140224" class="anchor"><span id="_Toc371146351" class="anchor"></span></span></span>5.1 Introduction
-------------------------------------------------------------------------------------------------------------------------------------------------------------

A home energy rating system (HERS) is used to assess and assign a descriptive rating to the energy performance of a building. Accurate energy analysis systems are prerequisites for financing residential energy efficiency through the mortgage process with energy efficient mortgages (EEMs) and energy efficient loans. AKWarm provides this service in the form of certificates and energy use reports that are useful for financial institutions, home owners and others.

AKWarm ratings and EEMs may be applied to site constructed or manufactured residential buildings of the following types: detached single-family, attached single-family, individually conditioned; and attached single-family, centrally conditioned. Both new and existing homes may receive AKWarm ratings at the time of sale. Any home which meets the established rating threshold for an energy efficient mortgage would be eligible for an EEM.

Owners of existing homes wishing to improve the energy efficiency of their home may also have their home rated. Homeowners may be eligible for energy efficient home improvement loans for the implementation of energy conservation measures. The home will receive a pre-retrofit rating and specific energy conservation measures and associated estimations of energy cost savings will be identified. A predicted rating (which assumes all identified measures are implemented) will also be prepared. Finally, a post-retrofit rating can be performed to determine the home’s ratting in the event that not all of the identified energy conservation measures are implemented.

Proposed (to-be-built) homes may receive a “projected rating based on plans” if complete building plans and specifications for minimum rated features are available. To receive a final rating, a site inspection of the completed home must be conducted.

<span id="_Toc371140098" class="anchor"><span id="_Toc371140225" class="anchor"><span id="_Toc371146352" class="anchor"></span></span></span>5.2 Rating Procedure
-----------------------------------------------------------------------------------------------------------------------------------------------------------------

To determine the appropriate rating, three estimates of annual purchased energy consumption must be made:

1) an estimate of the energy usage (source BTU’s) of the rated home as built (or proposed) and

2) an estimate of the energy usage (source BTU’s) of the rated home if it were reconfigured to exclude and/or include specific energy efficiency features - the reference home, and

3) an estimate of the energy use (source BTU’s) of the rated home in a “best-case” (100 points) situation.

For home improvement ratings, an additional estimate must be made of the rated home re-configured to include the proposed energy efficient measures.

A comparison of the estimates will yield the energy efficiency rating of the home and/or the home with the proposed conservation measures installed. Currently, the reference home is assumed to score 83 points on the 0 to 100 point scale. A rated home with the same annual purchased energy costs as its associated reference home would also score 83 points.

Energy consumption is estimated using AKWarm’s internal computer based on calculations involving the efficiency of the thermal envelope (including orientation an shading factors), the efficiency of the heating and hot water systems, and other major electrical loads. These minimum rated features are described below.

### <span id="_Toc371140099" class="anchor"><span id="_Toc371140226" class="anchor"></span></span>5.2.1 Standardization of Operating Conditions

AKWarm standardizes the occupancy-related variables of the home being rated to ensure that the physical characteristics of the home are rated, not the occupants. This routine also deletes all garage components from the home, since the garage is not considered in the rating process. It also reduces the volume of the home if there is a garage, since the blower door test includes the garage.

1.  Occupancy: Using information from the Railbelt End Use Study and other Alaksan studies, the following method is used to set the number of occupants to the average level for this size home:

> For single family homes, Standard Occupancy = 2.29 + .000411 \* Average Floor Area
>
> For multi-family buildings, standard occupancy is Standard Occupancy \* \# Living Units

1.  Wind shielding is set to ***Average***, because it is not considered in the rating.

2.  The volume of the home is reduced by the volume of the air in the garage, since the garage is not rated.

3.  Heating Thermostat Setpoint is set to ***70°F***.

4.  Miscellaneous Lights and Other Appliance Use is set to ***Average***.

5.  If no house has no cooking range installed, an electric range is entered for rating purposes. If one exists leave it at the fuel type selected by the user. This only affects internal gains.

6.  If there is no dryer, the rating routine does not add one. This only affects internal gains.

7.  Secondary heating systems are deleted.

8.  Garage components are deleted.

For purposes of the energy rating, AKWarm calculates a Reference House and Best (100 point) House energy use. It takes the approach of modifying certain fields of the home description that are used to calculate energy use. This routine does not modify the underlying physical description of home, but goes directly to the final R-values and efficiencies that are used in the energy calculation routine.

### <span id="_Toc371140100" class="anchor"><span id="_Toc371140227" class="anchor"></span></span>5.2.2 Reference House

1.  Standardize thermal mass to ***Average*** for both reference and best home.

2.  Convert all walls to above grade walls and delete windows and doors.

3.  Convert all ceiling components to attic components, deleting skylights.

4.  Convert floors to above-grade floors.

5.  External shading is set to *Moderate*.

6.  Set Reference house setback thermostat to ***Controls all of Home.***

7.  Set primary heating system characteristics:

Fuel type is the type specified in the rating info type variable

Set AFUE default efficiency to reference level and remove all add-on devices.

Set heating distribution type to ***Direct***.

If reference fuel type is not electric or wood, set auxiliary power use to a value for forced air heating systems.

|------------------------|---------------------|
| Reference Fuel         | Auxiliary Power (%) |
| Gas, Propane           | 4.4                 |
| \#1 Oil, \#2 Oil, Coal | 4.9                 |
| Other                  | 0                   |

The reference home to which the rated home is to be compared has the same configuration as the rated home with the following exceptions: thermal insulation values and mandatory minimum standards for air infiltration, ventilation and appliance standards are set to those listed in the prescriptive standard of the Building Energy Efficiency Standard for the region in which the home is located.

### <span id="_Toc371140101" class="anchor"><span id="_Toc371140228" class="anchor"></span></span>5.2.3 Source BTUs

For rating purposes only, the energy use in MMBTUs is evaluated in relation to the source of the fuel. For each energy source other than electricity, the BTUs/unit for that actual fuel is used. For electricity, the source is considered as either gas or oil, unless the home is located in a city that has hydropower as its source of electricity.

<span id="_Toc371140102" class="anchor"><span id="_Toc371140229" class="anchor"><span id="_Toc371146353" class="anchor"></span></span></span>5.3 Rating Calculations
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

### <span id="_Toc371140103" class="anchor"><span id="_Toc371140230" class="anchor"></span></span>5.3.1 Actual Energy Cost 

AKWarm calculates and reports the energy cost and CO2 production of the home, based on its actual operating characteristics. This component does not use the standardized variables used for the rating.

### <span id="_Toc371140104" class="anchor"><span id="_Toc371140231" class="anchor"></span></span>5.3.2 How AKWarm Calculates Avoided Air Pollution Through Energy Efficiency

When AKWarm provides an energy rating for a home, it will also list the estimated total carbon dioxide (CO2) emissions from the home, based on combined space and electric usage. When improvement measures are chosen the program will display a reduced CO2 emissions (estimated).

When energy efficient improvements are made to a building, savings are at least three-fold. Energy consumption and associated energy costs are reduced, and there is also a societal value of avoided air pollution costs. Carbon dioxide is the most common greenhouse gas produced by human activities, accounting for about 60% of the increase in *radiative forcing* (the measure used to determine the extent to which the atmosphere is trapping heat due to emissions of greenhouse gases) since pre-industrial times. By far the largest source of CO2 emissions is from the oxidation of carbon in fossil fuels, accounting for 70-90% of these emissions.

Carbon dioxide is emitted during the combustion of fossil and biomass fuels. Fossil fuels include coal, oil, and natural gas. For this calculation biomass fuels primarily include wood, charcoal, and agricultural wastes.

The amount of CO2 emitted is directly related to the amount of fuel consumed, the fraction of the fuel that is oxidized, and the carbon content of the fuel.

To estimate emissions of carbon dioxide from fossil and biomass fuels, four steps are performed: 1) required data is obtained; 2) total carbon content in the fuel is estimated; 3) the amount of carbon that is oxidized is estimated; and 4) a conversion is made to total CO2 emissions from energy consumption.

Carbon content varies according to fuel type. We have used the carbon emissions coefficients for each fuel published by EPA in the *State Workbook: Methodologies For Estimating Greenhouse Gas Emissions.*

> *Fuel Type Carbon Emissions Coefficient*
>
> Natural Gas (106Btu) x 32.(lbs C/ 106Btu ) = Total Carbon (lbs C)
>
> Distillate Fuel (106Btu ) x 44.2 (lbs C/106Btu ) = Total Carbon (lbs C)
>
> Other Solid Fuels (106Btu ) x 57.0 (lbs C/ 106Btu ) = Total Carbon (lbs C)
>
> Sub-Bituminous Coal (106Btu ) x 80.0 (lbsC/106Btu ) = Total Carbon (lbs C)

(The values for Alaska sub-bituminous coal were obtained from Usibelli Coal Mine in Healy, Alaska. They are higher than the national average for this type of coal.

The EPA methodology estimates that the percentage of carbon oxidized to carbon dioxide from the combustion of the fuel is 99% for all solid, liquid and gas fossil fuels. Therefore the “total carbon” calculation obtained above is multiplied by .99 to obtain the **total amount of carbon oxidized**.

This figure is then converted to total CO2 emissions by multiplying total carbon oxidized by the molecular weight ration of CO2 to C (44/12) to obtain **Total CO2 Emissions** (lbs/ 106Btu ).

These “Total CO2 Emissions (lbs/ 106Btu )” are then used in calculating the amount of carbon dioxide produced as a result of the energy use in a particular house, and the avoided air pollution through energy efficiency.

AKWarm provides an estimate of CO2 emissions associated with both 1) fuel consumption and 2) electrical usage of a particular house. Each of these values is calculated separately and added together to determine the total annual CO2 emissions of the building that is displayed on the AKWarm reports.

**1) CO2 Emissions Associated With Fuel Consumption - Calculated in AKWarm **

The CO2 emissions associated with fuel consumption are not dealt with in any AKWarm database libraries, but are calculated internally in the program, by multiplying the number of MBtus of each fuel used times the CO2 value listed below for each type of fuel.

1.  AKWarm uses values for CO2 given by US Environmental Protection Agency in “Methodologies For Estimating Greenhouse Gas Emissions, State Workbook” for natural gas, propane, and oil.

2.  Because coal quality varies tremendously, coal values used in AKWarm were obtained from Usibelli Coal Company directly.

3.  No net CO2 emissions are associated with burning wood because growing trees absorb more CO2 than is released when burning wood.

To accomplish this type of analysis, which evaluated the air improvements affects of energy savings, it is necessary to assign a Btu content for each fuel type. AKWarm uses the following conversions for fuel types used in Alaska:

> Natural Gas: 1 therm = 100,000 Btu
>
> 1 ccf = 1.03 therms = 103,000 Btu
>
> 1 mcf = 1,000 cf = 1030 mBtu
>
> Fuel Oil: \#1: 1 gallon = 138,690 Btu
>
> 1 42-gallon barrel = 5.825 x 106Btu
>
> LPG: 1 barrel = 4.011 x 106Btu
>
> Coal: 1 ton = 15.6 x 106Btu

The procedure for determining pounds of CO2 produced is as follows:

Calculate:

**A. For Fuel Oil:**

**B. For natural gas fuel:**

**C. For sub-bituminous coal:**

Using this methodology, the following values for CO2 emissions (lbs/ 106Btu ) were determined for use in AKWarm :

> Natural Gas 116 lb/MBtu
>
> Propane 138 lb/MBtu
>
> Oil\#1 160 lb/MBtu
>
> Oil \#2 140 lb/MBtu
>
> Coal 291 lb/MBtu
>
> Wood 0 lb/MBtu

AKWarm computer uses these figures directly when evaluating non-electric space heating consumption and when computing non-electric space heating savings.

**2) CO2 Emissions Associated With Electricity Consumption - AKWarm Database Library**

For electrical savings, total CO2 emissions are determined for each utility in the state (lbs/kWh), base on the percentages of each fossil fuel used for generating electricity. The data used for electric power utility fuel usage is from the 1994 *Alaska Public Utilities Commission Annual Report: Statistical Information for Fiscal Year 1993,* and the *Alaska Power Statistics* for 1992, published by the Alaska Energy Authority (AEA), now the Dept. of Community & Regional Affairs, Division of Energy. Fuel use and net generation figures are those reported annually to the AEA by each utility. This analysis does not include the inefficiencies associated with transmission losses.

A. Southern Railbelt Utilities

When dealing with the Railbelt utilities, it was decided that, because of the great degree of buying and selling and mixing of electricity from various sources, it would not be possible to determine precisely what each utility’s distinct composite would be and that, for purposes of CO2 production, it would be more efficient to consider the Southern Railbelt as one source.

So, the combined generation of Chugach Electric Association, Anchorage Municipal Light & Power, Homer Electric, Matanuska Electric Association, Seward Electric Association, Alaska Energy Authority-Bradley Lake, and Alaska Power Authority-Eklutna, were combined. The percentages and amounts generated by natural gas, oil and hydropower were determined, and the CO2 was then determined.

1.  This value: 1.1 lbs CO2 /kWh, was used for all of the electric utilities in the Southern Railbelt.

**B. Northern Railbelt Utilities**

When looking at Northern Railbelt utilities, it was more obvious that they were distinct entities with more clearly defined generation and sales. It was decided to analyze each of these utilities separately to determine CO2 emissions.

For purposes of this study, Golden Valley Electric’s power that comes from Bradley lake is considered self-generated. This gives GVEA the total value of hydropower’s lack of CO2 emissions for that amount of power, which was combined with CO2 produced by the electricity generated from coal and oil.

1.  The CO2 emissions for BVEA was determined to be 2.7 lbs CO2 /kWh, when including hydro from Bradley Lake.

Fairbanks Municipal Utilities generated most of its electricity from coal, but also has a district heating plant. To account for the district heating component of FMUS system, we calculated the total \# of gallons of oil saved (assuming 70% heating efficiency) by district heating; then figured the CO2 emissions associated with this and subtracted from the overall FMUS CO2 emissions.

1.  CO2 emissions for Fairbanks Municipal Utilities = 4.6 lbs CO2 /kWh.

**C. Other Electric Utilities in Alaska**

CO2 emissions associated with other electric utilities in Alaska was determined by developing a spreadsheet that made use of the quantities of each fuel consumed and the amount of electricity sold as reported in the *Alaska Power Statistics* for 1992, published by the Alaska Energy Authority (AEA), now the Dept. of Community & Regional Affairs, Division of Energy. The EPA calculation described above was utilized to calculate pounds of CO2 produced per kWh of electricity.

1.  2.  The data reported for some utilities was not reported, or was sometimes inaccurate or incomplete, producing unacceptable results. In some instances, we were able to use 1992 reported data. For some utilities there was no reported data. Those utilities, all with small oil-based generating plants, were assigned a nominal value of 2.2 pounds of CO2 produced per kWh, based on the efficiencies of the other utilities analyzed, and the national average of 2.14 lbs CO2 /kWh.

3.  For those utilities that use a mixture of oil and hydropower for generation, the amount of CO2 produced is based on the amount of oil consumed compared to the total amount of electricity sold, giving credit for the non-CO2 emitting hydropower.

4.  Any utility that included separate generating plants with different efficiencies and distribution lines, was divided into distinct subsets and each community was assigned the one that served it. For instance, Alaska Power and Telephone has five different listings, for both CO2 and utility rates, and communities served by AP&T are assigned the listing for the plant that serves them. This information is provided in the ACCESS Electric Utility Database Library.

5.  Alaska Village Electric Cooperative serves 45 communities. The calculated CO2 production is averaged from the output in the 45 communities.

### <span id="_Toc371140105" class="anchor"><span id="_Toc371140232" class="anchor"></span></span>5.3.3 Rating Point Calculation

Using the standardized occupancy conditions AKWarm again calculates energy use, and compares this to the reference and and best case homes. The resultant star rating associated with the points and any warning messages (see below) are stored for printing on the certificate.

The points are calculated by adding a positive or negative point adjustment to the assigned score (85) of a comparable reference home. The point adjustment is determined by multiplying the maximum point improvement possible (15) by the ratio of the difference between the reference house energy consumption and the rated house energy consumption divided by the difference between the reference house energy consumption and the best house energy consumption

Rating Points = Reference house energy use \* (100- Reference house points)/ (Reference energy use - Best house energy use) + Reference house points

### <span id="_Toc371140106" class="anchor"><span id="_Toc371140233" class="anchor"></span></span>5.3.4 Rating Star Levels

The number of stars associated with the energy rating is based on star point levels set in the Energy Library. A “plus” rating is signified by returning an extra half star; e.g. 3 stars returns 3, 3 stars plus returns 3.5.

### <span id="_Toc371140107" class="anchor"><span id="_Toc371140234" class="anchor"></span></span>5.3.5 Messages Printed on Rating Certificate

**BEES Compliance **

The AKWarm rating certificate indicates whether a home that is being tested for BEES compliance meets or fails the Standard. The program checks the following criteria:

1.  Pa Air change rate must be less than 7

2.  House must have enough points to make a 4 Star Plus Rating

**Ventilation Message**

The energy rating does not include a test of proper ventilation, even though BEES compliance does require adequate ventilation. If the measured airtightness rate is less than .5 ach, even though it does not affect the rating points, it triggers a warning message that is printed on the rating:

“The measured air tightness of this home indicates that it may not provide sufficient ventilation air for acceptable indoor air quality as defined by ASHRAE 62-89, without adequate mechanical ventilation. Equipment. If whole house mechanical ventilation has been installed, it is recommended that it be properly maintained and operated. If no whole house mechanical ventilation equipment has been installed, it is strongly recommended that the homeowner consider aninvestment in this improvement. (A test of the building’s ventilation air rate would help determine the importance of a mechanical ventilation system in this home.)”

### 5.3.6 Rating Calibration Parameters (as defined in Energy Library, and in use 3/98)

The following parameters are determined independently of AKWarm’s internal coding. They are listed in the ACCESS Energy Library Database that is attached to the AKWarm file. These parameters may be modified without affecting AKWarm’s energy use calculations, and only affect the rating calculations.

BEES Point Level = 83 Reference House Points = 85

Ratio of Best (100 point) Energy Use to BEES Energy Use: Space Heating: 0.2 Domestic Hot Water: 0.6

##### Site-to-Source BTU Multipliers

|---------------|------------|
| Fuel          | Multiplier |
| Electricity   | 3          |
| Natural Gas   | 1          |
| Propane       | 1          |
| \#1 Oil       | 1          |
| \#2 Oil       | 1          |
| Birch         | 0.8        |
| Spruce        | 0.8        |
| Coal          | 1          |
| Special Hydro | 1.5        |

##### Star Point Boundaries

|----------------------|--------|
| Star Level           | Points |
| 1 Star to 1 Star +   | 40     |
| 1 Star + to 2 Stars  | 50     |
| 2 Star to 2 Star +   | 60     |
| 2 Star + to 3 Star   | 68     |
| 3 Star to 3 Star +   | 73     |
| 3 Star + to 4 Star   | 78     |
| 4 Star + to 4 Star + | 83     |
| 4 Star + to 5 Star   | 88     |
| 5 Star to 5 Star +   | 92     |

<span id="GlossaryHeading" class="anchor"><span id="_Toc371140108" class="anchor"><span id="_Toc371140235" class="anchor"><span id="_Toc371146354" class="anchor"></span></span></span></span>Chapter 6 
========================================================================================================================================================================================================

 AKWarm Home Improvement Reports
================================

<span id="_Toc371140109" class="anchor"><span id="_Toc371140236" class="anchor"><span id="_Toc371146356" class="anchor"></span></span></span>6.1 Introduction
-------------------------------------------------------------------------------------------------------------------------------------------------------------

AKWarm can generate an Improvement Options Report describing a few ways the homeowner can improve the energy efficiency of the home, save money on utility bills, and improve the energy rating. Information from a user-selected list of recommendations is used to analysize the efficiency of various improvements and create a benefit-to-cost ratio for each improvement.

### <span id="_Toc371140110" class="anchor"><span id="_Toc371140237" class="anchor"></span></span>6.1.1 Improvement Measure Categories

For each shell component or energy feature, AKWarm offers an array of relevant improvement options. The user selects the most relevant option for AKWarm to evaluate. In the Energy Library, each improvement option is associated with a set of improvement levels (currently supports up to ten levels), based on R-value, type of insulation, , option to add to existing insulation or replace existing insulation, shading coefficient (for windows), installed cost of the level, life of the measure in years, and present value of maintenance cost for the level. For each option the user is able to adjust the library cost or specify do-it-yourself cost only.

1.  Shell component measures

2.  Space Heater Replacement

3.  Space Heater Improvements

4.  Domestic Water Heater Replacement

5.  Air Tightening

6.  Setback Thermostat

### <span id="D2H_HelpMarking" class="anchor"><span id="_Toc371140111" class="anchor"><span id="_Toc371140238" class="anchor"></span></span></span>6.1.2 Improvement Calculations

For each improvement option selected by the user, AKWarm will cycle through every level of improvement by replacing the existing information with the new information, and determine the following information.

1.  Annual energy cost savings from the measure

2.  Present Value of energy cost savings

3.  Benefit to Cost Ration for improvement

4.  Home’s total energy cost after the measure is implemented

5.  Home’s total energy rating points after the measure is implemented

6.  Home’s total space heating cost after implementation of measure

7.  Home’s total fuel cost by fuel type after implementation of the measure

8.  Home’s total CO2 production after implementation of this measure

AKWarm will then rank the improvements based on their efficiency, and finally, for each improvement will show the benefit to cost ratio for implementing that measure *after* implementing the more cost effective improvements. The output report is a package, including the cost effective improvements, in order of cost-effectiveness, and then the list of improvement measures the user selected that proved not to be cost effective. Again, the ratios and savings are based on implementation of that measure after the previous measures were implemented. If the user chooses to deselect a measure that was at the top of the list, the following measures would be re-evaluated for cost-effectiveness based on no improvement in that area.

At the present time, AKWarm is not equipped to evaluate the cost-effectiveness of changing fuel types for heating systems through the improvement options analysis. The user can achieve this analysis by running two separate calculations for the home, and noting the difference in cost, or by creating a separate file for the same home and changing the heating system type, and observing the different reports.
