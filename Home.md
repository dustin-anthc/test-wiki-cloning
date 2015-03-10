
![/Wiki\_Test\_Repository/AKWarmLogo.png](https://github.com/dustin-cchrc/Wiki_Test_Repository/blob/master/Images/AKWarmLogo.png)<BR>

<H1> Wiki Test Repository </H1>

Welcome to the wiki for **AKWarm** home energy rating software.  AKWarm is a free program owned by the [Alaska Housing Finance Corporation](http://www.ahfc.us/) that is used to model the energy use of residential buildings in cold climates, evaluate energy efficiency improvements, and provide an energy rating.  

The wiki is divided into two main sections-- one for current or prospective **users** of the software, and another for **AKWarm developers**


----------

# Users

### Technical Resources 
* [[Source BTUs (Including Special Hydro)|Source-BTU]]
* [[1998 Tech Manual|1998-Tech-Manual]]
* [[2007 Rating Program Evaluation|2007-Rating-Prgm-Eval]]
* [[2012 Calc Process|2012-Calc-Process]]


----------


# Developers
### The Basics
- [[Software Overview|AKWarm-Software-Overview]]:  Gives a general overview of the AKWarm software from a developer's perspective, and should be the first document read by a developer intending to work on the software.
- [[User Interface|AKWarm-User-Interface-Documentation]]: Describes the AKWarm_UI project, which is the proect that provides the user interface for AKWarm.  
- [[Calc Project|AKWarmCalc-Project]].  Describes the AKWarmCalc proect, which contains the main data structures and calculations for the software.
- [[Setup Project|AKWarm2Setup]]: Describes the AKWarm2Setup project, which produces the installer software for AKWarm.  Also describes all aspects of creating a new version of AKWarm for installation. 
- [[Energy Library Development|Energy-Library-Development-Project]]: Describes the purpose of the AKWarm Energy Library, the software routines using the Library, and how to edit and release a new Energy Library.
- [[Energy Library Maintenance|Energy-Library-Maintenance]]:  Explains the use of the command line utility created by the EnergyLibraryMaintenance project, which has the main purpose of converting Energy LIbraries from the MSAccess format to the format need by AKWarm.  

###Code Architecture Diagrams
- [Energy Calculation Diagram (PDF)](https://github.com/dustin-cchrc/Wiki_Test_Repository/blob/master/Code%20Architecture%20Diagrams/Energy%20Calculation%20Code%20Architecture%20Diagram.pdf?raw=true)
- [Water Heating Diagram (PDF)](https://github.com/dustin-cchrc/Wiki_Test_Repository/blob/master/Code%20Architecture%20Diagrams/DHWheater_EnergyCalc.pdf?raw=true)
- [Appliance Fuel Diagram (PDF)](https://github.com/dustin-cchrc/Wiki_Test_Repository/blob/master/Code%20Architecture%20Diagrams/AppFuel_EnergyCalc.pdf?raw=true)

###Calculation Details
- [[Rating Calculation|Rating_Calculation]]: Describes how the Alaska Home Energy Rating Calculation is performed.
- [[Space Heating and Cooling Energy Calculations|Space-Heating-and-Cooling-Energy-Calculations]]: Describes the space heating and cooling calculations in AKWarm, primarily focused on the residential model, but explaining in summary how the commercial model differs.
- [[Calculation Assumptions|Assumptions_Energy_Calc]]:  Lists a number of assumptions used in the residential energy calculations.

### Resources
* [[2005 Tax Credit Protocol V1.0|2005-Tax-Credit-Protocol-V1-0]]
* [[2013 BEES Update Method|2013-BEES-Update-Method]]

### Other
* [[Documentation Overview|Documentation-Overview-(mmap)]]

### TEAC Meeting Notes

![AHFC Banner](https://github.com/dustin-cchrc/Wiki_Test_Repository/blob/master/Images/AHFC%20MASTER%20HEADER.png)