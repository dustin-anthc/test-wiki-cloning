# Evaluating Energy Efficiency Improvements in AKWarm.

<a name="improvement-introduction"></a>
## Introduction

AKWarm can generate an Improvement Options Report describing a few ways the homeowner can improve the energy efficiency of the home, save money on utility bills, and improve the energy rating. Information from a user-selected list of recommendations is used to analyze the efficiency of various improvements and create a benefit-to-cost ratio for each improvement.

<a name="improvement-categories"></a>
## Improvement Measure Categories

For each shell component or energy feature, AKWarm offers an array of relevant improvement options. The user selects the most relevant option for AKWarm to evaluate. In the Energy Library, each improvement option is associated with a set of improvement levels based on R-value, type of insulation, option to add to existing insulation or replace existing insulation, shading coefficient (for windows), installed cost of the level, life of the measure in years, and present value of maintenance cost for the level. For each option the user is able to adjust the library cost or specify do-it-yourself cost only.  There are six general categories of improvement measures:

1.  Shell component measures

2.  Space Heater Replacement

3.  Space Heater Improvements

4.  Domestic Water Heater Replacement

5.  Air Tightening

6.  Setback Thermostat

<a name="improvement-calculations"></a>
## Improvement Calculations

For each improvement option selected by the user, AKWarm will cycle through every level of improvement by replacing the existing information with the new information, and determine the following information.

1.  Annual energy cost savings from the measure

2.  Present Value of energy cost savings

3.  Benefit-to-Cost Ratio for improvement

4.  Home’s total energy cost after the measure is implemented

5.  Home’s total energy rating points after the measure is implemented

6.  Home’s total space heating cost after implementation of measure

7.  Home’s total fuel cost by fuel type after implementation of the measure

8.  Home’s total CO2 production after implementation of this measure

AKWarm will then rank the improvements based on their cost-effectiveness and will show the benefit-to-cost ratio for implementing each measure *after* implementing the more cost effective improvements. The output report is a package including the cost effective improvements in order of cost-effectiveness and then the list of improvement measures the user selected that proved not to be cost effective. Again, the ratios and savings are based on implementation of that measure after the previous measures were implemented. If the user chooses to deselect a measure that was at the top of the list, all of the following measures would be re-evaluated for cost-effectiveness based on no improvement in that area.

At the present time, AKWarm is not equipped to evaluate the cost-effectiveness of changing fuel types for heating systems through the improvement options analysis. The user can achieve this analysis by running two separate calculations for the home, and noting the difference in cost, or by creating a separate file for the same home and changing the heating system type, and comparing the different reports.

#### Benefit-to-Cost Ratio Calculation

A benefit-to-cost ratio is calculated to determine the relative cost-effectiveness of all proposed energy efficiency measures. The numerator of the benefit-to-cost ratio is the net present value of the energy savings over the expected life of the energy efficiency measure, including the  fuel escalation factor and the Real Discount Rate published by the U.S. Department of Energy. Note that the real discount rate already includes an adjustment for the general price inflation. The denominator is the estimated installation cost of the energy efficiency measure taken from the [improvement cost library]((../wiki/Images/Appendices/AppendixC.xlsx)

The formula for this calculation can be represented as: 

[[..wiki/Images/BCR-equation.gif]]

*Where*

> *BCR = Benefit-to-Cost Ratio*
>
> *CS<sub>t</sub> = Energy cost savings at year t including fuel escalation factors*
>
> *N = Estimated life of the improvement in years*
>
> *d = Discount rate*
>
> *I<sub>t</sub> = Investment costs in year t*


## Improvement Libraries

The benefit-to-cost ratios of energy efficiency improvements are calculated using several different collections of data that are stored in AKWarm libraries.  There are libraries for the estimated life of an energy efficiency improvement, for fuel/utility costs, for projected energy escalation over time, and for the estimated cost to install each energy efficiency improvement.  These libraries are updated periodically.

#### Fuel Cost Library

The Alaska-specific [fuel cost library](../wiki/Images/Appendices/AppendixB.xlsx) is used for estimating energy cost savings for energy efficiency measures. These costs are updated biannually and are derived from the Alaska Department of Commerce, Community, and Economic Development’s *Alaska Fuel Price Report: Current Community Conditions*, the Alaska Energy Authority’s *Power Cost Equalization Program: Statistical Data by Community* and other published utility rates in Alaska. Fuel prices for electricity include estimated demand charges and differentiate between subsidized Power Cost Equalization (PCE) prices and unsubsidized prices depending on whether estimated monthly usage exceeds the PCE program's monthly 500 kWh limit. Additionally, the Regulatory Commission of Alaska’s surcharge for both electricity and natural gas is factored in to all energy cost estimates.

#### Energy Efficiency Improvements Cost Library

The Alaska-specific [improvement cost library]((../wiki/Images/Appendices/AppendixC.xlsx) is used when evaluating the cost-effectiveness of recommended energy efficiency measures.

This library gives a range of costs for a wide variety of specific energy efficiency measures. These costs include all materials, labor, and equipment for each measure. Within Alaska, installation costs for energy efficiency measures vary widely due to transportation requirements, availability of skilled labor, and other market forces. For this reason, each community has been assigned a relative cost factor, which can be found in the [Community Cost Factors Library](../wiki/Images/Appendices/AppendixD.xlsx)

The improvement cost library was created using bid costs from Weatherization Agencies working throughout the state as well as information from various Alaskan suppliers and installers.  It is updated periodically.  

#### Estimated Life of Energy Efficiency Measures

The expected life of an energy efficiency measure will affect the life cycle cost-benefit analysis calculations. AKWarm uses the estimated life expectancy figures in the [improvement cost library]((../wiki/Images/Appendices/AppendixC.xlsx) for each energy efficiency measure when calculating life cycle costs.  The estimated lives in this section are derived from generally accepted engineering estimates from ASHRAE. 

#### Fuel Escalation Factors

Fuel escalation factors are used when calculating the cost-effectiveness of energy efficiency measures. These factors are taken from the most recent version of the [National Institute of Standards and Technology’s](www.nist.gov) *Energy Price Indices and Discount Factors for Life-Cycle Cost Analysis: Table Ca-4*. The 2013 version of these numbers for Census Region 4 are located in the [Fuel Escalation Factor section](../wiki/Images/Appendices/AppendixE.xlsx).  Note that these factors are *not* based on a constant annual percentage growth.

## Improvement Options Report

The AKWarm Improvement Options Report that is available after hitting "Calculate" contains a cost evaluation of major improvements. Major improvements pertain to the more expensive improvements, such as adding insulation to an attic or replacing a heating system. Low cost recommendations are provided on a separate checklist. Low cost measures range in cost from requiring no materials and little time to install to improvements that may cost a few hundred dollars.

The improvement options report is generated after AKWarm analyzes possible energy efficiency improvements. It analyzes each improvement by “applying” the improvement to the building (i.e. modifying the home description to reflect installation of the improvement), and then re-calculating the energy use of the building to determine the energy saved. Because interaction between energy efficiency improvements is accounted for, many energy calculations are initiated by this module. All remaining measures are re-analyzed. This process continues until all recommended measures have been applied to the building.

The improvement options that were evaluated and determined to be cost effective are listed at the top of the page. These are measures that show a savings to cost ratio of 1 or more. This table includes a description of the improvement measure and the location for which it is recommended, as well as an estimate of the average cost of installation, the annual savings, and the rating points gained from installation.
