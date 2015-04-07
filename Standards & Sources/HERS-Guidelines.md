-   [Introduction](#intro)
-   [National Software Accuracy Testing](#national_testing)
-   [Alaska Program Consistency Testing](#consistency)
    -   [Alaska Home Energy Rating Score](#rating-score)
    -   [Mandatory Modeling Inputs](#modeling-inputs)
    -   [Alaska Testing Protocol](#testing-protocol)
-   [Required Reporting](#reporting)
-   [Definitions](#definitions)
-   [[Appendix A: Sample Alaska Home Energy Rating Calculation|Rating_Calculation#sample_calc]]
-   Appendix B: Alaska-specific utility and fuel prices
-   Appendix C: Improvement Life and Cost Library
-   Appendix D: Community Cost Factors
-   Appendix E: Fuel Escalation Factors
-   [[Appendix F: Alaska Test Home Inputs|Alaska-Test-Home-Inputs]]
-   [[Appendix G: Sample Energy Rating Certificate|../Images/Appendices/AppendixG.pdf]]
-   [[Appendix H: Sample Improvement Options Report|../Images/Appendices/AppendixH.pdf]]
-   [[Appendix I: Additional Considered Standards and Requirements|AppendixI]]
-   [[Appendix J: Forms Needed for Software Certification|AppendixJ]]


<a name="intro"></a>
Introduction 
============

Overview
--------

The Alaska Housing Finance Corporation (AHFC) uses AKWarm energy rating software as the basis for its Home Energy Rebate Program, to verify compliance with the Building Energy Efficiency Standard (BEES) and project tracking for the Weatherization Assistance Program. Currently AKWarm is the only software certified for use in these programs. Passage of House Bill 297 in 2014 makes AHFC the authorizing agency to certify home energy rating software for the state. This document outlines the procedures for certifying new home energy rating software in Alaska.

Intent
------

The intent of these guidelines is to establish the consistency across modeling software applications that is necessary to ensure that Alaska programs continue to be based on proven cost-effectiveness, consistent energy modeling, and efficient allocation of resources.

General Approach
----------------

In order to ensure that any new modeling software provides accurate and consistent results, CCHRC recommends that a proposed new home energy rating software application go through the following certification process:

1.  **National Testing:** Proposed software shall provide documentation showing that the software has met the heating load simulation testing required by ANSI/ASHRAE Standard 140-2011 as amended and accepted by AHFC. This ensures that the software provides reasonably accurate heating load calculations.

2.  **Alaska Program Consistency Testing:** Using the *mandatory modeling inputs* and *Alaska Home Energy Rating Score* calculation procedures outlined in section 3 of this document, proposed new home energy rating software applications shall model a series of Alaska-specific test homes detailed in section 3.5. The energy and cost results from these test homes shall fall within the range of accuracy specified in this document.

3.  **Reporting Requirements:** For final approval, software applications shall include a method to automatically generate reports proving that the Alaska-specific mandatory inputs, *reference homes*, and energy rating system calculation procedures are either built in to the software or are appropriately entered by end users. Additionally, an energy rating certificate meeting AHFC’s standards shall be produced at the conclusion of any energy rating performed. When evaluating a retrofit energy model, an Improvement Options Report shall be generated in accordance with the guidelines in section 4.3. Lastly, a standardized, HPXML-based energy model file must be provided with each rating to ensure proper data tracking.[1]

While Alaska-specific needs are the focus of this document, many of the requirements in this document are partially based on three national standards: *ANSI/ASHRAE 140-2011: Standard Method of Test for the Evaluation of Building Energy Analysis Computer Programs*, the *2015 International Energy Conservation Code*, and RESNET's *Mortgage Industry National Home Energy Rating Standards*.

<a name="national_testing"></a>
National Software Accuracy Testing
==================================

Building Heating Load Simulation Testing
----------------------------------------

In order to ensure that the software applications seeking certification in Alaska provide an acceptably high level of energy modeling accuracy, they must meet the requirements of selected nationally standardized tests. These tests are designed to verify consistency in building load simulations for residential energy rating software. Specifications and instructions for these tests are found in ANSI/ASHRAE Standard 140-2011. The ANSI/ASHRAE Standard 140, Class II, Tier 1 test procedure for heating loads *only* has been adopted and is a requirement for all energy modeling software applications to be certified in Alaska. Since cooling equipment is uncommon in residential housing in Alaska, the cooling testing specifications in ANSI/ASHRAE Standard 140, Class II, Tier 1 are not a requirement for software certification.

The acceptance criteria for these tests are developed in accordance with Annex 22 of ANSI/ASHRAE Standard 140-2011 and are provided in Table 1 and Table 2.

Table 1 shows the maximum and minimum allowable annual heating loads in millions of BTUs for the test homes defined in ASHRAE Standard 140. Parties seeking software certification in Alaska shall model the energy use of these test homes and shall be advanced in the certification process only if the modeled energy use falls within the ranges indicated.

<span id="_Ref403475510" class="anchor"></span>Table 1: Heating Load Ranges from ASHRAE 140

| **Test Home Case** | **Range Max** | **Range Min** |
|--------------------|---------------|---------------|
| L100AC             | 79.48         | 48.75         |
| L110AC             | 103.99        | 71.88         |
| L120AC             | 64.30         | 37.82         |
| L130AC             | 53.98         | 41.82         |
| L140AC             | 56.48         | 43.24         |
| L150AC             | 71.33         | 40.95         |
| L155AC             | 74.18         | 43.53         |
| L160AC             | 81.00         | 48.78         |
| L170AC             | 92.40         | 61.03         |
| L200AC             | 185.87        | 106.41        |
| L202AC             | 190.05        | 111.32        |
| L302XC             | 90.52         | 52.66         |
| L304XC             | 75.32         | 43.91         |
| L322XC             | 118.20        | 68.35         |
| L324XC             | 80.04         | 44.01         |

<span id="_Ref403475520" class="anchor"></span>

Table 2 shows the change in annual heating loads in millions of BTUs from one ASHRAE 140 test home to another. For software to be certified for use in Alaska, these test homes shall be modeled and the difference in annual energy use shall fall within the ranges indicated.

<span id="_Ref405287502" class="anchor"></span>Table 2: Heating Load Delta Ranges from ASHRAE 140

| **Test Home Case** | **Range Max** | **Range Min** |
|--------------------|---------------|---------------|
| L110AC-L100AC      | 28.12         | 19.37         |
| L120AC-L100AC      | -7.67         | -18.57        |
| L130AC-L100AC      | -5.97         | -27.50        |
| L140AC-L100AC      | -4.56         | -24.42        |
| L150AC-L100AC      | -3.02         | -12.53        |
| L155AC-L150AC      | 6.88          | -1.54         |
| L160AC-L100AC      | 5.10          | -3.72         |
| L170AC-L100AC      | 17.64         | 7.12          |
| L200AC-L100AC      | 107.66        | 56.39         |
| L202AC-L200AC      | 9.94          | -0.51         |
| L302XC-L100AC      | 14.50         | -3.30         |
| L302XC-L304XC      | 17.75         | 5.66          |
| L322XC-L100AC      | 39.29         | 15.71         |
| L322XC-L324XC      | 38.27         | 20.21         |

<a name="consistency"></a>
Alaska Program Consistency Testing
==================================

Overview
--------

<span id="_Toc413068876" class="anchor"></span>Since 2008, more than 75,000 home energy ratings have been performed on unique locations in Alaska for AHFC programs. These ratings have been performed using the rating calculation procedures found in AKWarm energy modeling software. Builders, raters, homeowners, and the energy efficiency community have become familiar with the ratings and the star system. In order to maintain consistency in AHFC's programs, all applicant software applications shall use the Alaska Home Energy Rating Calculation procedures outlined in Section 3.2 "Alaska Home Energy Rating Score".

AHFC’s BEES and New Home Rebate Program are based on homes being modeled in AKWarm to meet thresholds for specific percentages of energy reduction relative to a *reference home*. Over 25,000 homes have been certified to meet BEES using AKWarm since the program’s inception and approximately 2,600 homes have received between $7,000 and $10,000 from the New Home Rebate program in the last six years alone. Builders throughout Alaska are familiar with the ratings produced by the AKWarm modeling software. The mandatory inputs and procedures in section 3.3.1 on "Inputs for Modeling Energy Usage" are designed to ensure that modeling results fall within a reasonable range so that both these AHFC programs for new homes will remain consistent over time.

Of the over 75,000 locations to receive ratings, more than 35,000 were energy efficiency retrofits that have been undertaken as a part of either AHFC’s Home Energy Rebate or Weatherization Assistance Programs[2]. Energy auditors in these programs have evaluated energy efficiency measures (EEMs) using the AKWarm Residential energy modeling software and have recommended or performed cost-effective measures based on the model outputs. In order to ensure consistency within these programs and to make sure that modeling inputs are Alaska-specific, energy rating software applications shall use the cost libraries and calculation procedures outlined in section 3.3.2 on "Inputs for Modeling Cost-Effectiveness." The economic calculations used by these programs are necessary to ensure that work being done is truly cost-effective. Standardizing the inputs for these calculations is necessary to prevent creating a situation in which energy raters and other software users can influence program outcomes by switching software applications to yield the greatest results.

<a name="rating-score"></a>
Alaska Home Energy Rating Score 
--------------------------------

### *Standard Operating Characteristics*

The Home Energy Rating is intended to rate the efficiency of the home and not the occupants. Therefore a number of energy-affecting characteristics controlled by the home occupants are set to standard values before performing the various energy calculations associated with the rating Additionally, a number of other values are standardized to remove their effects from the rating process due to rating policy concerns. The occupancy and policy items that are standardized are:

1.  The **Number of Occupants** in the home shall be set to a value equal to:

		N = 2.29 + 0.000411 * La

> *Where:*
>
> N = Number of occupants
>
> La = Living space floor area, not counting garage
>
> Note 1: If a multi-family building is being rated in its entirety, the Living Area in the above calculation is the living area per unit and the calculated occupants are per living unit as well.
>
> Note 2: The calculated *number of occupants* field affects the internal gains in the building and the number of gallons of domestic hot water consumed.

1.  The **Space Heating Thermostat Setpoint** is set to 70 degrees F.

2.  The **Wind Shielding** shall be set to Terrain Class 3 and Shielding Class 3 from the Lawrence Berkeley Laboratory Infiltration model[3] in order to remove site-specific differences from the rating process.

3.  The **Lights and Miscellaneous Appliances** energy usage, exclusive of the cooking range and clothes dryer, shall be set to a continuous level of 317 Watts + 0.182 Watts per square foot of living space floor area. The internal gains shall be set to 95% of this calculated value.

4.  A **Cooking Range and Dryer** are included in the home and assumed to use Electricity as the energy source. The internal gains of the clothes dryer shall be set to 37 Watts continuously, and the cooking range shall produce internal gains of 70 Watts continuously.

5.  Because of variations in how frequently occupants might use a secondary heating system such as a wood stove, the **Secondary Heating System** shall be removed from the modeled home, and all heat shall be assumed to come from the Primary Heating System *for the purposes of the rating score only*.

6.  All shell components exposed to **Garage Temperature** shall be changed to Living Space temperature shell components for the purposes of energy calculations related to the rating score only. Doing so causes all garage components to be as important as Living Space components in the rating process.

Note that these standard operating characteristics are only necessary for calculating the Alaska Home Energy Rating Score. Software applications shall also output estimated energy cost, usage, and other outputs for the model using the non-standardized, user-entered inputs.

### *Reference Homes*

A *reference home* is a home with the same amount of gross wall area, ceiling area, floor area, and volume as the actual home but with a specified reference efficiency level for its shell components (represented as a composite U-value) and a specified efficiency and fuel type for the space and water heating equipment. The source energy use of the *reference home* corresponds to a particular point level on the Energy Rating scale. Currently, the *reference home* point level is 85 points. Note that the efficiency level of the *reference home* varies across rating regions within the state. Software applications shall be able to generate these *reference homes* using only the inputs for the rated design and the u-values and equipment efficiencies outlined in this section. The calculation procedure shall restrict the end user from directly modifying the building component characteristics of the *reference home*.

### *Shell Components and Air Change Rates*

To simplify the rating process, all windows, and doors in the *reference home* are combined with the wall to create a composite U-value. The same is done for the ceiling, including any skylights, which are combined to create a composite ceiling U-value. This reduces the number of efficiency characteristics that need to be specified for the *reference home*. The *reference home* wall U-value is a composite U-value used to compare against the composite U-value of the actual home.

All floor components in the *reference home* are converted to above-grade floor components. If the *actual* home has below-grade floor components, the modeling process will give those components credit for the insulating value of the ground, with an assumed soil conductivity of 0.8 BTU/hr-ft-°F. Below-grade walls are also converted to above-grade walls when the *reference home* is created.

After these conversions are made, *reference home* U-values are assigned to the shell components and a *reference home* 50 Pascal air change rate is assigned. These U-values and air change rates vary by Rating Region, although some regions use the same U-values and air exchange rates. Table 3 shows the *reference home* shell and air change values.

<span id="_Ref403475538" class="anchor"></span>Table 3: Alaska Reference Home U-Values

| **Region**                        | **Floor U-Value** | **Wall U-Value** | **Ceiling U-Value** | **50 Pa Air Change Rate** |
|-----------------------------------|-------------------|------------------|---------------------|---------------------------|
| Southeast                         | 0.0276            | 0.0858           | 0.0247              | 4.0                       |
| South Central, Kodiak & Aleutians | 0.0276            | 0.0858           | 0.0247              | 4.0                       |
| Bristol Bay                       | 0.0246            | 0.0753           | 0.0247              | 4.0                       |
| Interior & Yukon/Kuskokwim Delta  | 0.0246            | 0.0753           | 0.0247              | 4.0                       |
| Northwest Coastal                 | 0.0246            | 0.0656           | 0.0247              | 3.0                       |
| Arctic Slope                      | 0.0224            | 0.0658           | 0.0184              | 3.0                       |

The *reference home* shall be assumed to have a **Mechanical Ventilation** system without any heat recovery. This system shall have a flow rate sufficient to provide any additional outside air necessary beyond air leakage so that the combined flow rate is 0.25 ACH. This system shall have a power consumption level of 0.61 watts/cfm.

### *Space Heating and Water Heating Equipment*

Space and water heating efficiency and fuel type characteristics also need to be specified for the *reference home*. The heating fuel type for all regions shall be assumed to be \#1 Fuel Oil, except the South Central, Kodiak & Aleutians region which shall be specified as Natural Gas, and the Southeast region which shall be specified to be \#2 Fuel Oil.

The *reference home* shall be assumed to have a **space heating system** with an *80% AFUE* and a **space heating distribution system** with *100% efficiency* located within the thermal boundary. All *reference homes* shall have a **Setback Thermostat** controlling the *entire home*. Software shall also model and include the auxiliary electric use of the heating system in the space heating fuel usage. This electric use is necessary to power fans, pumps, and control devices. For regions using Fuel Oil as the *reference home* fuel type, the BTUs of auxiliary electricity use shall be assumed to be 4.9% of the BTUs of Fuel Oil use. For the region using Natural Gas, the auxiliary electricity use shall be assumed to be 4.4% of the Natural Gas use. These auxiliary usage values are typical for forced-air space heating systems.

For water heating the *reference home* is assumed to have a tank-type water heater located in semi-conditioned space with *no* insulating blanket and having an **Energy Factor of 0.6**. For the region with the Natural Gas fuel type, that water heater is assumed to have R-8 tank insulation and a recovery efficiency of 80%, typical for natural gas water heaters. For the Fuel Oil regions, the tank R-value is assumed to be R-12 and the recovery efficiency is 78%.

### *Rating Calculation*

**Step 1: Determine the Source Space Heating and Water Heating Energy Use of the Home,** using the standard operating characteristics described in this document. Home energy modeling software shall be used to estimate these energy use values, calculating energy use of the whole building as a single zone. Because multiple fuel types may be used to provide the space and water heat, the energy uses of these different fuel types are combined using *Source Energy* weighting factors to determine a total source energy use. These source energy factors are predominantly used to account for the conversion, transmission and distribution energy losses that occur when delivering energy to a building. Some types of energy, such as electricity, incur large losses so have large source-to-site weighting factors.

**Step 2: Create a Reference Home and Determine its Source Energy Use.** Create a *reference home* using the dimensions from the actual home and the u-values and equipment efficiencies outlined in this document. The source energy use of the *reference home* corresponds to a particular point level on the Energy Rating scale. Currently *reference home* point level is 85 points. Note that the efficiency level of the *reference home* varies across rating regions within the state.[4]


**Step 3: Determine the Source Energy use of the Home scoring 100 points on the Rating Scale**. The *Reference Home* determines one point on the Source Energy versus Rating Point linear relationship. A second point in that linear relationship is established by specifying the energy use of a 100 point home. The 100 point home is assumed to have 20% of the space heating energy use of the *reference home* (80% reduction in energy use) and 60% of the domestic water heating energy use of the *reference home*. Mathematically:

E<sub>100</sub> = E<sub>SH</sub> * 0.2 + E<sub>DHW</sub>  * 0.6

>*Where:*
>
>E<sub>100</sub> = The source energy use of the 100 point home
>
>E<sub>SH</sub> = The source space heating energy use of the reference home
>
>E<sub>DHW</sub> = The source domestic hot water energy use of the reference home

The 100 point home has 80% less space heating energy use and 40% less water heating use. A lower reduction in water heating use is chosen because it is more difficult and costly to reduce water heating energy use to very low levels.

**Step 4: Determine the Rating Point Score for the Actual Home** by linearly interpolating or linearly extrapolating from the two points described above--the *reference home* point and the 100 rating point Home point. This process will become clearer by the example presented in Appendix A.

**Step 5: Determine the Rating Star Score for the Home.** There are fixed point ranges for each Rating Star level shown in Table 4. It is simply a matter of determining which point range encompasses the actual Rating Point score for the home to determine what the associated Rating Star level is.

<span id="_Ref403486757" class="anchor"><span id="_Ref403486747" class="anchor"></span></span>Table 4: Rating Star Levels

| **Point Range** | **Rating Star Step Level** |
|-----------------|----------------------------|
| 0 ≤ x \< 40     | 1 Star                     |
| 40 ≤ x \< 50    | 1 Star Plus                |
| 50 ≤ x \< 60    | 2 Star                     |
| 60 ≤ x \< 68    | 2 Star Plus                |
| 68 ≤ x \< 73    | 3 Star                     |
| 73 ≤ x \< 78    | 3 Star Plus                |
| 78 ≤ x \< 83    | 4 Star                     |
| 83 ≤ x \< 89    | 4 Star Plus                |
| 89 ≤ x \< 92    | 5 Star                     |
| 92 ≤ x \< 95    | 5 Star Plus                |
| ≥ 95            | 6 Star                     |

<a name="modeling-inputs"></a>
Mandatory Modeling Inputs
-------------------------

### *Inputs for Modeling Energy Usage*

#### Climate Data

Alaska is a geographically large state with a wide range of climates, including many that lie outside the range of most areas in the continental U.S. For example, the average annual Base 65 heating degree days for areas in Alaska varies between approximately 7,000 and 20,000, whereas cities in the continental US considered to be in “very cold climates” such as Minneapolis, MN, Burlington, VT, and Denver, CO all have less than 8,000 annual heating degree days.

In order to ensure that climate differences throughout Alaska are appropriately modeled, energy modeling software must use at least 12 distinct climate categories to represent different locations. These categories shall be appropriately spaced such that each individual area category has a range of less than 1,200 heating degree days. It is also recommended that areas with similar solar gains and wind speeds be grouped together.

Software shall also use climate data that has been derived from at least a 10-year period to account for annual variations. Pre-approved sources of climate data include TMY3 data and NOAA 30-year climate averages.[5]

#### Default Modeling Inputs

Estimated energy use for domestic hot water is a significant factor in the Alaska Home Energy Rating Score calculation formula. Thus for consistency in ratings it is important to use the same estimates for average water use per person. For rating calculation purposes, modeling software shall use the default of 15.2 gallons of hot water per person, per day, where the number of occupants is standardized using the following formula:

		N = 2.29 + 0.000411 * La

> *Where:*
>
> N = Number of occupants
>
> La = Living space floor area, not counting garage
> not counting garage


Energy modeling software shall calculate the energy savings from a programmable thermostat with the following two requirements when estimating the energy benefits: the temperature shall be set back for 8 hours per day, and a 50% multiplier shall be used to account for the likelihood that it will not be properly programmed.

#### Minimum Equipment Efficiencies

Start Research comparing actual fuel usage and modeled values has pointed to the possibility that low default heating equipment efficiency in modeling software leads to over-prediction of energy use.[6] To mitigate this possible error, software programs shall have default equipment efficiencies at or above the minimum values in Table 5. Note that it is allowable for users to override these efficiencies *if* there is an equipment label or measured steady state efficiency lower than this minimum.

<span id="_Ref411603670" class="anchor"></span>**Table 5: Minimum Default Equipment Efficiencies**

| **Equipment Type**                 | **Minimum Value** |
|------------------------------------|-------------------|
| Forced-air furnace, AFUE           | 72%               |
| Hot water / steam boiler, AFUE     | 60%               |
| Heat Pump, HSPF                    | 6.5               |
| Heat Pump, SEER                    | 9.0               |
| Gas-fired storage water heater, EF | 0.50              |
| Oil-fired storage water heater, EF | 0.45              |
| Electric storage water heater, EF  | 0.86              |

#### Source-to-Site Energy Multipliers

The multipliers in Table 5 shall be used when modeling energy use in Alaska.

<span id="_Ref403475581" class="anchor"></span>Table 6: Source-to-Site Multipliers by Fuel Type

| **Fuel Type**             | **Source-to-Site Multiplier** |
|---------------------------|-------------------------------|
| Electricity               | 3.0                           |
| Special Hydro Electricity | 1.5                           |
| Natural Gas               | 1.0                           |
| \#1 Fuel Oil              | 1.0                           |
| \#2 Fuel Oil              | 1.0                           |
| Propane                   | 1.0                           |
| Spruce                    | 0.8                           |
| Birch                     | 0.8                           |
| Coal                      | 1.0                           |
| District Steam Heat       | 1.0                           |
| District Hot Water Heat   | 1.0                           |

The Special Hydro Electricity multiplier shall be used in the following communities where electricity from hydroelectric dams provide the primary space heating: Craig, Douglas, Haines, Juneau, Kasaan, Ketchikan, Klawock, Kodiak, Larsen Bay, Metlakatla, Petersburg, Sitka, Skagway, Thorne Bay, Ward Cove, and Wrangell. These communities rely primarily on hydroelectric power, but many use diesel powered generators for peak loads. Wood multipliers are less than 1.0 to reflect the fact that in Alaska they represent a significant renewable resource.

### *Inputs for Modeling Cost-Effectiveness*

#### Fuel Costs

The Alaska-specific fuel costs found in Appendix B shall be used for the purposes of estimating energy cost savings for EEMs. These costs are updated biannually and are derived from the Alaska Department of Commerce, Community, and Economic Development’s *Alaska Fuel Price Report: Current Community Conditions*, the Alaska Energy Authority’s *Power Cost Equalization Program: Statistical Data by Community* and other published utility rates in Alaska. Fuel prices for electricity shall include estimated demand charges and shall differentiate between subsidized Power Cost Equalization (PCE) prices and unsubsidized prices depending on whether estimated monthly usage exceeds the PCE program's monthly 500 kWh limit. Additionally, the Regulatory Commission of Alaska’s surcharge for both electricity and natural gas shall be factored in to all energy cost estimates.

#### Energy Efficiency Improvements Cost Library

Modeling software shall have the capacity to use the following Alaska-specific installation costs when evaluating the cost-effectiveness of recommended energy efficiency measures.

*Appendix C: Improvement Life and Cost Library* gives a range of costs for a wide variety of specific EEMs. These costs include all materials, labor, and equipment for each measure. Within Alaska, installation costs for energy efficiency measures vary widely due to transportation requirements, availability of skilled labor, and other market forces. For this reason, each community has been assigned a relative cost factor, found in *Appendix D: Community Cost Factors*. These factors shall be used to determine the installation cost based on the tables in Appendix C.

#### Estimated Life of Energy Efficiency Measures

The expected life of an energy efficiency measure will affect the life cycle cost-benefit analysis calculations. Thus it is important that these expected life inputs be standardized to ensure consistency in ratings in Alaska. Software shall use the estimated life expectancy figures in Appendix C for each EEM when calculating life cycle costs.

#### Fuel Escalation Factors

Fuel escalation factors shall be used when calculating the cost-effectiveness of EEMs. These factors shall be taken from the most recent version of the National Institute of Standards and Technology’s *Energy Price Indices and Discount Factors for Life-Cycle Cost Analysis: Table Ca-4*[7]. The 2013 version of these numbers for Census Region 4 are located in Appendix E: Fuel Escalation Factors. Software applications seeking certification in subsequent years should refer to the National Institute of Standards and Technology’s website for updated information. Note that these factors are *not* based on a constant annual percentage growth.

#### Calculating Savings to Investment Ratios

A savings to investment ratio (SIR) shall be calculated to determine the relative cost-effectiveness of all proposed energy efficiency measures. The numerator of the SIR shall be the net present value of the energy savings over the expected life of the EEM, including the aforementioned fuel escalation factor and the Real Discount Rate published by the U.S. Department of Energy.[8] Note that the real discount rate already includes an adjustment for the general price inflation. The denominator shall be the estimated installation cost of the EEM, taken from Appendix C of this document. See section 3.4.2 for the savings to investment ratio formula. An Improvement Options Report shall be produced with each EEM ranked from those with the highest SIR to those with the lowest SIR so that users can easily determine the most cost-effective retrofits.

<a name="testing-protocol"></a>
Alaska Testing Protocol
-----------------------

While national home energy rating software modeling standards ensure that the algorithms used provide a reasonable estimate of heating loads, additional Alaska-specific testing is necessary to ensure that results remain consistent with the thousands of energy ratings that have been performed in Alaska and to document compliance with the Alaska Building Energy Efficiency Standard, which is based on the International Energy Conservation Code with Alaska-specific amendments.. This Alaska-specific testing protocol requires that software use the mandatory inputs and rating calculation procedures outlined in this document so that the results can be compared with currently certified software.

### *Testing Protocol Part 1: Evaluating Energy Ratings for BEES Certification*

Proposed modeling software shall conduct a series of comparative tests using the Alaska Test Home inputs located in Appendix F. These homes shall be modeled in the proposed software using the mandatory inputs outlined in this document and Alaska Home Energy Rating Scores shall be computed following the procedures previously detailed.

The Alaska Test Homes are located in the same five communities as the Alaska Reference Homes, representing each BEES climate zone. The component dimensions of these homes are computed from the averages for all homes in these five communities that received BEES certification between 2006 and 2012. Two sets of modeling inputs will be used for each home: one set uses the 2012 BEES prescriptive values; and one set uses regionally common insulation values, air-tightness levels, and HVAC equipment efficiencies to meet or exceed the current 6 Star minimum rating of 95 points, for a total of 10 test models. The modeling inputs for these Alaska Test Homes are detailed in Appendix F. An Alaska Home Energy Rating Score shall be calculated using the proposed software for each of these 10 models and compared with the values in Table 6. In order to be approved for use in Alaska, rating points for each individual model must fall within the ranges listed in Table 6.

<span id="_Ref403475598" class="anchor"></span>Table 6: Alaska Home Energy Rating Score Ranges

| **Community** | **AK Energy Rating Scores for 2012 BEES Prescriptive Models** | **Allowable Rating Point Range** | **AK Energy Rating Scores for 6 Star Models** | **Allowable Rating Point Range** |
|---------------|---------------------------------------------------------------|----------------------------------|-----------------------------------------------|----------------------------------|
| Anchorage     | 88.8                                                          | 87.0 - 90.6                      | 95.2                                          | 94.2 - 96.2                      |
| Barrow        | 89.9                                                          | 88.0 - 91.8                      | 95.3                                          | 94.3 - 96.3                      |
| Fairbanks     | 90.7                                                          | 89.1 - 92.3                      | 95.3                                          | 94.4 - 96.2                      |
| Juneau        | 89.2                                                          | 87.2 - 91.2                      | 95.7                                          | 94.7 - 96.7                      |
| Nome          | 89.8                                                          | 87.7 - 91.9                      | 95.5                                          | 94.4 - 96.6                      |

The point ranges were determined by first calculating the annual source energy use in millions of BTUs for each model, applying a factor of <sup>+</sup>/<sub>-</sub> 10%, and then re-calculating the Alaska Home Energy Rating Score. While 10% is a smaller allowable variance than the average range of <sup>+</sup>/<sub>-</sub> 23.6% allowed in the ASHRAE 140-2011 modeling procedure, it is necessary in order to ensure that ratings done with different software are within one Rating Step in Alaska. Additionally, because the rating calculation compares three buildings: the actual home, the *reference home* and the 100 point home, the rating score will not be affected so long as the software application consistently over- or under-estimates energy use for each of these three models.

### *Testing Protocol Part 2: Evaluating Improvements for AHFC’s Energy Efficiency Retrofit Programs*

The software applicant must perform the following series of tests. The Alaska Test Homes will have the same component dimensions as those in the Evaluating Energy Ratings for BEES Certification Tests and will be located in the same communities. The first set of models will use the 2012 BEES prescriptive values as inputs and the second set of models will use regionally common insulation values, air-tightness levels, and HVAC equipment efficiencies found in the median as-is home ratings previously conducted in Alaska[9]. Detailed inputs for these models are located in Appendix F.

These 10 models shall then be used to evaluate the estimated annual energy savings in millions of BTUs obtained by individually installing the EEMs outlined in Table 7. The energy savings for each EEM shall be calculated separately using the mandatory inputs and procedures outlined in this document. Next, the energy savings shall then be divided by the total amount of estimated site energy used by the building to create a “percentage energy saved by measure”. The percentage energy savings by measure can then be compared with the results in Table 8 and Table 9 to determine if it is within the allowable range of values. The center value of this range was obtained by modeling each EEM in AKWarm. The range itself was calculated based on the median percentage difference (<sup>+</sup>/<sub>-</sub> 56%) from the Heating Load Delta test as described in ASHRAE 140. All EEMs must be within these allowable ranges in order to be certified for use in Alaska.

Additionally, each software applicant shall complete a Savings to Investment Ratio (SIR) algorithm test for one of these modeled energy efficiency measures. This manually performed test takes the modeled annual energy cost savings of the EEM directly from the software outputs and then manually calculates the Savings to Investment Ratio using the fuel price escalation factors, improvement lives, and improvement costs from Appendices A, B and C. The savings to investment ratio will be calculated by the following formula:

[[/Images/SIR-formula.gif]]

*Where*

> *SIR = Savings-to-Investment Ratio*
>
> *CS<sub>t</sub> = Energy cost savings at year t including fuel escalation factors*
>
> *N = Estimated life of the improvement in years*
>
> *d = Discount rate*
>
> *I<sub>t</sub> = Investment costs in year t*

The software's computed SIR for this measure shall be within a <sup>+</sup>/<sub>-</sub> 5% range of the manually calculated SIR in order to be certified for use in Alaska.

<span id="_Ref403475633" class="anchor"></span>

Table 7: Energy Efficiency Measures for Evaluation

| **Number:** | **Location:**                        | **Description**                                                                                                                                                                                                                      |
|-------------|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1           | Vented Attic                         | Add R21 of blown cellulose to attic.                                                                                                                                                                                                 |
| 2           | Windows                              | Replace non-south facing windows with triple pane, argon filled windows with a u-value of 0.23 and a SHGC of 0.36                                                                                                                    |
| 3           | Heating Equipment                    | Replace heating system. For areas with natural gas, this should be a 92% AFUE forced air condensing furnace. For other areas, it should be an 87% AFUE condensing oil-fired boiler.                                                  |
| 4           | Ventilation                          | Install a Heat Recovery Ventilation system with an apparent sensible effectiveness of 70%. The system uses 1.05 Watts / cfm.                                                                                                         |
| 5           | Domestic Hot Water                   | Replace water heater with an on-demand system with an energy factor of 0.76 for fuel oil systems, 0.80 for natural gas systems, and 0.93 for electric systems The fuel type should match the fuel type of the preexisting equipment. |
| 6           | Door                                 | Replace door with one that has a u-value of 0.16                                                                                                                                                                                     |
| 7           | Above Grade Wall, House (not garage) | Add R-20 rigid foam to the exterior (siding costs are not included).                                                                                                                                                                 |

<span id="_Ref403475651" class="anchor"></span>Table 8: Percent Annual Energy Savings by Improvement Measure

| <span id="_Ref404769491" class="anchor"></span>**Test Model** | **R21 Cellulose in Attic** | **Triple Pane Window** | **92% / 87% AFUE Heating** | **HRV** | **U-0.16 door** | **R20 exterior foam** | **On demand DHW** |
|---------------------------------------------------------------|----------------------------|------------------------|----------------------------|---------|-----------------|-----------------------|-------------------|
| Anchorage - Prescriptive                                      | 3.3%                       | 1.6%                   | 7.9%                       | 3.1%    | 1.4%            | 7.3%                  | 3.2%              |
| Barrow - Prescriptive                                         | 3.6%                       | -2.7%                  | 6.9%                       | 2.1%    | 0.6%            | 6.0%                  | 4.0%              |
| Fairbanks - Prescriptive                                      | 4.1%                       | -1.1%                  | 5.2%                       | 2.6%    | 0.7%            | 4.5%                  | 2.5%              |
| Juneau - Prescriptive                                         | 2.7%                       | 1.8%                   | 3.9%                       | 2.2%    | 1.1%            | 9.0%                  | 3.5%              |
| Nome - Prescriptive                                           | 4.5%                       | -1.6%                  | 3.8%                       | 1.9%    | 0.8%            | 5.7%                  | 3.8%              |
| Anchorage - Median Retrofit                                   | 3.9%                       | 4.0%                   | 12.2%                      | 0.0%    | 1.1%            | 12.6%                 | 2.3%              |
| Barrow - Median Retrofit                                      | 6.3%                       | 4.6%                   | 8.7%                       | 0.0%    | 0.3%            | 13.0%                 | 2.5%              |
| Fairbanks - Median Retrofit                                   | 3.3%                       | 3.0%                   | 16.2%                      | 0.1%    | 0.9%            | 7.5%                  | 0.9%              |
| Juneau - Median Retrofit                                      | 3.7%                       | 5.6%                   | 3.2%                       | 0.0%    | 1.3%            | 16.4%                 | 0.0%              |
| Nome - Median Retrofit                                        | 4.3%                       | 4.8%                   | 3.9%                       | 0.0%    | 1.9%            | 10.9%                 | 2.0%              |

<span id="_Ref404769879" class="anchor"></span>Table 9: Ranges for Percent Annual Energy Savings by Improvement Measure

| **Test Model**              | **R21 Cellulose in Attic** | **Triple Pane Window** | **92% / 87% AFUE Heating** | **HRV** | **U-0.16 door** | **R20 exterior foam** | **On demand DHW** |
|-----------------------------|----------------------------|------------------------|----------------------------|---------|-----------------|-----------------------|-------------------|
|                             | Min                        | Max                    | Min                        | Max     | Min             | Max                   | Min               |
| Anchorage - BEES            | 1.4%                       | 5.1%                   | 0.7%                       | 2.5%    | 3.5%            | 12.3%                 | 1.3%              |
| Barrow - BEES               | 1.6%                       | 5.6%                   | -1.2%                      | -4.1%   | 3.0%            | 10.7%                 | 0.9%              |
| Fairbanks - BEES            | 1.8%                       | 6.3%                   | -0.5%                      | -1.8%   | 2.3%            | 8.0%                  | 1.1%              |
| Juneau - BEES               | 1.2%                       | 4.2%                   | 0.8%                       | 2.9%    | 1.7%            | 6.1%                  | 1.0%              |
| Nome - BEES                 | 2.0%                       | 7.0%                   | -0.7%                      | -2.6%   | 1.7%            | 5.9%                  | 0.8%              |
| Anchorage - Median Retrofit | 1.7%                       | 6.1%                   | 1.8%                       | 6.2%    | 5.4%            | 19.1%                 | 0.0%              |
| Barrow - Median Retrofit    | 2.8%                       | 9.8%                   | 2.0%                       | 7.2%    | 3.8%            | 13.5%                 | 0.0%              |
| Fairbanks - Median Retrofit | 1.5%                       | 5.2%                   | 1.3%                       | 4.8%    | 7.1%            | 25.2%                 | 0.1%              |
| Juneau - Median Retrofit    | 1.6%                       | 5.7%                   | 2.5%                       | 8.7%    | 1.4%            | 5.0%                  | 0.0%              |
| Nome - Median Retrofit      | 1.9%                       | 6.7%                   | 2.1%                       | 7.5%    | 1.7%            | 6.1%                  | 0.0%              |

The following table lists the total energy savings in millions of BTUs per year for each test model to assist software developers in determining the root cause of discrepancies in energy efficiency measures.

<span id="_Ref403475759" class="anchor"></span>Table 10: Annual Energy Savings by Measure in Millions of BTUs

| **Alaska Test Model**       | **R21 Cellulose in Attic** | **Triple Fane Window** | **92% / 87% AFUE Heating** | **HRV** | **U-0.16 door** | **R20 exterior foam** | **On demand DHW** |
|-----------------------------|----------------------------|------------------------|----------------------------|---------|-----------------|-----------------------|-------------------|
| Anchorage - Prescriptive    | 4.8                        | 2.4                    | 11.5                       | 4.5     | 2.1             | 10.7                  | 4.7               |
| Barrow - Prescriptive       | 3.9                        | -2.9                   | 7.5                        | 2.3     | 0.6             | 6.5                   | 4.4               |
| Fairbanks - Prescriptive    | 6.1                        | -1.7                   | 7.8                        | 3.9     | 1.1             | 6.8                   | 3.8               |
| Juneau - Prescriptive       | 2.9                        | 2.0                    | 4.2                        | 2.4     | 1.2             | 9.7                   | 3.8               |
| Nome - Prescriptive         | 4.4                        | -1.6                   | 3.7                        | 1.9     | 0.8             | 5.6                   | 3.7               |
| Anchorage - Median Retrofit | 10.2                       | 10.5                   | 32.0                       | 0.0     | 2.8             | 33.0                  | 5.9               |
| Barrow - Median Retrofit    | 12.8                       | 9.3                    | 17.6                       | 0.0     | 0.6             | 26.4                  | 5.1               |
| Fairbanks - Median Retrofit | 11.2                       | 10.2                   | 54.3                       | 0.4     | 3.1             | 25.3                  | 3.0               |
| Juneau - Median Retrofit    | 6.4                        | 9.7                    | 5.5                        | 0.0     | 2.3             | 28.5                  | 0.0               |
| Nome - Median Retrofit      | 7.1                        | 7.9                    | 6.5                        | 0.0     | 3.2             | 18.0                  | 3.3               |

<a name="reporting"></a>

Required Reporting
==================

Verification of mandatory inputs, cost-effectiveness procedures, and proper Alaska Home Energy Rating Score calculations
------------------------------------------------------------------------------------------------------------------------

To be certified for use in Alaska, home energy rating software applications shall verify that the mandatory inputs, cost-effectiveness procedures, and Alaska Home Energy Rating Score calculations are being used. There are two options for doing this:

-   Option 1: Verify that all mandatory inputs are built into the software.

    -   A copy of the software with one of the Alaska Test Models shall be sent to AHFC along with the files used to show compliance with testing. Staff will run the program and ensure that both the Alaska Home Energy Rating Score and Improvements match the testing results provided by the agency and fall within the allowable ranges without users having to enter them.

    -   The software outputs shall include a text section and AHFC logo that verifies that the library version that was used is the one that was approved for use in Alaska.[10]

<!-- -->

-   Option 2: User-entered mandatory inputs

    -   Users shall enter the mandatory inputs outlined in this document, so long as the software automatically outputs a report that details all of the required inputs that were entered. This allows AHFC staff to randomly conduct audits to ensure that the mandatory inputs are being properly entered by users.

    -   The software developer shall submit a guide for their software application highlighting which reports include the user-entered information and where all of the mandatory inputs are specifically located for AHFC to reference.


Energy Rating Certificate
-------------------------

The software shall have the capacity to provide an Energy Rating Certificate for any home audited with the program. The certificate shall be no longer than two single-sided pages or one double-sided page and at a minimum shall include the following information:

-   The Alaska Home Energy Rating Score

-   The Star Level of the home and a visual showing the division of Star Levels by the number of points

-   The estimated annual energy costs

-   A breakdown of heating costs by component type ("Wall", "Floor", "Hot Water", etc.)

-   The amount of carbon dioxide emissions produced by the home

-   General information, including the client and rater names, the rater's contact information, the date of the rating, the software name and version, the XML file name, and a section for a rater's certifying signature.

Appendix G includes a sample energy rating certificate.

Improvement Options Report 
---------------------------

When certifying audits for Alaska programs, software shall provide a printable Improvement Options Report that, at a minimum shall include the following:

-   The initial Alaska Home Energy Rating Score and the corresponding Star Level

-   The additional number of rating points necessary to reach the next 5 Star Levels

-   General information, including the address, floor area, rater information, and fuel prices used in the analysis

-   A list of the recommended improvement options with the following features:

    -   The options shall be ordered from those with the highest savings to investment ratios to those with the lowest.

    -   The improvement description and location shall be listed

    -   For each improvement, the annual savings, break-even cost, and rating points gained shall be listed

    -   The Alaska Home Energy Rating Score after all the improvements up through the current one have been implemented

    -   The expected design heat loss for the building in BTU/hr after all of the improvements up through the current one have been implemented.

-   A section with detailed descriptions of each recommended improvement and important considerations when choosing a particular upgrade.

Appendix H includes a sample improvement options report.

<a name="data-collection"></a>
Data Collection Procedures for Program Tracking and Management 
---------------------------------------------------------------

Energy ratings performed by certified energy auditors and assessors in Alaska are uploaded into the Alaska Retrofit Information System (ARIS) database after an energy audit has been completed. The ability to search ARIS and its capability to automatically generate reports allow AHFC staff to ensure that audits are being conducted properly and funds are being allocated efficiently. Having this data housed in a single location also allows for generation of data-driven reports on the programs’ effectiveness that can be shared with the Alaska Legislature and the general public. For these reasons, it is essential that any new software has the capacity to provide a file that can be easily uploaded and incorporated into the ARIS database structure. Software shall have the capacity to provide an XML output in one of two formats: using the same field names as the AKWarm Residential software, or an HPXML file that meets the Building Performance Institute's BPI-2100-S-2013 and BPI-2200-S-2013 Standards[11] designed to promote standardized data collection and transfer methods for the residential energy efficiency industry. If the latter is chosen, the software shall maintain the Alaska Home Energy Rating Score in the "Energy Score" field, in the "Other" energy score type category. Additionally, the "Climate Zone IECC" field shall be modified such that climate zone 9 may be entered as an option to conform to the Alaska Building Energy Efficiency Standard.


----------


<a name="definitions"></a>
Definitions
===========

> ACH: Air changes per hour; this is used to describe the leakiness of a house, and signifies how many times the total volume of air of a home is replaced over the course of an hour. ACH50 is also sometimes used, which is the number of air changes per hour that occur when a home is subjected to a 50 Pascal pressure differential, typically created using a blower door.
> 
> AHFC: Alaska Housing Finance Corporation.
> 
> AFUE: Annual Fuel Utilization Efficiency. A ratio of the annual output energy from a boiler or furnace to the annual input energy. It is a widely-referenced metric for specifying the seasonal energy usage of electric, gas, and oil-fired boilers and furnaces. Its intent is to provide a standard basis of comparison between these heating appliances for residential and light-commercial buildings. .
> 
> AKWarm: AKWarm© is the residential energy modeling software that has been used in energy audits of over 75,000 unique housing units in Alaska. It is owned by AHFC and can be downloaded for free at http://www.analysisnorth.com/AkWarm/AkWarm2download.html
> 
> Alaska Home Energy Rating Score: A score that rates the energy efficiency of a home in Alaska, with higher numbers indicating more efficient homes. The score has corresponding star ratings which are in common use in the Alaskan housing market.
> 
> ANSI: The American National Standards Institute.
> 
> ARIS: The Alaska Retrofit Information System is a database owned by AHFC and used by State agencies to track energy efficiency programs and information in Alaska. Every residential energy audit performed for a retrofit program financed by the State is stored here, as well as some commercial building audits.
> 
> ASHRAE: The American Society of Heating, Refrigerating and Air-Conditioning Engineers.
> 
> ANSI/ASHRAE Standard 140-2011: The Standard Method of Test for the Evaluation of Building Energy Analysis Computer Programs. This standard specifies test procedures for evaluating the technical capabilities and ranges of applicability of computer programs that calculate the thermal performance of buildings and their HVAC systems.
> 
> BEES: Alaska's Building Energy Efficiency Standard, which is based on the International Energy Conservation Code with Alaska-specific amendments. This standard must be met for all homes that receive AHFC financing.
> 
> BTU: British Thermal Unit, a unit of energy equal to the amount needed to cool or heat one pound of water by one degree Fahrenheit.
> 
> cfm: Cubic feet per minute, typically used as a unit for air movement through infiltration or mechanical ventilation.
> 
> DHW: Domestic Hot Water; the residential hot water produced for non-space heating purposes such as cleaning and showering.
> 
> EEM: Energy Efficiency Measure; Any type of activity or technology implemented to reduce the energy use of a building.
> 
> Energy Factor: A metric used to compare the energy conversion efficiency of residential hot water heaters.
> 
> Heating Degree Days: A measurement used to reflect the heating demand of a building in a particular climate. It is determined by summing the annual total number of degrees below 65 the temperature is per hour per day.
> 
> Home Energy Rebate Program: An energy efficiency retrofit program financed by the State of Alaska and implemented by AHFC. This program provides initial and post-retrofit energy audits and pays homeowners an incentive based on how much they increase the energy efficiency in their home.
> 
> HPXML: An XML-based standardized data collection, storage, and transfer method for the home performance industry, based on Building Performance Institute Standards BPI-2100-S-2013 and BPI-2200-S-2013, available for download at http://www.bpi.org/standards\_approved.aspx.
> 
> HRV: Heat Recovery Ventilation system; a system that provides whole-house air exchange while recovering some of the heat from the exhaust air.
> 
> HVAC: Heating, ventilation and air-conditioning.
> 
> Improvement Options Report: A report provided to homeowners after an initial energy audit that lists the recommended improvements that can be made to make their homes more energy efficient. This list should be in order of priority from the most cost-effective to the least.
> 
> NOAA: The National Oceanic and Atmospheric Administration, one of the main providers of high quality climate data in the U.S.
> 
> Real Discount Rate: The rate used to discount constant year benefits and costs that have already been adjusted to account for inflation.
> 
> Reference Home: A reference home is a house with the same dimensions and configuration as a home that is being rated but with standardized insulation levels, mechanical equipment and air leakage measurements. The comparison on energy to this home is the basis for the Alaska Home Energy Rating Score.
> 
> RESNET: The Residential Energy Services Network, an organization that makes standards for building energy efficiency rating and certification systems in the U.S.
> 
> SIR: Savings to Investment Ratio, the discounted total savings over the life of an investment (energy efficiency measures, in this context) divided by the initial capital cost of the investment.
> 
> Source-to-Site Multiplier: A multiplier used to account for the loss in energy as it is converted from one form to another at a power plant. For example, a 33% efficient diesel generator needs 3 units of diesel to produce 1 units of electricity, hence it has a Source-to-Site multiplier of 3.0
> 
> TMY3: Typical meteorological year data. A collection of data for 1020 locations in the U.S. used to represent a typical year based on climate averages over the period from 1976 to 2005. TMY3 also includes a standardized data input and storage method that can be used to create weather files for other locations with sufficient data. For more details, see the National Renewable Energy Laboratory User Manual at:
> 
> <http://www.nrel.gov/docs/fy08osti/43156.pdf>.
> 
> U-value: A measure of a material's overall effectiveness against heat loss. It is the inverse of R-value, with lower values indicating better insulative properties.
> 
> Weatherization Assistance Program: An energy efficiency program jointly financed by the State of Alaska and the Federal Government to provide energy efficiency retrofits to low-income and disabled applicants.
> 
> XML: Extensible Markup Language, which is a markup language that defines a set of rules for encoding documents in a format which is both human-readable and machine-readable.


----------


[1] See section 4.4 on Data Collection Procedures for Program Tracking and Management for details

[2] Note that software certified for use in the Weatherization Assistance Program must have already obtained U.S. Department of Energy Approval, as a portion of this program is federally funded.

[3] Deru, M., Burns, P. (2003). *Infiltration and Natural Ventilation Model for Whole-Building Energy Simulation of Residential Buildings*. Available at: http://www.nrel.gov/docs/fy03osti/33698.pdf

[4] See Table 3 in section 3.2.3 for details

[5] Available at: [http://apps1.eere.energy.gov/buildings/energyplus/cfm/weather\_data3.cfm/region=4\_north\_and\_central\_america\_wmo\_region\_4/country=1\_usa/cname=USA\#AK](../customXml/item1.xml) and [http://www.ncdc.noaa.gov/cdo-web/datasets](numbering.xml), respectively

[6] Blasnik, Michael. "Lies, Damned Lies, and Modeling." *17th Annual Westford Symposium on Building Science.* http://www.buildingscienceconsulting.com/presentations/documents/01\_Lies\_Damned\_Lies\_and\_Modeling\_rev.pdf

[7] Updated annually and available at www.nist.gov

[8] Maintenance costs may be assumed to be zero for this calculation.

[9] The models were created using homes that received an As-Is energy rating in Alaska between 2006 and 2012 and had a rating score within 3 points of the median of 69.2

[10] Please contact AHFC to obtain a copy of the logo and approved text.

[11] Standards available at http://hpxmlonline.com/
