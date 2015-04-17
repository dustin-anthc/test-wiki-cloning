# [Weatherization Energy Audit Submittal Requirements](../wiki/Images/Weatherization-Energy-Audit-Submittal-Requirements.pdf)

This U.S. Department of Energy program notice describes the minimum requirements energy auditing tools need to meet in order to be approved for use in the federal Weatherization Assistance Program.  

# Analytic Methods

## Energy Estimation Methodology

Three main sections of this Wiki deal with AKWarm's energy estimation methodology: 

1. The Energy Calculation section details the calculations used by the AKWarm software
2. The Technical Users Manual describes a variety of assumptions used in energy calculations and calculation methodology
3. and the HERS Guidelines describe the requirements that AKWarm has been shown to meet, and its appendices include the actual library data used in the calculations.  

The following section provides answers to the DOE audit questions in the form of brief descriptions and links to the relevant sections of this Wiki where more detailed information can be found.  



----------
## DOE Audit Questions and Responses 

- **What energy estimating method is used?**

>AKWarm conducts a monthly energy balance on a house design to determine potential energy requirements. The monthly energy balance includes monthly bin analyses of specific building components and mechanical systems. It evaluates the effects of solar and internal gains and determines space heating, water heating, appliances needs, based on monthly modeling of both above-grade and below grade building envelope components

>1. AKWarm uses the user-supplied information for house size, location, occupant level (number of bedrooms plus one), and energy component descriptions.

>2. From the Energy Library, AKWarm gets the weather information (temperature, wind speed and design temperature) and fuel and electric prices for the city where the home is located.

>3. For each energy use, AKWarm does monthly calculations: each routine internally loops through each month’s weather information.

