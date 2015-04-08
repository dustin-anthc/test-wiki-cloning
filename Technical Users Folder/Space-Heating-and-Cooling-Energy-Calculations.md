-   [Introduction](#intro)
-   [General Overview of the Residential Space Heating Calculation](#general_overview)
-   [Calculation Details](#calc_details)
    -   [Temperature Difference driving Gross Heat Loss](#temp_difference)
    -   [U-Values of Shell Components](#u-values)
    -   [Natural Air Leakage and Mechanical Ventilation Rates](#air_leakage)
    -   [Internal Gain Calculation](#internal_gains)
    -   [Solar Gain Calculation](#solar_gains)
    -   [Primary and Secondary Heating Systems](#heating)
    -   [Distribution System Efficiency](#distribution)
    -   [Heating Plant Efficiency](#heat_efficiency)
-   [Cooling Load and Electricity Use](#cooling)
-   [Space Heating Design Heat Load Calculation](#design_load)
-   [How the Space Heating and Cooling Calculations differ for Commercial Buildings](#commercial)

<a name="intro"></a>
Introduction
------------

The space heating energy use calculation is the most important calculation performed by AkWarm when analyzing residential buildings and is of major importance in the commercial building energy analysis. This page describes the details of that calculation in a way that is hopefully understandable to a technical energy analyst; computer programming experience is not a prerequisite. The page focuses on the residential space heating calculation but includes a section that describes how the commercial space heating calculation differs from the residential. A description of the space cooling calculation is also included in this page.

<a name="general_overview"></a>
General Overview of the Residential Space Heating Calculation
-------------------------------------------------------------

The space heating energy use calculation is a monthly calculation; each month is analyzed separately and the monthly results are summed to produce the annual energy use. Analyzing efficiency improvements requires that AkWarm perform the calculation many times for each run of the model. To keep the time required to complete an analysis to an acceptable level, hourly or daily energy use calculations are not performed.

For each month, these are the calculations that are performed:

-   The **Gross Heat Loss** (not accounting for any internal or solar gains) of the building’s shell components, natural air leakage, and mechanical ventilation air flow is determined given the thermostat setpoints and the average outdoor temperature for the month. The Main Living Space of the home and the Garage are analyzed separately because those spaces can have different thermostat setpoints. However, after separately calculating the heat loss of the Garage and the Main Living Space, those two heat losses are combined for the subsequent steps in the calculation.

-   The **Internal Gains** from people, lights, and appliances (including the water heater) are determined. Some portion of these internal gains are usable and offset the need for space heating, and the rest of the gains cause the building to overheat beyond the thermostat setpoint temperature. A formula from the [Hot-2000 simulation program](http://www.nrcan.gc.ca/energy/software-tools/7423) is used to determine the fraction of the internal gains that are usable.

-   The **Solar Gains** from windows, skylights, and from solar incident on opaque walls and door surfaces are calculated. Again, a portion of these gains are usable and offset space heating needs; the rest of the gain causes overheating beyond the setpoint temperature. The solar gain usability is determined by analyzing the size of the gain relative to the heat loss occurring during the month.

-   The **Net Heat Load** is determined by subtracting usable internal gains and usable solar gains from the Gross Heat Loss. That net heat load is partitioned across the Primary and Secondary Heating Systems according to the user-selected amount of secondary heating system use.

-   For the primary and secondary heating systems, the **Distribution System Efficiency** is determined from the type of distribution system (forced air, hydronic, direct) and the location, insulation, and leakage of the distribution pipes/ducts. These distribution efficiencies are used to scale up the net heat load and calculate the heat load on the primary and secondary heating plants.

-   The **Seasonal Efficiency of the Primary and Secondary Heating Plants** are determined from the [AFUE](http://www.cchrc.org/sites/default/files/docs/afue_final.pdf) of the plants in the Energy Library or the direct entry of the AFUE by the user. Also, the AFUE is adjusted for the existence of any upgrade devices on the heating system (e.g. vent damper, modulating aquastat). Once the heating plant efficiency has been determined, the fuel use of the heating plant can be calculated by dividing the net heat load seen by the plant by the seasonal efficiency.

<a name="calc_details"></a>
Calculation Details
-------------------

This section provides additional details on the space heating fuel use calculation, organized in the same order as the steps of the calculation presented in the prior section.[1]

<a name="losses"></a>
##Losses
<a name="temp_difference"></a>
#### Temperature Difference driving Gross Heat Loss

The basic calculation of gross heat loss in a given month has the form of a *temperature difference* times a *building heat loss coefficient* (which is the rate of heat loss per degree of temperature difference for the building). The *temperature difference* is the difference in temperature between the inside of the building and the outdoors.

First addressing the outdoor temperature, AkWarm stores weather data in the Energy Library database. In that database are 20 primary weather cities that have temperature, wind speed, and solar radiation data available for each month. If the building that AkWarm is analyzing is located in one of the primary cities, AkWarm has access to monthly data to perform the heat loss calculation with.

If the building is located in one of the other 200+ cities in AkWarm, monthly weather data is arrived at by another means. For the cities other than the primary weather cities, *annual* temperature and wind speed data is generally available in the Energy Library. Each one of those secondary cities is associated with one of the 20 primary weather cities. The annual average data for the secondary city is used to make adjustments to the monthly data from the associated primary weather city so that a more site-specific set of monthly data is available for the AkWarm analysis.[2]

Before use in the heat loss calculation, the monthly average outdoor temperature is “revised” to adjust the temperature downward if some hours of the month are expected to have a outdoor temperature exceeding the desired heating setpoint of the building. For the vast majority of Alaskan cities and months, this adjustment is zero or very small.[3]

Two different indoor spaces are separately analyzed with AkWarm--the Main Living space and the Garage space--because these spaces can have very different thermostat setpoints. Absent a setback thermostat, the indoor temperature used in the gross heat loss calculation is simply the thermostat setpoint of the space. Internal gains and solar gains can cause these spaces to overheat beyond the thermostat setpoint, but these overheating issues are accounted for in the calculations that address the usability of internal and solar gains.

The existence and use of a setback thermostat can lower the average heating setpoint for the month, since the thermostat reduces the temperature of the indoor space during sleeping and possibly other unoccupied periods. AkWarm allows the user to specify whether a setback thermostat is used in the Main Living Space. AkWarm does not model a setback thermostat for the Garage space; if one exists, the user will need to make an adjustment to the heating setpoint in the Garage to account for the effects of the setback.

For the Main Living Space, the user is allowed to select whether the setback thermostat controls all of the space or half of the space. AkWarm makes a downward adjustment to the average indoor temperature based on this selection and other parameters. To better understand the adjustment, consider how a setback thermostat affects the indoor temperature. If the setback reduces the heating setpoint from 70 degrees to 60 degrees starting at 11 pm every night, the indoor temperature does not immediately drop to 60 degrees at 11 pm. Instead, the thermal mass of the home causes the indoor temperature to gradually decline towards 60 degrees. The indoor temperature may or may not reach 60 degrees before the setback thermostat raises the setpoint temperature in the morning. AkWarm considers this rate of cooldown when determining the overall reduction in average indoor temperature caused by the setback thermostat. The temperature reduction effect varies by month, because the rate of cooldown depends on the outdoor temperature.

Some of the assumptions that enter into AkWarm’s calculation of the effect of a setback thermostat are: a 5 degree Fahrenheit setback in the setpoint occurs for 8 hours each day; the thermal mass of the building is 3.5 Btus per square foot of living area per degree Fahrenheit, a value reflective of standard wood frame construction. If only half of the home is controlled by a setback thermostat, the reduction in temperature caused by the thermostat is reduced by 60%, because the the setback effect is hampered by the adjacent space that is not being set back. Also, when the Energy Rating calculation is performed on the building, the overall effect of the setback thermostat is reduced by 50% because not all occupants of a home effectively utilize a setback thermostat.[4]

<a name="u-values"></a>
#### U-Values of Shell Components

The gross heat loss in a particular month is product of the indoor-to-outdoor temperature difference, discussed above, and the building’s heat loss coefficient. The heat loss coefficient is the heat loss rate in Btu/hour per degree of temperature difference. Conduction through the building’s shell components is the major contributor to the heat loss coefficient. Natural infiltration and forced mechanical ventilation are the other contributors and are discussed in a subsequent section.

Rarely is the insulating value of a shell component the same across all portions of the component. For example, heat loss per unit area through the studs of a basic stud wall is larger than the heat loss per unit area through the insulated cavity of the wall. For each type of shell component, AkWarm first divides the component into sections that have the same insulating value. For the basic stud wall example, the wall is divided into three sections: the insulated cavity portion of the wall, the studs and plates portion, and the window and door header sections (the windows and doors themselves are addressed as separate shell components). AkWarm estimates the fraction of the wall that is falls into each section type and then calculates the heat loss coefficient for each of the sections. All layers of the shell component construction are considered, including interior and exterior air films. The insulating value of the exterior air film is determined from an estimated wind speed on the surface of the component. That wind speed is determined by adjusting the airport wind speed to a site wind speed that considers the terrain around the building, the wind shielding obstacles (e.g. trees), and the height of the building.[5]

Below-grade walls and floors are covered by ground on their exterior surfaces. The ground acts as additional thermal insulation, retarding heat flow through the component. AkWarm calculates an effective R-value for the ground and then adds that R-value to the R-value of the shell component. The effective ground R-value is determined by assuming semi-circular heat flow paths and a soil conductivity of 0.8 Btu/hr-ft-deg F, as described in Figure 12 on page 18.30 of the 2009 ASHRAE Fundamentals Handbook.

The R-values of the insulation types used in the shell component calculations are stored in the Energy Library. Additional insulation types are added as needed to the Energy Library. For windows, the overall U-value of a particular window frame / window glass combination is also stored in the Energy Library.

<a name="air_leakage"></a>
#### Natural Air Leakage and Mechanical Ventilation Rates

Natural air leakage also contributes to the building’s heat loss coefficient. AkWarm uses the Lawrence Berkeley Laboratory infiltration model[6] to estimate the amount of natural air leakage in each month given the 50 Pascal blower door test results entered by the user. A number of parameters in the model are fixed in the AkWarm calculation, including:



- n, the flow exponent = 0.67
- R = 0.5
- X = 0.0 

*These are parameters describing the assumed leakage distribution in the building.*

AkWarm uses the airport-to-site wind conversion method found in the LBL infiltration model to predict the site wind speed, which affects the amount of predicted infiltration. Inputs to the LBL model include the height of the building (which is entered by the AkWarm user), a Terrain Class (5 possible categories), and a Shielding Class (5 possible categories). Instead of having the AkWarm user estimate a Terrain and Shielding Class, AkWarm asks the user to select one of three general wind shielding levels: Shielded, Average, Exposed. Those selections correspond the following Terrain and Shielding classes in the LBL model:

**Shielded**: Terrain Class 4, Shielding Class 4

**Average**: Terrain Class 3, Shielding Class 3

**Exposed:** Terrain Class 3, Shielding Class 2

Because AkWarm calculates the heat loss of the garage separate from the main living space, the estimated infiltration needs to be partitioned between these two zones (it is assumed that the blower door test included both the main living space and the garage). To do this, AkWarm proportions the leakage according to the ratio of the above-grade shell component area of the garage versus the main living space.

AkWarm allows the user to specify a continuous mechanical ventilation system, if one exists. If a ventilation system exists, the user specifies whether the system utilizes heat recovery or not. For heat recovery ventilation systems, AkWarm assumes a heat recovery apparent sensible effectiveness of 0.70. The electrical power consumed for mechanical ventilation is assumed to be 0.61 Watts/CFM for systems without heat recovery, and 1.05 Watts/CFM for those with heat recovery.

If the AkWarm user checks the box “System has controls to operate at less than maximum flow, e.g. clock timer, speed controller, or humidistat”, AkWarm assumes that these controls will be used to limit the flow ventilation to a reasonable level for the home. This level of reasonable flow is discussed in the following paragraph. If the controls checkbox is *unchecked*, the user is required to enter a flow rate of the ventilation system, and AkWarm assumes that the ventilation system runs continually at that user-entered flow rate.

If the ventilation control checkbox is selected, AkWarm calculates the amount of mechanical ventilation flow for each month based on the following approach:

> 1) If there is *no* mechanical ventilation system, AkWarm still assumes that occupants will open windows to provide enough total air flow to reach 0.29 Air Changes per Hour (ACH) in the main living space (not counting the garage). If the natural infiltration in a particular month exceeds this level, then no additional air from open windows is included. But, if the natural infiltration in a month is less than 0.29 ACH, additional air flow is added to reach this target level. Thus, AkWarm does not calculate any reduced energy use in a home that is tightened below a natural air flow rate of 0.29 ACH, because AkWarm assumes occupants will use windows to restore an adequate supply of fresh air.
>
> 2) If the home does have a mechanical ventilation system, AkWarm assumes that occupants will control the system to provide a total air flow in each of month of 0.25 ACH. For example, if AkWarm calculates a natural air leakage rate of 0.15 ACH in January, AkWarm will assume that the average flow rate of the mechanical ventilation system in January will be 0.10 ACH, sufficient to produce a total of 0.25 ACH of fresh air. If the natural leakage rate in a month exceeds 0.25 ACH, the mechanical ventilation system is assumed to not operate.[7]

The above paragraphs indicate a minimum total ventilation rate of 0.29 ACH in a home *without* a mechanical ventilation system and a minimum total ventilation rate of 0.25 ACH in a home *with* a mechanical ventilation system. There is a reason for the different air change levels: for a home without a mechanical ventilation system, occupants are forced to use windows to provide additional fresh air to the home. Because the airflow provided by an open window is not very controllable, it is reasonable to assume that the average air flow will be higher than a home with a controllable mechancial ventilation system due to the poorly regulated airflow through open windows.

Because of the difference between the 0.29 ACH and the 0.25 ACH assumption, a tight home with a mechanical ventilation system having *no* heat recovery will show a lower energy use and a higher Energy Rating score than a tight home without any mechanical ventilation system. Even without heat recovery, there is a reward for installing a controllable mechanical ventilation system.

The amount of energy lost by a cubic foot of air leaving a building either due to natural infiltration or mechanical ventilation depends on the density of the air. An estimate of the average air density can be made knowing the elevation of the building above sea level; air density exponentially decays with elevation. The Energy Library has the elevation of the cities available in AkWarm; this value is used to estimate air density.

<a name="gains"></a>
## Gains
<a name="internal_gains"></a>
#### Internal Gain Calculation

Internal heat gains are generated by people, lights and appliances, including the domestic hot water heater. A large portion of these gains offset heat load and therefore reduce the heating fuel use of the building.

One source of internal heat gains is the occupants of the building. For the heating calculation, only the sensible heat gains are relevant, and AkWarm assumes the average sensible heat gain per person is 174 Btu/hour. The heating calculation is done using a monthly time step, so the overall day/night heat gain average is the proper figure to use in the calculation.

For lights and appliances other than the clothes dryer, cooking range, and domestic hot water heater, internal gains are simply calculated by assuming 95% of the electrical energy consumed by the appliance is converted to internal heat gain inside the home; the rest of the energy use is assumed to be release outside the building or into the ceiling shell component (e.g. recessed lights). For these appliances, AkWarm has two different ways of describing the overall level of usage. Because the Home Energy Rating calculated by AkWarm only considers the Space Heating and Domestic Hot Water usage of the home, the traditional method of describing lighting and appliances (other than cooking and drying) was to simply indicate if the home had Low, Average, or High usage. For Average use, the Btu/hour electric use of these lights and appliances is 1,083 + 0.6227 x Main Living Floor Area in square feet. For Low use, this figure is reduced by 35%, and for High use this figure is increased by 35%.[8]

A recent addition to AkWarm is the ability to individually itemize lights and appliances. If this approach is taken, the internal heat gain is simply the monthly electricity use of these itemized appliances expressed in average Btu/hour and then multiplied by 95% to account for some gains being released outside of the conditioned space.

Energy use and internal gains from lights and appliances are spread across the months with some seasonal variation, with a peak energy use occurring in December and a minimum in June.

AkWarm specifically addresses Clothes Drying and Cooking Range equipment. The user specifies the type of fuel used by the equipment, and then average fuel use and internal gain figures are assigned according to the fuel selected. For clothes dryers, only 19 - 30% (varies with fuel) of the energy used is assumed to generate internal gains, since much of the clothes drying heat is exhausted outdoors. For cooking ranges , 72 – 81% of the fuel energy is converted to internal gain; some leaves via the kitchen exhaust hood or is converted to latent heat, which is not useful in offsetting space heating loads.[9]

Tank type domestic hot water heaters also generate internal gains if they are located in conditioned or semi-conditioned space. AkWarm calculates the standby tank loss and assumes 100% of that loss is internal heat gain if the tank is located in conditioned space, and assumes 65% of the loss is internal gain if the tank is located in semi-conditioned space.

Not all of internal gains offset space heating load because sometimes the gains cause the home to heat beyond the thermostat setpoint, causing higher than needed heat loss. A formula from the Hot-2000 thermal modeling program is used to determine the usability fraction of the internal gains in each month. This formula depends on the ratio of the gross internal gains to the gross heat load in the month. As that ratio increases, the usability of the internal gains decreases, since overheating is more likely to occur. For Alaskan locations, the gain-to-load ratio for residential buildings is low, and thus the usability of internal gains is quite high. The Energy Flows report shows the gross and usable internal gains by month for the home being modeled.

<a name="solar_gains"></a>
#### Solar Gain Calculation

Solar gains are another type of heat gain that help offset the need for space heating fuel. AkWarm considers solar heat gain from windows, skylights, walls, and doors. For windows and skylights, the glazing system admits solar gain into the building. For opaque walls and doors, solar gain incident on the exterior surface of the component serves to increase the temperature of that surface and diminish heat loss from the building. AkWarm does *not* consider solar gain through roof components, because these components are often covered with snow, which reflects most of the solar; also, attic spaces are often present that isolate the solar gain from the conditioned space.

For the 20 main weather cities in the AkWarm Energy Library, the Library contains average solar gain per day incident on vertical South, vertical East/West, vertical North, and Horizontal surfaces. These values are provided for each month.[10] Although the Energy Library distinguishes between the East/West orientation and the North orientation, AkWarm simplifies user input by only giving three choices for glazing orientation: South, Not South, and Skylight (Horizontal).

The solar gain values in the Energy Library assume that the solar-receiving surface is unobstructed, which is rarely the case. For windows and skylights, AkWarm asks the user to specify the level of External Shading (e.g. trees, buildings, hills) and gives three choices: Little, Moderate, Heavy. AkWarm reduces solar gain by the following amounts for each choice:

> **Little**: 10% reduction
> 
> **Moderate:** 30% reduction
> 
> **Heavy:** 50% reduction

AkWarm also considers the fact that home occupants often have shades on the inside of windows, and these shades are often closed or partially closed during the daytime. To account for this impact on solar admitted to the building, AkWarm reduces the solar admitted through the glazing portion of the window by 25%.

For windows and skylights, AkWarm stores the Shading Coefficient associated with various glazing types in the Energy Library. That value along with assumptions concerning the amount of window framing allow AkWarm to estimate the Solar Heat Gain Coefficient (SHGC) for the window. The SHGC gives the fraction of the incident solar that is admitted as heat into the building, subject to the shading modifiers discussed previously. The AkWarm user can also directly enter the window’s SHGC as an input. Because the NFRC rating for windows now includes the SHGC, this value is readily available for new windows.

For walls and doors, AkWarm calculates an effective SHGC for the component.[11] The SHGC is quite sensitive to the wind speed on the exterior surface of the component. AkWarm assumes that the wind on the exterior surface of a wall or door averages 75% of the site’s wind speed, because of surfaces are on the leeward side of the building where wind speed is low. AkWarm applies an external shading (trees, buildings, hills) adjustment equal to the average for the windows of the building, since the user does not specifically enter an external shading choice for the walls and doors.

Once the gross solar admitted to the building is calculated considering all of the above factors, the usability of that solar gains needs to be estimated. Some of the solar gain causes the building to overheat, lessening the value of the solar towards offsetting space heating fuel use. An algorithm from the Hot-2000 thermal simulation program is used to calculate solar gain usability.

With this algorithm, the usability depends on the ratio of the solar gain to the net heat load after removing usable internal gains. The usability also depends on the ratio of the thermal mass of the building to the solar gain. AkWarm uses a fixed assumption for the thermal mass of the building per square foot of floor area (3.5 Btus/ft2-deg F). The Energy Flows report shows the gross solar gain and the usable solar gain by month, as calculated by AkWarm.

<a name="heating-systems"></a>
## Heating Systems

<a name="heating"></a>
#### Primary and Secondary Heating Systems

Once the net heating load is calculated (gross load minus usable internal gains and usable solar gains), that net heating load is partitioned between the primary and secondary heating systems, if a secondary system is specified by the AkWarm user. If a secondary system exists, the user must select whether the system provides a Small, Some, or Moderate level of the heating load. According to this choice, AkWarm assigns some of the heating load to the secondary system:

> **Small:** 10% of the heating load assigned to the Secondary System
>
> **Some:** 25% of the heating load assigned to the Secondary System
>
> **Moderate:** 40% of the heating load assigned to the Secondary System

This portion of the load is served by the Secondary heating system, and the rest of the load is served by the Primary system.

<a name="distribution"></a>
#### Distribution System Efficiency

Once the heating load for a Primary or Secondary Heating System is calculated, the distribution system that takes heat from the heating plant and delivers it to the conditioned spaces needs to be analyzed. That system is typically a forced air distribution system, a hydronic distribution system, or a direct-to-space system that distributes heat from a heating plant that is located within the space to be heated (e.g. a woodstove or a Toyostove). These heat distribution systems have the potential of creating additional losses to the outdoors that must be made up by the heating plant. AkWarm estimates the distribution system efficiency in order to account for these additional losses.

For forced air distribution systems, the AkWarm user is required to specify the percentage of the ductwork that is in unconditioned and semi-conditioned space. For those portions of the ductwork, the user also indicates whether the ducts are insulated to at least R-3. The user also indicates whether the ducts are Tight, Moderate, or Leaky. From these inputs, AkWarm estimates a distribution system efficiency ranging from 35% for a system with uninsulated, leaky ducts located in unconditioned space to an efficiency of 100% for ducts located entirely within conditioned space. AkWarm does not penalize forced air systems for creating room-to-room pressure imbalances that can occur even if ductwork is totally within conditioned space.[12]

For hydronic distribution systems, AkWarm again asks the user to specify the portion of the piping that is located in unconditioned and semi-conditioned space, and to specify whether those sections are insulated to at least R-3. From this information, AkWarm estimates a distribution system efficiency ranging from 83.6% for uninsulated hydronic piping located entirely in unconditioned space to 100% for hydronic piping located entirely in conditioned space. Details are available at the programming routine cited in the last footnote.

For heating systems with direct-to-space distribution, AkWarm assigns a 100% distribution efficiency.

<a name="heat_efficiency"></a>
#### Heating Plant Efficiency

Once the net heating load has been partitioned across the Primary and Secondary heating systems and the distribution efficiencies of those systems has been accounted for, the final step in calculating space heating fuel use is to estimate the seasonal efficiency of the Primary and Secondary heating plants. The AkWarm user is presented with a list of possible heating systems that comes from the Energy Library. Each one of those systems has an AFUE (Annual Fuel Utilization Efficiency) assigned in the Energy Library. If the user makes no further inputs, this AFUE is used as the seasonal efficiency of the heating plant.

However, the user has additional inputs available that can be used to modify the efficiency used by AkWarm in the calculation. One option the user has is to enter a “Certified AFUE, if Available”. If this input is filled in, AkWarm uses this AFUE value in place of the value present in the Energy Library.

Another option available to the user is to select from a few different add-on upgrade devices that are appropriate from the heating plant selected. The three possible upgrade devices are Vent Damper, Modulating Aquastat (outdoor-temperature reset control), and Flame Retention Burner. Only those upgrade devices appropriate for the heating system selected are presented to the user. If the user selects any of these upgrade devices, AkWarm increases the system AFUE by the expected improvement in the seasonal efficiency resulting from the upgrade device. The efficiency improvement is not a fixed value but instead relates to the type of system that the upgrade is applied to. For example, a conventional boiler has substantial standby losses going up the flue pipe to the outdoors. A vent damper will have a larger impact on such a system than it will on a system with low flue standby losses such a condensing boiler.

Finally, the user can enter into AkWarm the results of a combustion efficiency test. That test measures the actual operating steady-state combustion efficiency of the heating plant. The seasonal efficiency (AFUE) will be lower due to standby losses and due to losses from the jacket or cabinet of the heating plant. For each heating system type stored in the AkWarm Energy Library, the typical spread between the combustion efficiency and the AFUE is stored. For example, for a “Conventional Boiler” system type, that spread is 15 percentage points, meaning a conventional boiler with an AFUE of 60% will typically have a combustion efficiency of 75%. So, if the user enters a Combustion Efficiency test result into AkWarm, the Combustion/AFUE spread is subtracted from that value to estimate the AFUE of the plant. Returning to the Conventional Boiler example, if the user enters a Combustion Test Efficiency of 80%, AkWarm will estimate the AFUE of the boiler to be 80% - 15% = 65%. That 65% AFUE value will be used in the remaining calculations (it even overrides a Certified AFUE entry by the user). If upgrade devices are selected by the user, this 65% AFUE will be adjusted upward for the effect of those upgrade devices.

Once the seasonal efficiencies of the Primary and Secondary heating plants have been determined, the fuel use of each system is determined by dividing the net heating load served by the plant by its seasonal efficiency.

<a name="cooling"></a>
Cooling Load and Electricity Use
--------------------------------

AkWarm uses a very simple bin method to estimate the cooling load in each month. Residential cooling loads in Alaska are very low and few homes actually have cooling systems. So, accuracy in this calculation is not as important.

For each of the 20 main weather cities available in the AkWarm Energy Library, hourly bin data is stored for each month for use in the cooling load calculation. The bins are based on dry bulb temperature and are 2 degrees Fahrenheit wide. Only temperatures greater than 50 degrees F are included in the bins. For each bin, the number of hours during the month when the dry-bulb temperature falls in the bin is recorded. Also recorded for the bin is the ratio of solar gain for those hours relative to the average solar gain in the month.[13] For example, for the month of June in Anchorage, the first bin spans 50 - 52 degrees F. Recorded in that bin is the fact that 132 hours in June typically fall into that dry bulb temperature range. Also, the average solar gain during those hours is 0.314 times the average solar gain for the month, expressed on a Btu/hour/ft2 basis (this bin contains a large number of nighttime hours, thus causing the solar to be less than the month’s average). These bin values are calculated from TMY (Typical Meteorological Year) climate data.[14]

To do the cooling load calculation, AkWarm steps through each bin in the month being analyzed and calculates the cooling load associated with that bin. First, if the bin temperature is *cooler* than 5 degrees less than the cooling thermostat setpoint, AkWarm assigns no cooling load, since natural cooling from open windows is probably sufficient to cool the home. For bins above that temperature threshold, AkWarm calculates heat loss or gain due to shell component conduction and air infiltration. Average internal gains for the month are added. Finally the average solar gain for the month is scaled by the bin’s solar ratio to estimate the solar gain occurring during the hours falling in the bin.

After the total cooling load is calculated for the month, the cooling load is scaled up by the cooling distribution system efficiency. A simple IECC model of distribution efficiency is used, which depends on whether the air-conditioning ductwork is entirely in conditioned space or not, and whether the ductwork meets the IECC reduced Leakage specification. After the cooling load is increased to account for distribution losses, the user-entered Seasonal Energy Efficiency Ratio (SEER) is used to calculate the electricity use of the air-conditioning unit. The seasonal efficiency of the air-conditioner is simply the SEER divided by 3.413 Btu/hr-W.

<a name="design_load"></a>
Space Heating Design Heat Load Calculation
------------------------------------------

As well as calculating an annual energy use for space heating, AkWarm also estimates the design space heating load of the building so that a heating system can be sized properly. Many of the same calculations that were used for the annual energy estimate are reused for the design load calculation. The aspects of the design calculation that are unique are discussed here.

The design heat load calculation depends on the design outdoor conditions, including the design dry-bulb temperature and the coincident design wind speed. These values are stored in the Energy Library but also can be overridden by the user. The design temperature combined with the indoor main living space temperature and the garage temperature determine the temperature differences that the home sees during design conditions. The coincident design wind speed is important for determining the natural infiltration that occurs during design conditions, and it also affects the R-value of shell components’ exterior air films.

During design conditions, the ground temperature is substantially warmer than the outside air temperature. Because of this, shell components in contact with the ground are not subject to as extreme conditions as components exposed to outside air. AkWarm accounts for this effect by performing special analysis of shell components in contact with the ground. For those components, a portion of the Heat Loss Coefficient is assumed to apply to a temperature difference calculated between the indoor air and the ground temperature, as opposed to the extreme outdoor air temperature.

Because occupants may operate their mechanical ventilation systems differently under design conditions than under normal conditions, AkWarm asks for specific ventilation flow rates during design heat loss conditions. Both main living space and garage (if any) flow rates are requested. These are used to determine heat loss associated with ventilation air. Unbalanced ventilation systems are appropriately considered in terms of their effective flow rates.

The design heat load calculation produces separate results for the main living space and for the garage, since these spaces often utilize different heating systems. Because of this disaggregation, some additional inputs are required for the garage space, such as ventilation rate and heating distribution efficiency. Also, if there is any uninsulated wall and/or ceiling separating living space from the garage, the user is asked to enter the area. The heat flow through that common component area is used to reduce the design garage heat load and increase the design living space heat load.

<a name="commercial"></a>
How the Space Heating and Cooling Calculations differ for Commercial Buildings
------------------------------------------------------------------------------

Given the limited time available to develop the commercial AkWarm model, the general approach to the space heating and cooling calculations in the commercial model had to remain similar to that used in the residential model. There are some notable differences, many of which are described below:[15]

1.  Two zones are modeled in the building, a Perimeter zone and a Core zone. All shell heat loss, solar gain, and space heating requirements are assumed to occur in the Perimeter zone. Only cooling loads are modeled in the Core zone. The user lists spaces in the building and indicates the percentage of each space that falls into the Perimeter versus Core zone. Each space has a heating and cooling setpoint schedule. These schedules are appropriately weighted to determine the average heating and cooling setpoints for the Perimeter and Core zones.

2.  Lights are appliances are itemized in detail in the commercial model; no simple per-square-foot input option is available. Each load can be assigned to the Perimeter, Core, or Outdoors zone so that heat gains are added to the proper zone. If the time pattern of internal gains varies from a typical residential pattern, the gain-to-load ratio is modified so that a more appropriate internal gain utilization factor is calculated.

3.  Latent heat gains from occupants are accounted for and considered in the cooling load calculation.

4.  In the natural infiltration model, the user can enter blower door test results at either a 50 Pascal or 75 Pascal pressure. The user can also enter an estimate of the leakage per square foot of above-grade shell area (cfm at 75 Pa per square foot of shell), if a blower door test is not performed. Finally, the user can directly enter the blower door test flow exponent (*n*) instead of that exponent being fixed at 0.67.[16]

5.  Any number of mechanical ventilation systems can be entered. The user must specify the operating schedule of each system, the flow rate of the system, whether it is balanced flow or unbalanced flow, the heat recovery efficiency if any, and the power consumption of the system. The inputs are much more detailed than those present in the residential model.[17]

6.  Any number of heating and cooling plants can be entered, serving building load through any number of distribution systems. The building’s space heating and cooling loads can be flexibly allocated across those systems. Heating plants can serve both space heating and domestic hot water loads. The AkWarm user is required to directly enter the efficiency of the heating plants, cooling plants, and distribution systems; no Energy Library lookup is available.

[1] The routine in the programming source code that performs the residential energy calculation is the AkWarmCalc.EnergyCalc.Calculate().

[2] See the AkWarmCalc.Weather.New() routine for details on these adjustments.

[3] For those with programming experience, see the *AkWarmCalc.EnergyCalc.RevisedTemp()* function.

[4] See the AkWarmCalc.EnergyCalc.CalcSetbackEffect() routine for more details.

[5] Shell components covered by ground and those exposed to a buffer space such as an attic are treated differently.

[6] See “The Prediction of Air Infiltration”, LBL-19040, M. Sherman and B. Dickinson, July 1985 for details.

[7] More details on the mechanical ventilation calculation are in the AkWarmCalc.EnergyCalc.CalcMechVent() routine.

[8] Here is the same formula for Average use in terms of kWh/year: 2,782 + 1.599 x Main Living Floor Area in square feet.

[9] More details at AkWarmCalc.EnergyCalc.CalcApplianceEnergy().

[10] These values are generally not provided directly in climate data reports. An effective way to calculate these values for inclusion in the Energy Library is to use the National Renewable Energy Lab (NREL) System Advisor Model, which takes TMY data as a source and can provide monthly solar values for various surface angles.

[11] See the AkWarmCalc.EnergyUtil.OpaqueSHGC() routine for more details.

[12] For those with programming experience, more details concerning the calculation of distribution efficiency can be found in the AkWarmCalc.HtrDistribution.Calculate() routine.

[13] When calculating the solar ratio, TMY solar data is used and the diffuse component is weighted by a factor of 1.25 and the direct normal component is weighted by 1.0.

[14] More details on the cooling calculation are available at AkWarmCalc.EnergyCalc.CalcCoolingLoadAndFuel().

[15] The main routine that controls the Commercial energy calculation is AkWarmCalc.EnergyCalcComm.Calculate().

[16] See AkWarmCalc.AirLeakage.CalculateInfiltration() for more details on the calculation.

[17] The routine that calculates the net ventilation and energy use characteristics of the ventilation systems is AkWarmCalc.VentilationList.Calculate().
