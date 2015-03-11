-   [Introduction](#introduction)
-   [Object Models](#object_models)
-   [Calculations](#calculations)
-   [List of Files and Associated Descriptions](#list_files)
    -   [Residential Energy Related](#residential_energy)
    -   [Residential Lights and Appliances](#residential_lights)
    -   [Shell Components and Related](#shell_components)
    -   [Energy Classes used by both Residential and Commercial](#energy_classes)
    -   [Commercial Energy Related](#commercial_energy)
    -   [Commercial Electrical Loads](#commercial_electric)
    -   [Commercial HVAC Related](#commercial_hvac)
    -   [Commercial Usage Scheduling Classes](#commercial_usage)
    -   [General Purpose Data Structures](#data_structures)

<a name="introduction"></a> Introduction
------------

The AkWarmCalc project contains classes that hold and process the user’s input data and hold the results of AkWarm’s energy, rating, and improvement calculations. No user interface code is contained in this project. The AkWarmCalc code in theory could be used with a number of different user interface implementations but is currently being used with one implementation, that being the Windows Forms interface in the AkWarm\_UI project.


<a name="object_models"></a>
Object Models
-------------

For one particular AkWarm analysis, which is either one residential building or one commercial building, the data for that analysis is stored in an object hierarchy (a root object containing other objects, which in turn contain objects, etc). For a residential analysis, the root object in the object model is of the type *Project*. The hierarchy of objects starting with the root *Project* object describe the inputs to the residential home analysis and also hold a number of the calculated results. For an analysis of a commercial building, the root object is of the type *ProjectComm.* A similar hierarchy of objects is contained within that root object.

The two diagrams below, which have links to more readable full size diagrams, show the AkWarm Residential Object Model and the AkWarm Commercial Object Model. The diagrams show some of the most important objects in the hierarchy but many more objects are present in the models. These objects can be investigated through examination of the source code.


![Residential Object Model](https://cloud.githubusercontent.com/assets/8260437/6024780/abd09804-ab9b-11e4-96a5-2250acfce031.png)

![Commercial Object Model](https://cloud.githubusercontent.com/assets/8260437/6024775/a22734ca-ab9b-11e4-95e3-73e49bfbc4d5.png)

When a user saves an AkWarm analysis to the user’s hard drive, each individual analysis occupies a separate file on disk. The application does *not* utilize a database system to store multiple AkWarm analyses within one database. AkWarm uses the .NET System.Xml.Serialization libraries to serialize the *Project* or *ProjectComm* object hierarchy into an XML document that is compressed and lightly encrypted before being stored on disk as an *.hm2* (residential) or *.hmc* (commercial) AkWarm file. See the *Project.SerializeToFile()* and *Project.ToByteArray()* methods for details on the serialization process.


<a name="calculations"></a> 
Calculations
------------

Three different calculations are performed on a residential building--the energy use calculation, the home energy rating calculation, and the improvement analysis calculation. For commercial buildings, the same calculations are performed with the exception that the energy rating calculation is not performed. All of the calculation code is found in this *AkWarmCalc* project. The energy use calculation is performed by the *Calculate()* method found in the *EnergyCalc* class for the residential analysis and the same-named method in the *EnergyCalcComm* class for the commercial analysis. Energy use is calculated on a monthly basis and includes space heating, space cooling, water heating, and lights and appliances energy use.

For the residential analysis, the Home Energy Rating calculation is performed by comparing the energy use of the residential building being analyzed against the energy use of a “reference” building built with components of a prescribed level of energy efficiency. That home energy rating calculation is performed by the *Rate()* method of the *BEESrating* class. Because the rating process involves a comparison of energy use, the previously-described energy use calculation is used by and is of central importance to the rating calculation.

Both the residential and commercial modules analyze possible energy efficiency improvements to the building. The improvement analysis is performed by modeling the energy use of the building *without* the improvement applied and then modeling the building *with* the improvement applied. The difference in total energy use of the building between those two configurations is the energy savings attributable to the improvement. Because the *total* energy use of the building is used in the improvement savings calculation, the improvement’s impacts on all energy uses (space heating, space cooling, etc.) are accounted for.

Efficiency improvements interact with each other in the sense that the application of one improvement can affect the savings realized by a different improvement. For example, adding insulation to an attic saves more energy when the home uses an inefficient heating system than when the home uses an efficient heating system. Therefore, implementation of a heating system improvement will diminish the savings from an attic insulation improvement.

Because of the issue of interaction between improvements, an order of implementing improvements must be established. AkWarm applies improvements in order of cost-effectiveness, applying the most cost-effective measure first. If there are ten improvements to analyze, AkWarm analyzes all ten improvements to determine the most cost-effective improvement to apply. After determining that improvement and applying it to the building, AkWarm re-analyzes the remaining nine improvements (because interaction may have changed their cost-effectiveness) to determine the next most cost-effective improvement. This process continues until all of the improvements are applied. Because each improvement is re-analyzed many times, the analysis of improvements is clearly the most time-consuming portion of the AkWarm calculations. The number of energy calculations required goes up as the square of the number of improvements. Buildings with a large number of improvements can take a significant amount of time to calculate, particularly for commercial buildings where energy calculations are more computationally intensive.

The improvement analysis for the residential analysis is performed by the *AnalyzeImprovements()* method in the *ImprovementAnalyzer* class. For the commercial analysis, the *Calculate()* method in the *ImprovementAnalyzerComm* class is used. The general structure for analyzing improvements for commercial buildings is much cleaner than the structure used in the older residential analysis, although both produce the same results. Code structure would be improved and would be more consistent if the residential improvement analysis code were restructured to match the commercial code.

After AkWarm performs the calculations above, some of the results of the calculations are stored in the object model so that those results are serialized into the AkWarm file. None of the calculated results *need* to be stored in the AkWarm file, since the calculated results can always be reproduced from the user input values, which are stored in the file. However, the data in the AkWarm file is ultimately loaded into the ARIS (Alaska Retrofit Information System) database, and the calculated results are essential for producing ARIS reports and analyses. A very large number of calculated values are available, and only the most important values are saved in the AkWarm file.


<a name="list_files"></a>
List of Files and Associated Descriptions
-----------------------------------------

The files in the AkWarmCalc project are listed below with short descriptions of their purpose. The files are categorized by function.


<a name="residential_energy"></a>
### Residential Energy Related

These files are used in the Residential analysis only and are files that address energy characteristics or calculations for the home.. Other residential-only files are found in the *Residential Lights and Appliances* category that follows this one.

**BEESrating.vb -** Performs the Home Energy Rating calculation. Main entry point is the *Rate()* method. This class name is misleading as the rating calculation is done for purposes other than just BEES compliance.

**BEESratingResults.vb -** Stores the results of the Home Energy Rating calculation for inclusion in the AkWarm file.

**CalcController.vb -** Is used to initiate the energy, rating, and improvement analysis calculations (improvement analysis is started in a separate thread). Also stores the results of those calculations in the proper objects for inclusion in the AkWarm file. The main entry method is *Calculate()*.

**CoolingSystem.vb -** Models a residential cooling system.

**DesignHeatLoss.vb -** Holds the inputs for the design heat loss calculation. Has convenience methods for selecting between Energy Library values or User inputs when the user chooses to override Library values.

**DHWheater.vb -** Models the domestic hot water heater for the home and calculates its energy use (see the *CalcEnergyUse()* method).

**DHWheaterList.vb -** A list class for holding the DHWheater object for the home. Currently only has one water heater but is capable of holding multiple heaters.

**DHWheater\_out.vb -** Holds calculated or Energy Library look-up values associated with the domestic hot water heater. These are held in an object so that they can be archived in the AkWarm file.

**EnergyCalc.vb -** The class that performs the annual energy use and the design heat loss calculations for the home. The main entry point is the *Calculate()* method.

**EnergyResults.vb -** Stores the results of the annual energy use and design heat loss calculations performed by the *EnergyCalc* class. This object is stored in the AkWarm file.

**HealthSafetyAppliance.vb -** Models the health and safety related characteristics of a combustion appliance.

**HealthSafetyApplianceList.vb -** A list class for holding a set of *HealthSafetyAppliance* objects.

**Heater.vb -** Models one of the space heating systems in the home. Calculates the efficiency of the heating system through use of the *Calculate()* method.

**Heater\_out.vb -** Holds calculated or Energy Library look-up values associated with a space heating system. These are stored in an object so that they can be archived in the AkWarm file.

**Home.vb -** The parent class that contains a *HomeInputs* object for storing inputs, a *EnergyResults* object for storing energy calculation results, a *BEESratingResults* object for storing Rating results, and a *ImprovementResults* object for storing results of the improvement analysis.

**HomeInputs.vb -** The class that stores all of the inputs related to the home being analyzed.

**HtrDistribution.vb -** Models a space heating distribution system (forced air, hydronic, direct-to-space). The *Calculate()* method calculates the efficiency of that distribution system.

**HtrUpgradeDevice.vb -** Models a possible upgrade device (vent damper, modulating aquastat, flame retention burner) to a space heating system.

**IECCrating.vb -** Class that compares the energy use of the home being analyzed to a an IECC 2004 Supplement Reference home. Used to determine if home qualifies for the federal Homebuilder Tax Credit (50% of IECC 2004 energy use). The method that performs the rating is *Rate()*.

**Improvement.vb -** This class is used to analyze one improvement. It is a temporary class used during analysis, but it is not retained in the AkWarm file. Note: see the Commercial improvement analysis approach for a cleaner way to perform the improvements analysis.

**ImprovementAnalyzer.vb -** The class that performs the analysis of all efficiency improvements. The method that starts the analysis is *AnalyzeImprovements().*

**ImprovementResults.vb -** Stores the results of the improvements analysis. Summary values for all improvements and for just cost-effective improvements are given. Specific details are given for each improvement analyzed as well.

**OldFileDefs.vb -** This class is used to read AkWarm Version 1 files, which end in the file extension “.hom”. Old files cannot be saved in the old file format; they must be saved to the new “.hm2” file format.

**Project.vb -** This class is the root object in the residential object model. It contains the home description and calculated results, as well as AkWarm version information and various flags. For example, one flag indicates whether the file is an “Official” file (a file saved using an official rater password).

**RaterInfo.vb -** Class to describe an Energy Rater or User of the software, storing name, company, etc.

**Setpoint.vb -** Describes a heating or cooling temperature setpoint, including any setback (setup for cooling) and any proposed setback thermostat improvement option.

**SpaceHeaterList.vb -** A list-type class that holds the two (Primary and Secondary) *Heater* space heating system objects. The list is capable of holding more than two space heaters, but only two are used currently.

**SummaryByEndUse.vb -** A class that holds one numeric value for each residential end use. The value can any number such as energy use or energy cost.

**ThermalDistribution.vb -** Models a thermal distribution system used to deliver space heating or space cooling. This model is patterned after the IECC 2004 Supplement way of characterizing a distribution system. It is being used for modeling the distribution system for the space cooling system in AkWarm. The distribution system for the space heating system is still being modeled through the original AkWarm approach (see the *HtrDistribution* class). This *ThermalDistribution* class is also used to model both space heating and cooling distribution systems for the purposes of IECC 2004 modeling. See the *IECCrating* class.

**UserFuelPrice.vb -** (Deprecated) Old method of storing user-entered fuel prices. See the *FuelPrices* and *FuelPriceEntry* classes for the current approach to storing user-entered fuel prices. This deprecated class is still needed for reading old AkWarm files.

**VentilationSystem.vb -** Models the home’s mechanical ventilation system, if present.


<a name="residential_lights"></a>
### Residential Lights and Appliances

The following classes are used to model ‘itemized’ inputs for residential lights and appliances to support more detailed analysis of energy use and improvement benefits. For the ‘old style’ basic lights and appliances analysis, the inputs are contained in the HomeInputs object and analysis is contained in the EnergyCalc object.

**ResidentialLightsAndAppliances/LightOrAppliance.vb** - Class containing information describing one or more identical residential lights or appliances.

**ResidentialLightsAndAppliances/LightOrApplianceConsumption.vb** - Base class for consumption information for a residential light or appliance. Must be inherited.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionByRate.vb** - Consumption information for a light or appliance where the instantaneous consumption rate is known. Inherits from LightOrApplianceConsumption.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionPerTimePeriod.vb** - Consumption information for a light or appliance where the consumption over an extended time period is known. Inherits from LightOrApplianceConsumption.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionPerUse.vb** - Consumption information for a light or appliance where the usage is cyclical and the consumption per use is known. Inherits from LightOrApplianceConsumption.

**ResidentialLightsAndAppliances/LightOrApplianceImpRec.vb** - This class provides an EnergyLibrary style improvement record for a light or appliance improvement as required by the Improvement analyzer. This information does not come from the database, instead information is hard-coded or passed into the constructor of this class. This class mimics the structure of other Energy Library classes associated with improvements.

**ResidentialLightsAndAppliances/LightOrAppliancePrePost.vb** - Class containing pre and post retrofit versions of a light or appliance. Also contains improvement costs.

**ResidentialLightsAndAppliances/LightsAndAppliancesList.vb** - List of LightOrAppliancePrePost objects.


<a name="shell_components"></a>
### Shell Components and Related

The following classes used to model shell components are used by both Residential and Commercial AkWarm.

**Shell/AreaCalculatorShape.vb -** Stores and calculates areas for shapes used in the Area Calculator form.

**Shell/AreaCalculatorShapeSegment.vb -** Models one border segment in the *AreaCalculatorShape*.

**Shell/FrameCavity.vb -** A layer in a shell component consisting of framing members and a cavity between the members for insulation.

**Shell/InsulLayer.vb -** A layer of insulation of a particular type and thickness.

**Shell/Section.vb -** One section of a shell component having a particular R-value and a fraction of the shell component occupied by this section. A shell component is modeled by a set of these sections.

**Shell/SectionList.vb -** A set of *Section* objects that together allow determination of the overall R-value of the component.

**Shell/ShellComponent.vb -** The base class for all the specific shell component types.

**Shell/ShellComponentList.vb -** A list class to hold all of the shell components of the home/building. Class methods provide a number of different calculated values for the set of shell components.

**Shell/ShellComponent\_out.vb -** Holds a number of calculated or lookup values associated with one shell component. These are stored in an object so that they appear in the AkWarm file for archive purposes.

**Shell/ShellInterfaces.vb -** A module that contains Visual Basic Interface definitions related to shell components. Currently holds an Interface that must be supported by shell components that have a Certified U-value user input, *ICertifiedUValueInfo*.

**Shell/Sh\_AboveFloor.vb -** Models an above-grade floor component.

**Shell/Sh\_AboveWall.vb -** Models an above-grade wall component.

**Shell/Sh\_BelowFloor.vb -** The base class for the two below-grade floor component classes below.

**Shell/Sh\_BelowFloorCenter.vb -** Models a below-grade floor component, center section. Inherits from *Sh\_BelowFloor.*

**Shell/Sh\_BelowFloorPerim.vb -** Models a below-grade floor component, perimeter section. Inherits from *Sh\_BelowFloor.*

**Shell/Sh\_BelowWall.vb -** Models a below-grade wall component, which can have an above-grade section as well.

**Shell/Sh\_CeilingAttic.vb -** Models an insulated ceiling component, with an attic above.

**Shell/Sh\_CeilingCathedral.vb -** Models a cathedral ceiling component. Inherits from *Sh\_CeilingAttic*.

**Shell/Sh\_ExternalDoor.vb -** Models an external entry door component (but not a garage door).

**Shell/Sh\_GarageDoor.vb -** Models a vehicle garage door component (not a man-size door).

**Shell/Sh\_Window.vb -** Models a window or skylight component.


<a name="energy_classes"></a>
### Energy Classes used by both Residential and Commercial

These are energy-related classes that are used in both Residential and Commercial AkWarm.

**CalcMonthlyFuelUse.vb -** Holds the AkWarm-calculated amount of fuel used in one month for a particular fuel type. Used in actual-versus-modeled fuel use comparisons.

**CalcMonthlyFuelUseList.vb -** List class to hold and provide convenience methods for all of the *CalcMonthlyFuelUse* objects.

**Calc Details/EfficiencyLevels.vb -** Contains a class and an interface used to implement the feature whether a user can select which efficiency levels AkWarm will consider when analyzing an improvement.

**EnergyUtil.vb -** Provides a large number of general energy-related calculations and data, such as lists of possible fuel types and fuel type characteristics, air film and air gap R-values, etc. This class also tracks and provides a reference to the Energy Library currently being used by the application (see the *EnergyLibrary()* method). AkWarm would be structurally improved if some of these methods were moved closer to the classes they relate to. For example, the air film R-value functions could be in a separate shell component utility class in the *Shell* folder. Also, some or all of the constants in this class could be moved to the Energy Library so that they could be more visible and changeable.

**FuelPrices.vb -** The list of fuel prices for the building, which may come from the Energy Library or from a user override entry. This file contains both the *FuelPrices* list class and the *FuelPriceEntry* class which holds one fuel price.

**FuelRecord.vb -** Holds twelve months of actual fuel usage data for one fuel type. This data is entered by the user and is used in actual-versus-modeled fuel use comparisons.

**FuelRecordList.vb -** A list class to hold all of the *FuelRecord* objects for the building.

**ImprovementInputs.vb -** The user inputs applicable to an efficiency improvement, including an ID identifying the particular improvement, any user-entered cost adjustments for the improvement, notes about the improvement, etc.

**ImprovementItemResults.vb -** Holds the cost/benefit and energy saving results for one improvement. This is the object stored in the AkWarm file to record details about one improvement.

**ImprovementItemResultsList.vb -** A list class containing all of the *ImprovementItemResults* objects.

**ImprovementTotals.vb -** Holds total costs and savings for a group of improvements. The two groups currently used in the program are *all* improvements and *cost-effective* improvements.

**LibraryUtil.vb -** Provides a number of utility methods that assist in working with Energy Libraries. Examples are *IsNewestLibrary()*, which indicates whether the library is the newest available on the computer for the currently operating version of AkWarm.

**SummaryByFuel.vb -** Stores one value for each different fuel type available in AkWarm. Used by the application for storing costs by fuel type and energy use by fuel type.

**SummaryByLoss.vb -** Stores one value for each different energy loss category (e.g. Floor, WallDoor). Used by the application for storing cost and loss values by loss category.

**SummaryListElementByFuel.vb -** Holds one *SummaryByFuel* object for a particular ID and Name identifier. Used to summarize fuel use by various residential lights and appliances categories. Not currently used in the Commercial software, but it the class has general applicability.

**ValidateLibraryValueAttribute.vb -** A data-validation attribute used to determine whether an primary key ID from an Energy Library table is valid or not. This class was not put in the DataAttributes project because the class references the Energy Library, and we did not want that sort of a dependency in the DataAttributes project.

**Weather.vb -** Class to calculate and provide the weather data for any given city, using data from the Energy Library. See the *New()* constructor method for the logic used to calculate the weather data.


<a name="commercial_energy"></a>
### Commercial Energy Related

**AirLeakage.vb -** Holds building air tightness inputs and calculates natural infiltration (see *CalculateInfiltration()* method).

**BldgSpace.vb -** Models a space within the building, describing occupancy and temperature setpoints in that space.

**BuildingSpaceList.vb -** List class to hold all of the *BldgSpace* objects.

**Building.vb -** Contains objects that hold the inputs describing the building, the calculated energy results, and the calculated results of the efficiency improvement analysis.

**BuildingInputs.vb -** Holds all of the user-inputs describing the building.

**EnergyCalcComm.vb** - The class that performs the annual energy use and the design heat loss calculations for the building. The main entry point is the *Calculate()* method.

**EnergyResultsComm.vb -** Stores the results of the annual energy use and design heat loss calculations performed by the *EnergyCalcComm* class. This object is stored in the AkWarm file.

**ImprovementAnalyzerComm.vb** - The class that performs the analysis of all efficiency improvements. The method that starts the analysis is *Calculate().*

**ImprovementResultsComm.vb** - Stores the results of the improvements analysis. Summary values for all improvements and for just cost-effective improvements are given. Specific details are given for each improvement analyzed as well.

**ProjectComm.vb** - This class is the root object in the residential object model. It contains the building description and calculated results, as well as AkWarm version information and various flags. For example, one flag indicates whether the file was recalculated after inputs were changed.

**SummaryByEndUseComm.vb -** A class that holds one numeric value for each commercial end use. The value can any number such as energy use or energy cost.

**Calc Details/BuildingEnergyUse.vb -** *EnergyCalcComm* stores its calculated energy results in an object of this class. This class then provides those raw results and also various processed summaries of the results by fuel type and/or end use.

**Calc Details/LoadInterfaces.vb -** A module that contains a number of Visual Basic Interfaces that are used in the energy calculation and improvement analysis process.

**Other End Uses/AnyFuelLoad.vb -** Base class for an energy-using load that could use any fuel type. Clothes Dryers and Cooking equipment are examples.

**Other End Uses/AnyFuelLoadList.vb -** List class to hold a set of *AnyFuelLoad* objects.

**Other End Uses/AnyFuelLoadPrePost.vb -** Class that holds an Existing and Proposed (Retrofit) set of *AnyFuelLoad*’s. The existing and proposed loads are each of the type *AnyFuelLoadList*. The description and costs of implementing the proposed retrofit are contained in the class as well.

**Other End Uses/ClothesDryer.vb -** Models a clothes dryer. Inherits from the *AnyFuelLoad* class.

**Other End Uses/CookingEquipment.vb -** Models a piece of cooking equipment. Inherits from the *AnyFuelLoad* class.


<a name="commercial_electric"></a>
### Commercial Electrical Loads

**Electrical Loads/AkWarmLoad.vb** - Class to hold pre and post improvement versions of an electrical load.

**Electrical Loads/AkWarmLoadImprovement.vb** - Class implementing IImprovement that represents a Controls, Power, or Combined improvement for an Electrical Load.

**Electrical Loads/AkWarmLoadsList.vb** - List class to hold AkWarmLoads.

**Electrical Loads/CycleLoad.vb** - Base class representing cyclical electrical loads where the power consumption per cycle is known. Inhertis from ElectricalLoad.

**Electrical Loads/ElectricalLoad.vb** - Base class for a commercial electrical load. This is inherited by CycleLoad and HourlyLoad.

**Electrical Loads/HourlyLoad.vb** - Base class representing electrical loads where the power consumption rate is known. Inhertis from ElectricalLoad and is inherited by LightingLoad, RefrigerationLoad and OtherHourlyLoad.

**Electrical Loads/LightingLoad.vb** - Class representing lighting loads. Inherits from HourlyLoad.

**Electrical Loads/LoadControlSavings.vb** - Class represents savings accrued from using a control on an electrical load. Instances of this class are used as properties on specific ElectricalLoads classes.

**Electrical Loads/OtherHourlyLoad.vb** - Class representing generic hourly loads. Inhertis from HourlyLoad.

**Electrical Loads/RefrigerationLoad.vb** - Class representing refrigeration loads. Inherits from HourlyLoad.


<a name="commercial_hvac"></a>
### Commercial HVAC Related

**HVAC/CoolingPlant.vb -** Models a cooling plant (chiller or air conditioner) and calculates the energy use of the plant given a set of monthly loads (see the *Calculate()* method).

**HVAC/CoolingPlantList.vb -** List class to hold a set of cooling plants.

**HVAC/DHWstorage.vb -** Models a domestic hot water storage tank. The *HourlyHeatLoss*() method calculates the heat loss from the tank.

**HVAC/DHWstorageList.vb -** List class for holding a set of *DHWstorage* tanks.

**HVAC/DHWsystem.vb -** Models a domestic hot water system consisting of zero or more storage tanks and possibly a system for recirculating hot water. Does not include the heating plant that supplies the heat to the domestic hot water.

**HVAC/Distribution.vb -** Models a thermal distribution system that takes heating and/or cooling from heating and/or cooling plants and delivers it to conditioned space. Includes the pumps and fans associated with that distribution system.

**HVAC/DistributionList.vb -** List class to hold a set of *Distribution* systems.

**HVAC/HeatPlant.vb -** Models one heating plant that converts fuel (counting electricity) into heat. See the *Calculate()* method for the calculation of the plant energy use. Does *not* model the thermal distribution system that delivers the heat to conditioned space.

**HVAC/HeatPlantList.vb -** List class to model a set of *HeatPlant*s.

**HVAC/HVACsystem.vb -** A class to contain the building’s heating plants (*HeatPlantList)*, cooling plants (*CoolPlantList)*, thermal distribution systems (*DistributionList)*, domestic hot water system (*DHWsystem).* Does *not* include the mechanical ventilation systems, which are stored separately.

**HVAC/HVACsystemPrePost.vb -** Contains the existing *HVACsystem*, a proposed (Retrofit) *HVACsystem*, and details about the costs involved with the retrofit.

**HVAC/PlantLoadPercent.vb -** Class to indicate the percent of a load served by a particular heating or cooling plant. Used to partition load across a set of heating or cooling plants.

**HVAC/PumpFan.vb -** Models a pump or a fan.

**HVAC/PumpFanList.vb -** List class to hold a set of pumps and/or fans.

**HVAC/Ventilation.vb -** Models a mechanical ventilation system for bringing outside air into a building.

**HVAC/VentilationList.vb -** List class to hold a set of *Ventilation* systems.

**HVAC/VentilationPrePost.vb -** Holds two sets of ventilation systems: an existing set and a proposed set. Also holds costs and information related to the retrofit of the proposed system.


<a name="commercial_usage"></a>
### Commercial Usage Scheduling Classes

The following classes support the definition of detailed usage schedules that are currently used for Building Spaces, Electrical Loads, AnyFuel Loads, Pumps, Fans and Ventilation. The schedules separate a year into ‘High’ and ‘Low’ use times.

**Scheduling/UsageDays.vb** - The ‘days of the week’ components of a schedule.

**Scheduling/UsageHighTimes.vb** - The ‘time of day’ compnenents of a schedule.

**Scheduling/UsageSchedule.vb** - The core schedule class. Describes whether a space or equipment is in "High Use" or "Low Use" mode for any particular date and time

**Scheduling/UsageSchedulesList.vb** - List class to hold multiple schedules.

**Scheduling/UsageSeason.vb** - The seasonal components of a schedule, defined by start and end dates. A special type of season, ‘All Remaining Dates’ represents any dates that are not specifically allocated to a different season.


<a name="data_structures"></a>
### General Purpose Data Structures

These classes are common to useable in both Residential and Commercial AkWarm. They are more general purpose data structures and are not specifically energy related.

**ArithExpression.vb -** Accepts an arithmetic expression entered by the user and calculates the resulting value. Various mathematical operators can be used in the expression. Used for area and length entries in AkWarm.

**Constants.vb -** Holds general purpose constants such as MISSING, which represents a missing value.

**ImageLink.vb -** Holds a file path link to an image or PDF file. Also holds notes about the image.

**ImageLinkList.vb -** List class to hold a set of *ImageLink*s.

**LookupTable.vb -** Allows creation of a lookup table (actually a VB Dictionary) from a simple string of key/value pairs.

**MonthArray.vb -** Stores a value for each month of the year and an annual value. Provides other convenience methods related to monthly values.

**MonthArrayDictionary.vb -** A Generic Dictionary where the Keys are of any specified type and the values are *MonthArray*’s.

**MonthArrayDictionary2Key.vb -** A two-key dictionary where Key1 and Key2 are of specified but potentially different types and the values are *MonthArray*’s.

**NameAddress.vb -** Holds a name, organization and address.

**SingleDictionary.vb -** A Generic Dictionary where the key is a specified type and the value is a Single precision floating point number.

**SingleDictionary2Key.vb -** A Generic Dictionary with two keys of specified but potentially different types and the values are Single precision floating point numbers.

**SmartObject.vb -** A souped-up Object type that is the base class for many classes in AkWarm. It has methods to support cloning, returning properties via their string name, returning an XML representation of the object, etc.

**ValueWithSource.vb -** A single-precision nullable floating point value that has a property that indicates the source of the value: Not Available, Estimated, or Measured.

**VersionInfo.vb -** Holds version information about the AkWarm application and the Energy Library being used.

**Calc Details/TypicalWeek.vb -** Holds a value for each hour of one week. AkWarm uses the class to specify hour load and energy use profiles. Currently only used in Commercial AkWarm where schedules are important.

**Calc Details/MonthArrayOfTypicalWeek.vb -** Contains a *TypicalWeek* object for each month of the year and an annual object as well. Currently only used in Commercial AkWarm.

**Calc Details/DictionaryOfMonthArrayOfTypicalWeek.vb -** A VB Dictionary with a key of a specified type and values that are *MonthArrayOfTypicalWeek*’s. Currently only used in Commercial AkWarm.

**Calc Details/Dictionary2KeyOfMonthArrayOfTypicalWeek.vb -** A VB dictionary with two keys of specified but possibly different types having values that *MonthArrayOfTypicalWeek*’s. Currently only used in Commercial AkWarm.