-   [Overview of Rating Calculation Steps](#overview)
-   [Sample Calculation](#sample_calc)
-   [Additional Calculation Details](#more_details)
    -   [Standardized Operating Conditions](#soc)
    -   [Source Energy Factors](#source_energy)
    -   [Reference Home Characteristics](#reference_home)

<a name="overview"></a>
Overview of Rating Calculation Steps
------------------------------------

This document describes the calculation details for the Home Energy Rating Points and Stars calculated by AkWarm. The major steps involved in calculating the Home Energy Rating are:

1.  **Standardize the operating characteristics** of the home. The Rating is meant to give an indicator how efficient the home is and should not be affected by how the current occupants operate the home. The various operating characteristics that are standardized are described later in this document.

2.  **Determine the Space Heating and Water Heating Energy Use of the Home,** given these standard operating characteristics. The AkWarm energy calculation model is used to estimate these energy use values. Because multiple fuel types may be used to provide the space and water heat, the energy uses of these different fuel types are combined using *Source Energy* weighting factors to determine a total source energy use. These source energy factors are predominantly used to account for the conversion, transmission and distribution energy losses that occur when delivering energy to a building. Some types of energy, such as electricity, incur large such losses so have large source-to-site weighting factors.

3.  **Create a Reference Home and Determine its Source Energy Use.** A *reference home* is a home with the same amount of gross wall area, ceiling area, floor area, and volume as the actual home but with a specified reference efficiency level for its shell components and a specified efficiency and fuel type for the space and water heating equipment. The source energy use of the reference home corresponds to a particular point level on the Energy Rating scale. Currently (AkWarm version 2.2.0.3), the reference home point level is 85 points. Note that the efficiency level of the Reference Home varies across Rating regions within the state.

4.  **Determine the Source Energy use of the Home scoring 100 points on the Rating Scale**. The reference home determines one point on the Source Energy versus Rating Point linear relationship. A second point in that linear relationship is established by specifying the energy use of a 100 point home. For the 2.2.0.3 version of AkWarm and prior versions, the 100 point home is assumed to have 20% of the space heating energy use of the reference home (80% reduction in energy use) and 60% of the domestic water heating energy use of the reference home. Mathematically:
    Source Energy use of the 100 point home = (Reference Home Source Space Heating Energy Use) x 0.2 + (Reference Home Source Domestic Hot Water Energy Use) x 0.6
    The 100 point home has 80% less space heating energy use and 40% less water heating use. A lower reduction in water heating use is chosen because it is more difficult and costly to reduce water heating energy use to very low levels.

5.  **Determine the Rating Point Score for the Actual Home** by linearly interpolating or linearly extrapolating from the two points described above--the Reference Home point and the 100 rating point Home point. Limit this Energy Rating score to the range of 0 to 100 points. This process will become more clear by the example presented in a later section of this document.

6.  **Determine the Rating Star Score for this Home.** There are fixed point ranges for each Rating Star level. It is simply a matter of determining which point range encompasses the actual Rating Point score for the home to determine what the associated Rating Star level is.

<a name="sample_calc"></a>
Sample Calculation
------------------

As an example, consider a home that AkWarm calculates to have 310 MMBtu per year of source space heating energy use and 40 MMBtu per year of source domestic hot water energy use, after applying standard operating conditions to the home. The total source energy use of space and water heating is therefore 350 MMBtu per year. What would be the Rating Point score for this home?

Steps 1 and 2 are complete: standardization of operating conditions and calculation of the source energy use of the actual home. The next step is Step 3, which builds the Reference Home and models its energy use. The R-values, fuel types, and heating efficiencies for the region where the home is located are substituted into the home’s input description, and the resulting Reference Home is modeled in AkWarm. Assume that for this example, AkWarm calculates the Reference Home to have a space heating source energy use of 130 MMBtu/year and a water heating source energy use of 30 MMBtu/year, for a total of 160 MMBtu/year. The current rating system fixes the score of this Reference Home using 160 MMBtu/year of source energy at 85 Points.

Step 4 in the process is to determine the source energy use of a home scoring 100 points on the rating scale. The current rating system fixes the source energy use of the 100 point home at 20% of the space heating source energy use of the Reference Home plus 60% of the water heating source energy use. For this example, that 100 point energy use is: 0.2 x 130 MMBtu + 0.6 x 30 MMBtu = 44 MMBtu/year.

The Step 5 process of determining the Rating Point score of the actual home is best illustrated with the following diagram. A linear relationship is established between source energy use and the Rating Point score. That relationship is created by drawing a line through two points: 1) The energy use and point score of 85 for the Reference Home, and 2) The energy use and point score of 100 for the 100 Point Home. On the diagram, these two points are shown as the red dots. The blue line is the line formed by these two points. The line is constrained to not exceed 100 Rating Points or fall below 0 Rating Points.

![Example Rating Calculation Graph](https://github.com/dustin-cchrc/Wiki_Test_Repository/blob/master/rating_example.png)

Once this linear relationship is established, the source energy use of the actual home, 350 MMBtu/year in this example, is found on the blue line, and the corresponding Rating Point score is read off. For the 350 MMBtu/year home, the Rating Point score is ***60.4 Points***. This point score falls in the point range for a **2 Star Plus** home.

If the actual home had the same shape (wall area, ceiling area, etc.) but instead had a source energy use greater than 817 MMBtu/year, it would score 0 Rating Points, no matter how high the energy use beyond that level. Also, if the home had a source energy use less than 44 MMBtu/year, it would score 100 Points, no matter how low the energy use below that level.

<a name="more_details"></a>
Additional Calculation Details
------------------------------

<a name="soc"></a>
### Standardized Operating Conditions

The Home Energy Rating is intended to rate the efficiency of the home and not the occupants. Therefore a number of energy-affecting characteristics that are controlled by the home occupants are set to standard values before performing the various energy calculations associated with the rating. Also, certain other values are standardized to remove their effects from the rating process due to rating policy concerns. The items that are standardized are:

1.  The **Number of Occupants** in the home is set to value equal to:
    2.29 + 0.000411 x (Living Space Floor Area, not counting Garage)
    If the entire multi-family building is being rated, the Living Area in the above calculation is the living area per unit and the calculated occupants are per living unit as well.
    The number of occupants affect the internal gains in the building and the number of gallons of domestic hot water consumed.

2.  The **Space Heating Thermostat Setpoint** is set to 70 degrees F.

3.  The **Wind Shielding** is set to *Average*, in order to remove that input from the rating process.

4.  The **Lights and Miscellaneous Appliances** energy usage is set to *Average*.

5.  A **Cooking Range and Dryer** are included in the home and assumed to use *Electricity* as the fuel.

6.  Because of variations in how much occupants might use a secondary heating system such as a wood stove, the **Secondary Heating System is removed** from the home, and all heat is assumed to come from the Primary Heating System.

7.  All shell components that are exposed to **Garage Temperature** are changed to Living Space temperature shell components. Doing so causes all garage components to be as important as Living Space components in the rating process.

<a name="source_energy"></a>
### Source Energy Factors

The energy used by a building at the site of the building has often incurred conversion, transmission and distribution losses before reaching the building. In order to reflect these losses and also to reflect the fact that some energy forms are of higher quality and more valuable than other energy forms, source-to-site multiplicative factors are applied to the energy used by the building before adding together the energy used from multiple fuel types. The following source energy factors are used:

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

The values used for some of these factors are influenced by policy considerations. For example, the “Special Hydro” Electricity factor is applied for use of electricity in certain communities that acquire all or nearly all of their electricity from hydroelectric resources. Because the Special Hydro source multiplier is 1.5 and the normal electricity multiplier is 3.0, use of electricity for water and space heating is not discouraged as much in these communities. The current list of Special Hydro communities is:

> Craig, Douglas, Haines, Juneau, Kasaan, Ketchikan, Klawock, Kodiak, Petersburg, Sitka, Skagway, Thorne Bay, Ward Cove, Wrangell

The wood fuel types--Birch, and Spruce--receive source multipliers of 0.8, multipliers that are clearly not consistent with the concept of accounting for harvesting and transportation energy use. However, these favorable multipliers were chosen to encourage the use of wood, which is generally a renewable resource. Also, the low multipliers also reflect the lower quality of this fuel source; natural gas and fuel oil heating equipment have higher efficiencies than wood heating equipment because of the higher quality of those fuel types.

The District Steam and Hot Water energy types were given relatively favorable treatment because the heat source for these fuel types is often waste heat from an electricity generator.

<a name="reference_home"></a>
### Reference Home Characteristics

This section gives more details on the Reference Home, which is the home that has the same physical shape as the actual home but has specified efficiency characteristics. The current rating system specifies that this Reference Home will score 85 Rating Points.

#### Shell Components and Air Change Rates

The Reference Home has the same amount of gross wall area, ceiling area, floor area, and volume as the actual home. To simplify the rating process, all windows, doors, and skylights are removed from the Reference Home. This reduces the number of efficiency characteristics that need to be specified for the Reference Home (e.g. window orientations, U-values, and Solar Heat Gain Coefficients need not be specified). The Reference Home R-value for the walls is a composite R-value used to compare against the composite R-value of the actual home (the actual home *does* receive credit through the modeling process for the usable solar gain admitted by windows).

All floor components in the Reference Home are converted to above-grade floor components. If the *actual* home has below-grade floor components, the modeling process will give those components credit for the insulating value of the ground. Below-grade walls are also converted to above-grade walls when the Reference Home is created.

After these conversions are made, Reference Home R-values are assigned to the shell components and a Reference Home 50 Pascal air change rate is assigned. These R-values and air change rates vary by Rating Region, although some regions use the same R-values and air exchange rates. The table below shows the Reference Home shell and air change values.

| **Region**                        | **Floor R-Value** | **Wall R-Value** | **Ceiling R-Value** | **50 Pa Air Change Rate** |
|-----------------------------------|-------------------|------------------|---------------------|---------------------------|
| Southeast                         | 36.27             | 11.65            | 40.44               | 4.0                       |
| South Central, Kodiak & Aleutians | 25.22             | 11.38            | 40.44               | 4.0                       |
| Bristol Bay                       | 40.65             | 13.28            | 40.44               | 4.0                       |
| Interior & Yukon/Kuskokwim Delta  | 40.65             | 13.28            | 40.44               | 4.0                       |
| Northwest Coastal                 | 40.65             | 15.25            | 40.44               | 3.0                       |
| Arctic Slope                      | 44.74             | 15.20            | 54.48               | 3.0                       |

Also, the Reference Home is assumed to have a **Mechanical Ventilation** system without any heat recovery.

The R-Values and air change rates in the table were developed to keep reasonable consistency between the prescriptive BEES standard and a home that complies with BEES via the AkWarm performance-based method.

#### Space Heating and Water Heating Equipment

Space and water heating efficiency and fuel type characteristics also need to be specified for the Reference Home. The heating fuel type for all regions is assumed to be \#1 Fuel Oil, except the South Central, Kodiak & Aleutians region which is specified as Natural Gas, and the Southeast region which is specified to be \#2 Fuel Oil. All of these Reference Home fuel types have the same source energy multiplier.

The Reference Home is assumed to have a space heating system with a **80% AFUE** efficiency and a space heating **distribution system with 100% efficiency**. All Reference Homes have a **Setback Thermostat** controlling all of the home. AkWarm also models and includes the auxiliary electric use of the heating system in the space heating fuel use. This electric use is used for fans, pumps, and control devices. For regions using Fuel Oil as the Reference Home fuel type, the Btus of auxiliary electricity use is assumed to be 4.9% of the Btus of Fuel Oil use. For the region using Natural Gas, the auxiliary electricity use is assumed to be 4.4% of the Natural Gas use. These auxiliary usage values are typical for forced-air space heating systems.

For water heating the Reference Home is assumed to have a tank-type water heater located in semi-conditioned space with *no* insulating blanket and having an **Energy Factor of 0.6**. For the region with the Natural Gas fuel type, that water heater is assumed to have R-8 tank insulation and a recovery efficiency of 80%, typical for natural gas water heaters. For the Fuel Oil regions, the tank R-value is assumed to be R-12 and the recovery efficiency is 78%.
