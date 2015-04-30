-   [[Introduction|#remse-intro]]
-   [[How to use the Template|#how-to-use-template]]
-   [[Software Overview|#soft-overview]]
-   [[Mandatory Inputs|#mandatory-inputs]]
    -   [[Solar PV|#mandatory-pv]]
    -   [[Solar Thermal|#mandatory-thermal]]
    -   [[Wind|#mandatory-wind]]
-   [[Test Cases|#test-cases]]
    -   [[Solar PV|#test-pv]]
    -   [[Solar Thermal|#test-thermal]]
    -   [[Wind|#test-wind]]
-   [[Test Results|#test-results]]
-   [[Definitions|#remse-definitions]]

# Evaluation Template for Renewable Energy Modeling Software: *User Guide*

<a name="remse-intro"></a>
Introduction
============

This document, along with the Evaluation Template for Renewable Energy Modeling Software, outlines the minimal requirements for renewable energy modeling software to be certified for use by the Alaska Housing Finance Corporation (AHFC). Once AHFC approves a renewable energy modeling software program it may be used by approved personnel to model renewable systems and to receive credit in AKWarm for the energy offset by these systems. The Evaluation Template is the official document that will be used by AHFC and its subcontractors to determine if the applicant software meets the requirements. Evaluators shall use this guide when filling out the template. If the proposed renewable energy software meets this standard, its outputs shall be allowed to be used in all AKWarm energy ratings.

<a name="how-to-use-template"></a>
How to use the Template
=======================

There are two main requirements that renewable energy modeling software must meet in order to be certified for use:

1.  **The software must have the specified mandatory inputs and...**

2.  **The software must be capable of modeling the specified test cases within the acceptable margins.**

	
####  Mandatory Inputs:

First, software programs must have the mandatory input fields outlined in Section 3 of this document and found in the checklists of the Evaluation Template. This ensures that users will be able to enter all of the information deemed sufficient to accurately model a particular renewable energy technology per AHFC guidelines. Note that some fields, such as certain types of losses, may have built-in default values that are appropriate for this level of modeling and may be considered for approval. If these default values are not described in the software documentation, evaluators may consider contacting the software developers to determine if the fields are accounted for internally at all.

#### Test Cases:

Secondly, the software must model the test cases detailed in Section 4 and the modeled outputs must fall within the software test result ranges described in Section 5. This ensures that the algorithms being used in the renewable energy modeling software will provide an estimate of energy production that is reasonably consistent with those provided by software developed by national research organizations.

The person who is assessing whether or not a software program is approved is referred to as the "evaluator" throughout this document. The evaluator shall choose the appropriate section of the Evaluation Template for the renewable technology being modeled by the software and proceed to fill in the boxes for each input that is required. Note that the boxes in the template are color-coded, with the following significance:

| **Color:** | **Meaning:**                                                                                                                                                         |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            | Software input is required for approval.                                                                                                                             |
|            | Input is not required for approval, but is recommended. Special instructions to software users will be required to work around its absence in certain circumstances. |
|            | *Climate data only:* Software fails if the red field is the only climate data option the software can use.                                                           |

An evaluator shall fill out the Software Overview form, the applicable forms for renewable energy type, and the relevant portion of the Test Case Ranges form.

<a name="soft-overview"></a>
Software Overview
=================

In this template section the evaluator shall record all of the general information about the software so it is clear which program and version are being evaluated. Evaluators shall also comment on the usability of the software. Notes in this section should address things such as whether the user-interface is easy to navigate and whether there are help files available.

The evaluator shall also rate the required level of user knowledge needed to operate the program. There are three levels, each requiring a different level of training:

-   A **Beginner** level is software that would be easy to learn and use for all Energy Raters and would be useable by many homeowners.

    -   Raters must take a Site Analysis continuing education credit (CEU) class in order to be certified to use 'Beginner' software programs.

-   An **Intermediate** level of user knowledge means that the software would likely require some amount of training for all Energy Raters to be proficient in its use, and would be usable only by technically proficient homeowners.

    -   Raters must take a Site Analysis CEU course as a pre-requisite to be certified to use the software. In addition, Raters must also take a software specific CEU course and model, at minimum, the three Test Cases outlined in this document within the given ranges in order to become certified. This software-specific course should include instructions on how to enter user-defined panel/turbine characteristics in the case where a system is not in the software library, where and when it is necessary to enter detailed losses in AKWarm notes section, and other knowledge necessary to properly use a software program.

-   **Advanced** user knowledge signifies that the software would either require extensive training or technical background in order to use proficiently.

    -   In addition to the two CEU courses required for intermediate-level software, Raters must also submit documentation that they have renewable technology training. AHFC approved renewable training certifications may include, but are not limited to, the following:

        -   North American Board of Certified Energy Practitioners (NABCEP) certifications

        -   B.S. degree in Mechanical Engineering or higher

        -   Solar Energy International Professional Certificate

        -   Association of Energy Engineers Renewable Energy Professional (REP) certification

        -   Electronics Technicians’ Association PV or Small Wind certification

The evaluator shall include a description in the box detailing any notes on any additional software-specific special training requirements that may be required.

The evaluator shall determine whether the software program can auto-generate reports on the inputs used in the modeling process and the resulting outputs. Ideally these reports will be in PDF form, but other formats are acceptable so long as they can be converted to PDF format.

Finally, the evaluator shall check whether the software program is approved or not based on the results of the evaluation process.

<a name="mandatory-inputs"></a>
Mandatory Inputs
================

<a name="mandatory-pv"></a>
## Solar PV
      

<a name="pv-climate-inputs"></a>
### Climate Data Inputs

In this section, the evaluator shall select all climate data inputs that the software either has built-in or is able to accept. Note that the evaluator may have to refer to the software help file and/or manual to determine the source of data if it is built-in to the software library.

The software must be able to accept at least one of the climate data types listed here for approval without additional AHFC Official review. If none of these approved sources can be accepted by the software, then the evaluator and AHFC Official may review the "Other" climate data on a case-by-case basis to determine if it provides an acceptable level of accuracy. At that time, the AHFC Official may sign off on the “Other” climate data type.

Here are brief descriptions of the pre-approved climate data sources with at least one link to download climate data of that type:

-   ***TMY2***: This is an hourly data set for a one year period including both solar radiation and meteorological data. TMY stands for "typical meteorological year" and is determined by looking at data from 1961-1990 and using an algorithm to choose each month with the most typical weather. Data are available at the [National Solar Radiation Database website](http://rredc.nrel.gov/solar/old_data/nsrdb/1961-1990/tmy2/)

-   ***TMY3***: This an hourly data set for a one year period developed in a similar manner as the TMY2 data but based on more recent meteorological measurements (1991-2005 or 1976-2005 where sufficient data is available). TMY3 data also includes more sites in the US, with measurements from 1,020 sites. TMY3 is also a file format; that is, user collected data from specific sites may be entered into this format and recognized by many software programs. Official TMY3 datasets are available at the [National Solar Radiation Database website](http://rredc.nrel.gov/solar/old_data/nsrdb/1991-2005/tmy3/)

-   ***NASA SSE***: NASA's Surface Meteorology and Solar Energy 6.0 database includes solar energy and meteorology data derived from 22 years of satellite data. Though generally high-quality surface measured data will be more accurate, SSE data has has been compared with ground site data throughout the globe and falls within a reasonable range of accuracy. The primary advantage of the SSE data is that it is available for any location on earth, which is particularly important because many communities in Alaska do not have TMY3 data. SSE data is available at the [NASA website](https://eosweb.larc.nasa.gov/cgi-bin/sse/grid.cgi?email=skip@larc.nasa.gov)

-   ***EnergyPlus Weather (EPW)**:* EPW is a file format that was developed by the US Department of Energy to be compatible with the EnergyPlus Energy Simulation Software. In Alaska, it is populated by TMY2 and TMY3 data. Data in this format is available for download at the [EERE website](http://apps1.eere.energy.gov/buildings/energyplus/cfm/weather_data3.cfm/region=4_north_and_central_america_wmo_region_4/country=1_usa/cname=USA%23AK)

### System Orientation

Solar PV modeling software must have three system orientation input fields to qualify for approval:

-   **Azimuth:** The azimuth is the compass orientation of the panels where 0 is facing North and 180 is due South. Software shall have the capability of adjusting the compass orientation inputs by increments of 1 degree or smaller.

-   **Tilt:** The tilt defines the angle of the panel with respect to the ground in degrees, where 0 is horizontal and 90 is vertical. Software shall have the capability of adjusting the compass orientation inputs by increments of 1 degree or smaller.

-   **Tracking:** Software must also have the ability to model PV modules that track the sun; thus it is required that there be a way of choosing whether a panel is fixed or has a one- or two-axis tracking system.

Evaluators shall check each box if the input is available, and all boxes in this section must be checked for approval.

### Losses

Software must have a section to input losses in order to be approved. As long as there is some mechanism for inputting total system losses, the first box should be checked. A section for inputting shading losses is also required, as international studies have found annual energy production to be reduced on average between 5 and 10% from shading.[1](http://www.physics.arizona.edu/~cronin/Solar/References/Shade%20effects/sdarticle%20%282%29.pdf) These may be the same input field.

Software programs should have a section for itemized losses that can capture events such as snow or dirt covering the panels. If the software does not have a place to input these losses, on software approval, the Energy Rater shall be required to list these losses explicitly in the "Notes to AHFC" section of AKWarm.

### System

Software shall have **one** of the following three options:

1.  built-in PV module and inverter libraries,

2.  the ability for users to enter in system and inverter characteristics, or

3.  a combination of the (1) and (2).

If the software program has a built-in PV module library, the library shall contain system size ratings that have been verified through independent testing. One pre-approved source for such values is the California Energy Commission's (CEC) [*Incentive Eligible Photovoltaic Modules* list](http://www.gosolarcalifornia.ca.gov/equipment/pv_modules.php). Built-in inverter libraries shall also have independently verified efficiency ratings such as those found on the [CEC's list](http://www.gosolarcalifornia.org/equipment/inverters.php).

If the software program has the ability to enter in module and inverter characteristics, it shall include inputs for rated DC system size (or panel size, efficiency and number of modules) and inverter efficiency.

### Outputs

To receive approval, software programs must have the capacity to produce monthly and annual AC energy production numbers. Evaluators shall check these boxes if these values are available as outputs in the program.

<a name="mandatory-thermal"></a>
Solar Thermal
-------------

### Climate Data Inputs

Solar thermal climate data inputs are the same for solar PV climate data inputs. See the [[above section|#pv-climate-inputs]] for details on acceptable climate inputs for solar thermal systems.

### System Orientation

Solar thermal modeling software must have two system orientation input fields to qualify for approval:

-   **Azimuth:** The azimuth is the compass orientation of the panels where 0 is facing North and 180 is due South.

-   **Tilt:** The tilt defines the angle of the panel with respect to the ground in degrees, where 0 is horizontal and 90 is vertical.

Evaluators shall check each box if the input is available, and all boxes in this section must be checked for approval.

### Losses

Software must have a section to input losses in order to be approved. As long as there is some mechanism for inputting total system losses, the first box should be checked. A section for inputting shading losses is also required. [4] These may be the same input field.

Software programs should have a section for itemized losses that can capture events such as snow or dirt covering the panels, wiring losses, etc. If the software does not have a specific place to input these losses, on software approval, the Energy Rater shall be required to list these losses explicitly in the "Notes to AHFC" section of AKWarm.

Pumps that are part of solar thermal systems will typically account for some amount of energy usage that needs to be factored in. Ideal modeling software should have inputs for the rated pump characteristics and estimate the annual energy use. Pump power can also be estimated and entered into a generic system loss field. If the software does not have a specific place to input these losses, on software approval, the Energy Rater shall be required to list these losses explicitly in the "Notes to AHFC" section of AKWarm.

It is also recommended that the program have an input field either for the insulation level of the thermal storage tank or the associated storage tank losses. If the software does not have a specific place to input these losses, on software approval, the Energy Rater shall be required to list these losses explicitly in the "Notes to AHFC" section of AKWarm.

### Collectors

Solar thermal modeling software shall either have a built-in library of Solar Rating and Certification Corporation (SRCC) rated collectors or allow users to define panels using SRCC collector specifications. An input field for the number of collector panels in the system is also required. In addition, software must allow the user to specify whether the collector fluid is water or glycol. It is recommended, but not required, that software also allow users to specify different blends of water and glycol.

If the software does not have a built-in collector library, it shall have an input field for the type of collector and the collector area as well as two specific collector efficiency inputs which can be obtained from the SRCC rating, which shall be provided as an attachment to the AKWarm file as supporting information. The first input is the optical gain efficiency, referred to as FR<sub>ta</sub>, tau alpha, and as the Y-intercept in the International Standard Organization's (ISO) equation. The second input is the collector's thermal loss efficiency, referred to as Fr UL or as the slope in the ISO equation found on SRCC ratings.

### Storage

Solar thermal modeling software shall have the input fields necessary to factor in hot water storage into the annual energy yield estimates. There are four primary parameters required to do this: the size of the storage tank, the set-point temperature of the water in the tank, the efficiency of the heat exchanger, and the incoming water temperature. While the first three should all have specific fields for user input, note that the supply water temperature may be calculated automatically by the software program from the supplied climate data.

### Outputs

To receive approval, software programs must have the capacity to produce monthly and annual energy production numbers. Evaluators shall check these boxes if these values are available as outputs from the program.

<a name="mandatory-wind"></a>
Wind
----

### Climate Data Inputs

In this template section, the evaluator shall check that the software has the capacity to take hourly wind resource data. Due to the need to accept site-collected anemometer data software shall be able to accept hourly wind resource data from an outside source.

Software shall also have the ability to input a wind shear coefficient so that wind resource data can be adjusted for cases in which the data does not match the turbine hub height.

### Losses

Software must have the capacity for users to input the net losses of the system. Software qualifies whether it has multiple fields for losses or simply one field for all losses. If the software does not have specific places to input these itemized losses, on software approval, the Energy Rater shall be required to list these losses explicitly in the "Notes to AHFC" section of AKWarm.

### System

Wind modeling software shall have an input for the hub height of the turbine in order to properly match the wind resource data with the turbine power curve. The software shall also have either a built in wind turbine library listing Small Wind Certification Council (SWCC) certified turbines or shall have the capacity to define a new turbine.

If the software only has the capacity to create a user-defined turbine, then it must have a pre-approved configuration of inputs for the power curve. Two pre-approved input configurations are:

1) a table with wind speeds in increments of 1 m/s or equivalent and the power output at the given wind speeds, or

2) rated output of the system at 11 m/s of wind speed, the peak power output and wind speed at which the peak power is reached, and the cut-in and cut-out wind speeds.

Other methods for defining the power curve may be approved by an AHFC Official.

### Outputs

To receive approval, software programs must have the capacity to produce monthly and annual energy production numbers. Evaluators shall check these boxes if these values are available as outputs in the program.

<a name="test-cases"></a>
Test Cases
==========

In order to ensure that the software modeling algorithms produce results within a reasonable range, all programs seeking certification for use with a given type of renewable energy technology shall model the following relevant test cases and produce results within the range provided on the Test Case Ranges form of the Evaluation Template.

<a name="test-pv"></a>
Solar PV
--------

Three test cases shall be modeled for Solar Photovoltaic modeling software. The ranges for the test cases were produced using TMY3 data from the following sources:

-   Anchorage Merrill Field,

-   Fairbanks International Airport, and

-   Juneau International Airport.

Applying software shall use these TMY3 sources, or if unable to use TMY3 data, the nearest source for the climate data they can use.

The applicant software shall use all of the required inputs detailed here when modeling each test case. A second list of detailed inputs is also available below if additional inputs are required by the software; however, these are not mandatory if the software does not require them. Software applicants shall supply the actual file and/or a report containing all of the inputs used in the various test cases.

The evaluator shall verify that the applicant software used the appropriate inputs when modeling each test case, and then shall verify that the modeled outputs for each test case are within the ranges found in the Evaluation Template.

**Required Inputs for all Solar Photovoltaic Test Cases:**

-   *System Information:*

	-   *Library:*

    	-   *Solar Module Type:* SolarWorld 250 Monocrystalline

   		-   *Number of modules:* 18 panels (2 strings of 9 modules)

    	-   *Inverter Manufacturer:* SMA America

    	-   *Inverter Model:*  SB4000 US (240V)

	-   User-Entered:

    	-   *Rated System Size:* 4.5 kW

    	-   *Inverter Size:* 4 kW

-   *Inverter efficiency:* 96.08% efficiency (using Sandia labs / CA energy commission database) *Tracking Type:* Fixed

-   *Panel Tilt*:

	-   Anchorage: 60 degrees

	-   Fairbanks: 90 degrees

	-   Juneau: 45 degrees

-   *Azimuth*: 180

-   *Losses*:

    -   *Detailed losses shall be used if available*

        -   *Snow and Soiling:* 2%

        -   *Mismatch:* 2%

        -   *Connections:* 0.5%

        -   *Wiring*: 2%

        -   *Nameplate error:* 1%

        -   *Availability:* 3% loss

        -   *Light degradation:* 1.5%

	-   *If detailed loss inputs are not available, total non-shading losses* shall be set to 11.4%

	-   *Shading losses*:

        -   Single Number Entry:

            -   Anchorage, 60 degree tilt: 14.7%

            -   Juneau, 45 degree tilt: 17.8%

            -   Fairbanks, 90 degree tilt: 19.0%

        -   Other Shading Entries:

            -   For tabular losses, see attached file “PV Test Case Shading Data”

            -   For shading picture, see attached file "Shading Sunpath Image"

-   **Additional Input Details (if options are available):**

    -   *DC to AC ratio*: 1.125

    -   *Ground Coverage Ratio*: 0.3

    -   Roof-mounted panels

<a name="test-thermal"></a>
Solar Thermal
-------------

Three test cases shall be modeled for Solar Thermal modeling software, all using TMY3 data. These cases shall use the following **TMY3** locations for climate data:

-   Anchorage Merrill Field,

-   Fairbanks International Airport, and

-   Juneau International Airport.

The applicant software shall use all of the required inputs detailed here when modeling each test case. A second list of suggested input details is also available below if additional inputs are required for proper modeling; however, these are not mandatory. Software applicants shall supply the actual file and/or a report containing all of the inputs used in the various test cases.

The evaluator shall verify that the applicant software used the appropriate inputs when modeling each test case, and then shall verify that the modeled outputs for each test case are within the ranges found in the Evaluation Template.

Note that there is a section for both kilowatt hours per year and million's of BTUs per year for convenience; only one of these sections needs to be filled out.

-   ***Required Inputs for all Test Cases***

    -   *Hot Water Load:*  80 gallons DHW / day (302.4 kg DHW / day)

    -   *Tilt:*

        -   Anchorage: 60 degrees

        -   Fairbanks: 90 degrees

        -   Juneau: 45 degrees

    -   *Azimuth:*  180

    -   *Working fluid:* 100% glycol

    -   *Number of collectors:* 3

    -   *Collector type:*  Glazed Flat Plate

    -   *Collector manufacturer:* Heliodyne Inc.

    -   *Collector model*:   Gobi 408 002

    -   *Shading:* See “SolarPathfinder Test Case Shading”

    -   *Annual miscellaneous losses (from snow, soiling, etc.-- not including tank and pump losses):* 5%

    -   *Storage tank size:*  120 gallons (0.454 cubic meters)

    -   *Heat exchanger effectiveness:* 75%

    -   *Storage tank water temp:* 130 F (55 C)

-   **Additional Input Details (if options are available):**

    -   *Solar tank U-value:* 0.125 (R-8)

    -   *Water mains supply temp*:  If not automatically calculated by software, annual average shall be set to 40 F (4.4°C)

    -   *Max hot water temp:* 200 F (93.3 C)

    -   *Room temp in tank location:* 68 F  (20 C)

    -   *Pump / piping:*

        -   *Pump efficiency:* 85%

        -   *Pump power:* 60 Watts

        -   *Insulation U-value:* 0.3 W/m2 °C (R-3.3)

        -   *Piping length:* 50 feet (15.24 m)

        -   *Pipe diameter:* 1” (0.0254 m)

<a name="test-wind"></a>
Wind
----

The following three test cases shall be modeled in the applicant wind software program using the hourly wind resource data provided. All of the required inputs below shall be used; if the specified turbine is not in the program's turbine library, the detailed turbine inputs shall also be required.

### Wind Resource Data

Wind resource data files are not standardized across the industry. Due to this fact, evaluators will need to be flexible with software programs; the anemometer data provided along with this User Guide and Evaluation Template may need to be reformatted in order to be used in another program. Additionally, all of the original data that was used to create the attached wind resource data files for these test cases is available at the Alaska Energy Authority's [wind energy analysis data website](http://www.akenergyauthority.org/Programs/AEEE/Wind/analysisdata%20).

-   Bethel:  

    -   *Wind Resource Data:* Alaska Energy Authority Met tower data for wind speed (30 / 50 meters), direction, and ambient temperature and TMY3 data for pressure (see wind resource file).

    -   *Wind shear coefficient:* 0.118

-   Dillingham:

    -   *Wind Resource Data:* AEA met tower data for wind speed (19.5 and 29.26 meters), direction, and ambient temperature and TMY3 data for pressure (see wind resource file).

    -   *Wind shear coefficient*: 0.214

-   Kodiak Island

    -   *Wind Resource Data:* AEA met tower data for wind speed (20 and 30 meters), direction, and ambient temperature and TMY3 data for pressure (see attached wind resource file)

    -   *Wind shear coefficient*: 0.129

### Required Inputs

-   *Turbine Manufacturer:* Endurance Wind Power, Inc.

-   *Turbine Name:* S-343

-   *Hub height:* 27.5 meters

-   *Net Losses:* 17.7%

### Detailed Turbine Inputs

-   *Rated Power @ 11 m/s:* 5.4 kW

-   *Peak Power:* 6.0 kW @ 13.0 m/s

-   *Cut-out wind speed:* 25 m/s

-   *Cut-in wind speed:* 5.0 m/s

-   *Tabulated power curve:* Available at the [small wind certification website](http://smallwindcertification.org/wp-content/new-uploads/2014/10/Summary-Report-10-09-2014.pdf)

<a name="test-results"></a>
Test Results
============

The evaluator shall enter the annual energy production in the designated spaces on the Test Case Ranges form of the Evaluation Template and add any relevant notes in the space provided.

The process used to determine the ranges for the test cases was modeled after the *comparative testing* procedure used to determine the BESTEST ranges for home energy software.[5] Empirical data was not used because of a lack of long-term validated data on residential renewable systems in Alaska; short-term data is available but may cause discrepancies due to variations in annual climate, maintenance procedures, system design, and installation details. The ranges were determined by using three different industry-standard software programs to model the test cases in the case of solar PV[6], two for solar thermal[7], and two for wind.[8] The mean annual energy production for all programs was determined, and a range of +/-18% was added to either side. This range represents the maximum variance found between a test case mean and the tested software programs modeling the same test case rounded up to the next whole percentage.

If the software program has met all of the required input and output fields and the test case models all fall within the specified range, it is recommended that it be approved for use in AKWarm. The software may be used to model residential-scale renewable energy technologies in Alaska and input the estimated monthly energy production into AKWarm. Homeowners may receive credit in AKWarm for the energy use offset by renewable production.

Note that, on use of approved software, it is the responsibility of the Energy Rater or Assessor to model the renewable system per AHFC's guidelines and to attach the file used to model the system to the AKWarm rating.


----------
<a name="remse-definitions"></a>
Definitions
===========

**Azimuth:** The compass orientation of a solar panel, where 0 degrees is North and 180 degrees is facing due South.

**CEU:** Continuing Education Credits, which are required for maintenance of various building, engineering, and professional licenses.

**DC system size:** The combined nameplate power rating of all of the solar pv panels in an array. Solar pv panels produce Direct Current electricity which must then be converted to Alternating Current (AC) electricity for use in most homes. Note that the nameplate ratings for panels may be at Standard Test Conditions (STC) or at PVUSA Test Conditions (PTC), which will produce slightly different ratings.

**Evaluator:** The person who is using the Evaluation Template to determine if a software program will be approved for use in AKWarm. This may be AHFC personnel or a qualified contractor from another organization.

**Evaluation Template:** A template to be used with this User Guide that is to be filled out by the Evaluator. The results of completing the template will allow the Evaluator to make a final determination on whether to approve a new renewable energy modeling software program.

**Inverter:** A device that converts the variable DC power produced by a solar pv panel into AC power that can be used directly by the home or exported to a utility grid.

**ISO:** International Standards Organization, a non-governmental agency composed of national standards organizations from around the world which create international standards.

**Losses:** The annual reduction in energy production due to various factors, including:

-   *Snow and Soiling:* Losses caused by snow/dust/dirt/bird poop covering some portion of the panels

-   *Mismatch:* Electrical losses due to slight differences caused by manufacturing imperfections between modules in the array that cause the modules to have slightly different current-voltage characteristics.

-   *Wiring:* Resistive losses in the DC and AC wires connecting modules, inverters, and other parts of the system.

-   *Connections:* Resistive losses in electrical connectors in the system.

-   *Light Degradation:* Effect of the reduction in the array's power during the first few months of its operation caused by light-induced degradation of photovoltaic cells.

-   *Nameplate Rating:* The nameplate rating loss accounts for the accuracy of the manufacturer's nameplate rating. Field measurements of the electrical characteristics of photovoltaic modules in the array may show that they differ from their nameplate rating.

-   *Availability:* Reduction in the system's output cause by scheduled and unscheduled system shutdown for maintenance, grid outages, and other operational factors. 

**Met tower:** Meteorological towers are used to gather wind data necessary for site evaluation and typically include anemometers and other measurement devices at one or more heights.

**Power Curve:** A graph or table that indicates how large the electrical power output will be for a wind turbine at different wind speeds.

**Solar PV:** Solar photovoltaic panels are a renewable energy technology that produces electricity from sunlight. These are typically what most people think of when they picture a solar panel.

**Solar Thermal:** Solar thermal collectors use energy from the sun to heat a fluid which can then be pumped to a storage tank for use in home heating or domestic hot water.

**SRCC:** The Solar Rating and Certification Corporation is a non-profit, independent third-party certification entity which certifies the claims of solar thermal panel manufacturers.

**Test Cases:** Hypothetical renewable energy systems that have defined characteristics and have been modeled in industry-standard software to determine a reasonable range of acceptable estimates of energy production for testing purposes.

**Tilt:** The tilt defines the angle of the panel with respect to the ground in degrees, where 0 is horizontal and 90 is vertical

**TMY2:** Typical Meteorological Year data represents an "average" year of climate data for a particular region. TMY2 was created from data from the period between 1961 and 1990. TMY2 is also a data format that users can convert their site collected data into.

**TMY3:** Typical Meteorological Year data represents an "average" year of climate data for a particular region. TMY3 was created from data from the period between 1976 and 2005 where available, and 1991-2005 for other locations. TMY3 is also a data format that users can convert their site collected data into; note that TMY2 and TMY3 formats are *not* interchangeable.

**Wind shear coefficient:** A coefficient used for converting wind speed from one height to another height. The coefficient can be calculated if wind speeds at more than one height are known or can be estimated using engineering tables based on the surface roughness of an area.


----------
### References
[1] Drif, M.; Perez, P. J.; Aguilera, J.; Aguilar, J. D. (2008). "A new estimation method of irradiance on a partially shaded PV generator in grid-connected photovoltaic systems". *Renewable Energy* **33** (9): 2048–2056.  Available at:  [http://www.physics.arizona.edu/~cronin/Solar/References/Shade%20effects/sdarticle%20%282%29.pdf](../customXml/item1.xml)

[2] [http://www.gosolarcalifornia.ca.gov/equipment/pv\_modules.php](numbering.xml)

[3] [http://www.gosolarcalifornia.org/equipment/inverters.php](styles.xml)

[4] International studies have found annual energy production to be reduced on average between 5 and 10% from shading. Drif, M.; Perez, P. J.; Aguilera, J.; Aguilar, J. D. (2008). "A new estimation method of irradiance on a partially shaded PV generator in grid-connected photovoltaic systems". *Renewable Energy* **33** (9): 2048–2056.  Available at:  [http://www.physics.arizona.edu/~cronin/Solar/References/Shade%20effects/sdarticle%20%282%29.pdf](stylesWithEffects.xml)

[5] Judkoff, R and Neymark, J. "The BESTEST Method for Evaluating and Diagnosing Building Energy Software." American Council for an Energy Efficient Economy. http://aceee.org/files/proceedings/1998/data/papers/0515.PDF

[6] NREL's System Advisor Model and PVWatts, as well as the SolarPathfinder PV Assistant.

[7] NREL's System Advisor Model and the SolarPathfinder Thermal Assistant.

[8] The System Advisor Model developed by NREL was used to model the wind test case and was compared to the industry-standard Windographer software; results showed that capacity factors differed by less than 1%.