>For additional information, see the [[General Overview of the Residential Space Heating Calculation|Space-Heating-and-Cooling-Energy-Calculations#general_overview]] and/or the [[Technical Users Manual section|1998-Tech-Manual#]] on the house heat balance.

- **What format of climatic data is used?  If degree-day weather data is used, what base temperature is used and why?  Which weather data sites are used by different subgrantees in the Grantee territory?**

> AKWarm uses various climatic data for its calculations, including heating degree days, annual temperatures, and wind speeds.  20 main cities in Alaska have detailed data in the climate library, and the smaller communities typically have some amount of data that is then adjusted based on the nearest main city.  For a detailed description of how climate data is used in AKWarm, see the section on [[AKWarm Weather Data|Climate]]


- **Are existing energy use and energy requirements of the dwelling determined from actual energy bills, by generally accepted engineering calculations, or optionally, both?**

>Existing energy use is generally determined by accepted engineering calculations (see the [[Energy Calculations|Space-Heating-and-Cooling-Energy-Calculations#calc_details]] section for more details).  AKWarm also allows for actual energy bills to be input into the software and it produces an actual versus modeled visualization that assessors can use to highlight potential modeling errors.  

- **Does the energy audit address all significant heating and cooling loads?**

>Yes.  See the [[Energy Calculations|Space-Heating-and-Cooling-Energy-Calculations#calc_details]] section for more details.

- **How are conductive, convective, and radiative heat losses (or gains) estimated?**

>A detailed description of how AKWarm estimates heat loss can be found in the [[Heat Loss|Space-Heating-and-Cooling-Energy-Calculations#losses]] section, and gains can be found in the [[Heat Gains|Space-Heating-and-Cooling-Energy-Calculations#internal_gains]] section.

- **How is the energy consumption of heating and cooling equipment estimated during the audit for pre- and post-weatherization?**

> For a detailed description, please see the section on [[Heating Systems|Space-Heating-and-Cooling-Energy-Calculations#heating-systems]] and on [[Cooling Systems|Space-Heating-and-Cooling-Energy-Calculations#cooling]].  In summary, energy consumption of heating equipment is estimated in one of three ways:
> 

>1. The user may choose a heating system from a supplied library of systems.  The energy from these heating systems is calculated using the Annual Fuel Utilization Efficiency metric associated with each system in the library.
>
>2.  The user may enter a certified AFUE obtained from the Air-Conditioning, Heating, and Refrigeration Institute's website.  
>
>3.  The user can enter the results of a steady state combustion efficiency test, which AKWarm then converts into an AFUE by using a ratio of steady state efficiency to AFUE of a similar heating device. 



- **How are blower door readings and the results of other tests used by the energy estimating method?**

>Blower door tests are converted to an estimated natural air leakage rate which is then used in the heat loss calculation.  See the section on [[Natural Air Leakage|Space-Heating-and-Cooling-Energy-Calculations]] for more details.

- **Does the energy audit software address domestic hot water and/or household appliance measures?  If so, how is the energy estimated for these end uses?**

> AKWarm estimates energy use for household appliances so that [[internal gains|Space-Heating-and-Cooling-Calculations#gains]] are properly accounted for, but there are no options for appliance energy efficiency measures.
> Weatherization audits using AKWarm software do address domestic hot water consumption.  Estimation of energy use of systems is calculated using the method described [[here|1998-Tech-Manual#dhw]]

- **Are estimated fuel/energy cost savings discounted to net present value?**

> Yes, the estimated energy cost savings are discounted to net present value using the DOE discount rate which is updated annually.  Please see the section on [[Improvement Calculations|1998-Tech-Manual#improvements]] and the HERS Guidelines requirements for [[cost effectiveness inputs|HERS-Guidelines#cost-effectiveness-inputs]] for more details.  


- **For multifamily audits what internal verification feature, such as trueing-up the model with actual energy consumption, does the audit use to validate each audit, or how does the Grantee otherwise ensure that the building is properly modeled?**


## Measure Interaction

- **Describe how the energy audit tool accounts for the interaction between architectural and mechanical measures.**

> AKWarm analyzes each measure separately by comparing the energy use of the building with and without the improvement.  After it determines the most cost-effective improvement, it then incorporates it into the base model and re-calculates each additional measure to determine the second most cost-effective measure and so on.  Thus if the energy efficiency measures are performed in the order of cost-effectiveness, each item in the list takes into account the effects of each previous item.  For a more detailed description of this process, see the [[Improvement Calculations|AKWarm-Software-Overview#improvement-calculations]] section. 


- [[**Provide audit results of a sample dwelling unit to document that, when moving from an architectural to a mechanical measure, the energy audit tool adjusts the estimated fuel cost savings of measures with lower, *non-interacted* savings-to-investment ratios...**]]

## Cost-effectiveness Requirements

Describe how SIRs are calculated for all individual weatherization measures and for the overall package of measures installed in a dwelling unit. Include a description of how user defined measures will be allowed, including who will be allowed to develop, procedures, and Grantee monitoring of the cost effective use of user defined weatherization measures. List the costs included in
the denominator of individual and overall SIR calculations, including at minimum the cost of materials, labor and on-site supervision.

> SIRs for weatherization measures are first calculated individually to determine the most cost-effective measure.  The most-cost effective measure is then implemented and the remaining measures are again analyzed to determine their level of cost-effectiveness after the first measure has been implemented.  This process continues iteratively until all measures have been analyzed.  For details on the actual calculation, see the section on [[Improvement-Options]].  Additionally, the [improvement cost library](../wiki/Images/Appendices/AppendixC.xlsx) may help clarify what goes into the SIR calculations. 
> 
> [[**NEED TO ADDD IN DISCUSSION OF USER-DEFINED MEASURES**]] 

- **Explain how the cost of air sealing, as an energy saving measure, is included in the SIR for the package of weatherization measures. Air sealing (i.e., the air sealing measure that uses materials referenced in the Appendix A air sealing category) is the exclusive energy conservation measure that is not required to show a post-weatherization individual SIR of
1.0 or greater. The package of weatherization measures, including costs and projected savings for air sealing, must have a post-weatherization SIR of 1.0 or greater.**

[[**NOT SURE ABOUT THIS SECTION-- NEED TO ASK AHFC**]]

- **Describe how all incidental repair costs are included in the cost of the overall package of weatherization measures and the overall SIR (See WPN 12-9 for more details).**

[[**NOT SURE ABOUT THIS SECTION-- NEED TO ASK AHFC**]]

## Measures Considered

- **Provide a list of the weatherization measures that the Grantee typically "enables" for the energy audit tool to evaluate. Include material and labor costs for these measures from a Subgrantee considered to be representative of statewide conditions. Provide the expected lifetime of each measure that is used in the SIR calculation.**

>The weatherization measures that the energy audit tool may evaluate can be found in the [Improvement Life and Cost Library](../wiki/Images/Appendices/AppendixC.xlsx).  Because of the geographic size of Alaska and the difficulty in transporting materials to many portions of the state, one generic cost number is not available.  AkWarm, the audit tool for the state, uses a community cost factor to account for differences in the installed cost of energy efficiency measures.  The list of these factors can be found in the [community cost factor library](../wiki/Images/Appendices/AppendixD.xlsx).  Additionally, the [fuel escalation factor table](../wiki/Images/Appendices/AppendixE.xlsx) is useful in understanding how the life cycle savings are determined.

## Sample Audits

-  **Provide all input data, assumptions, and audit results (recommended measures) for ten sample dwelling units of each major type of structure (e.g., single family, manufactured housing and multifamily building) typical of those weatherized by the Grantee’s program. Completed field data collection forms, including any auditor notes, must be provided for the sample dwelling units, as well as printouts of the data entered into the energy audit software. The recommended measures reports from the audit tool must show the measure cost, first-year savings, SIR for each measure, as well as total job cost and overall SIR. The report must also include a line item for incidental repair costs per WPN 12-9 Incidental Repair Measures Guidance.**

[[**AHFC should probably choose which audits they would like to use**]]
