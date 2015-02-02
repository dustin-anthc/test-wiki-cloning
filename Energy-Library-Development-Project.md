- [Introduction](#introduction)
- [Energy Library File Details](#file_details)
- [Overview of Visual Basic Projects involving the Energy Library](#overview)
- [Releasing a New Energy Library](#release)
- [Adding a New Field or Table to the Energy Library](#add_new_field)
- [Notes on Editing Energy Library Data](#editing_notes)
	- [GENERAL INFORMATION](#general_info)
	- [GENERAL LIBRARIES](#general_libraries)
	- [BUILDING THERMAL COMPONENTS](#thermal_components)
	- [MECHANICAL SYSTEMS](#mechanical_systems)
	- [RECOMMENDED IMPROVEMENTS](#recommended_improvements)
	- [PROGRAM AND RATING LIBRARIES](#program_and_rating)

Introduction <a name="introduction"></a>
------------

The *Energy Library* is a database of information that the AkWarm application uses in a read-only fashion to performs its tasks. Examples of the information contained in the Energy Library are:

-   Weather Data for the Alaskan cities that AkWarm can model buildings in

-   Fuel Prices and Utility Rates by city

-   Types of insulations and their thermal characteristics

-   Possible energy-efficiency improvements and their costs and energy characteristics

This document describes the:

-   Energy Library file details

<!-- -->

-   Visual Basic Projects that primarily work with Energy Libraries

-   The process of updating and releasing a new Energy Library

-   The steps required to add a new field or table of information to the Energy Library to support a new AkWarm feature

-   Notes about editing and updating the Energy Library data

Energy Library File Details <a name="file_details"></a>
---------------------------

An Energy Library starts as a standard Microsoft Access database. The Microsoft Access format facilitates the editing and viewing of the data. There are actually two different MS Access databases involved when the data is being edited. One database holds the tables of data, but no forms for viewing and editing the data. As an example, the data for the May 18, 2012 release of the Energy Library is stored in an Access file named *2012-05-18.accdb.* The Access file that holds the forms to edit the data in *2012-05-18.accdb* is named *LibEdit.accdb.* The forms in *LibEdit.accdb* attach to the tables in *2012-05-18.accdb* to allow for access to that data. *LibEdit.accdb* does not change over time (unless the structure of the Energy Library changes), but each new release of the Energy Library results in a new database file, such as *2012-05-18.accdb,* holding the new Energy Library data.

The Microsoft Access database is not directly used by the AkWarm application. Instead the Access database is converted into a much smaller file, a file that contains a Visual Basic dictionary of lists; each list corresponds to a separate table in the MS Access database. That dictionary of lists is serialized into XML format, and the resulting XML file is compressed and lightly encrypted to become the final Energy Library file. For the example given in the prior paragraph, that final file is named *2012-05-18.lib.* The process of converting the MS Access file into this final *.lib* file is described in more detail later in this document.

An AkWarm installation on a user’s computer contains the most current Energy Library but also all prior Energy Library releases. These older libraries are kept available because it is often necessary to open an older AkWarm file that was created with an older Library version. AkWarm allows the user to work with that file using the original Library. Doing so helps ensure that the user can replicate the original calculated results that were produced when the file was first created.

Overview of Visual Basic Projects involving the Energy Library <a name="overview"></a>
--------------------------------------------------------------

There are a number of Visual Basic Projects that work with Energy Libraries. Following is the list, with a brief description of each. These projects will be referenced later in this document.

The following two projects are part of the AkWarm application run by the users of AkWarm:

***AkWarmEnergyLibrary:*** This project contains classes that open from disk and make available the information held in the Energy Library.

***AkWarmEnergyLibraryEntities:*** This project contains a class for each table in the Energy Library, describing the properties (fields) of the rows in the table. Also, some of the classes have business logic added through partial classes to further manipulate the data in the tables (see the classes in the BusinessObjects folder).

The following three projects are used to convert the MS Access Energy Library file into the *.lib* file used by the AkWarm application. These projects can also create the XML version of the Energy Library file, which can be read by many other software tools. These projects are only used by developers, not end users of the application.

***EnergyLibraryMaintenance:*** This project creates the command line utility that is used to convert the Energy Library from Microsoft Access to the format used by AkWarm. Conversion to XML format is also possible with the utility. A document with the title “EnergyLibraryMaintenance (elmaint)” and file name “Help\_EnergyLibraryMaintenance.pdf” gives detailed instructions for use of the command line utility.
***Important Compilation Note**:* You need to compile the *EnergyLibraryMaintenance* application for x86 processors. Otherwise, you will receive the error: "microsoft.ace.oledb.12.0 provider is not registered". Use the Build, Configuration Manager, to set to "x86" Platform, instead of the normal “Any CPU” Platform. Also, some DLLs will not be built with the Configuration set to “x86”. They appear unchecked in the Configuration Manager dialog. Force the building of those DLLs with the “Any CPU” setting by setting the checkboxes. Otherwise running the elmaint.exe command without those DLLs causes a missing DLL error.

***EnergyLibraryMaintenanceCommands:*** This project is used by the *EnergyLibraryMaintanence* project and implements the specific commands available in the command line utility.

***Command Interface:*** This project is used by the *EnergyLibraryMaintanence* project and holds a Visual Basic Interface that must be supported by each command supported by the command line utility.

The ***LibraryTester*** project creates a small GUI application that performs some simple data validity checks on an Energy Library. These tests are used to review and identify data entry errors in an Energy Library before releasing the library.

Releasing a New Energy Library <a name="release"></a>
------------------------------

New versions of the Energy Library are released as information in the library is updated. Fuel price changes are generally updated in the Library every six months, so a new library release occurs at least that often. Energy Libraries are installed when the AkWarm application is installed. However, new Energy Libraries can also be installed independently and automatically through a Web update process. The steps below outline the process of releasing a new Energy Library.

1.  Editing of the data itself occurs in the Microsoft Access version of the Energy Library. Generally, a new version of the Library starts with a copy of the last released version. For example, if the last released version was *2012-04-06.lib*, make a copy of the associated *2012-04-06.accdb* Microsoft Access database to start the new Library release with. If your chosen version date for the new library is 2012-05-18, rename the Access file to *2012-05-18.accdb* and move it to an empty folder. Also copy the *LibEdit.accdb* file to that folder.

2.  When you open the *LibEdit.accdb* file, it will automatically find and attach to the data tables in the *2012-05-18.accdb* file (make sure to enable macro content when you open the file). The Main Menu form will appear in the *LibEdit* file. Start by clicking the “Miscellaneous Info” button and change the “Library Version” field to “18-May-12” in the data entry form.

3.  The buttons on the Main Menu open simple editing forms for editing the data in the Energy Library. See the section later in this document titled “Notes on Editing Library Data” for additional information about editing the Library data.

4.  After editing of the Energy Library data has been completed in the Microsoft Access file, the Access file *2012-05-18.accdb* needs to be converted into the *.lib* format. (The *LibEdit.accdb* is only used for editing data and is not needed from this point onward). The command line utility produced by the *EnergyLibraryMaintenance* Project is used for this purpose. The filename for the command line utility is called *elmaint.exe*, and it can be found in the source code tree at *EnergyLibraryMaintenance\\bin\\x86\\Release\\elmaint.exe*. If the file is not present, then the *EnergyLibraryMaintenance* project needs to be built. To do so, set the *EnergyLibraryMaintenance* project as the Visual Studio StartUp project, set the Build Configuration to “Release”, and as noted before, the Active Solution Platform should be set to “x86”. Building the project should create the *elmaint.exe* file in the above listed location.

5.  Detailed instructions on use of the *elmaint.exe* utility are given in the *Help\_EnergyLibraryMaintenance.pdf* document, but the command needed for conversion of the Access file into a *.lib* file is:
    elmaint.exe Convert /source:2012-05-18.accdb /destination:2012-05-18.lib /encrypt
    The above syntax is correct if the Access file is located in the same folder as the elmaint.exe utility; if the file is in a different folder, substitute the full path name to the file in the above command.

6.  The *2012-05-18.lib* file can now be installed in the AkWarm solution by copying the file to the *AkWarmEnergyLibrary\\LibraryFiles* folder in the source code tree. The file then needs to be added to the *AkWarmEnergyLibrary* Visual Studio project by right-clicking on the *LibraryFiles* folder in that Visual Studio project and selecting *Add, Existing Item...* Then select the new *2012-05-18.lib* file in the file dialog. The file is now added to the Project, however two Visual Studio properties need to be set on the file: “Build Action” should be set to “Content”, and “Copy to Output Directory” should be set to “Copy Always”.

7.  When AkWarm is now run from the Visual Studio environment, the new library file should appear as the currently library file used by AkWarm. The library file should be tested with a number of different AkWarm files to ensure validity.
    *Important Note:* If you find a problem with the new Library file and it needs to be replaced or deleted, you must delete the Library file from the source code tree *and also* delete the Library file from the Application data folder, which is given by the special .NET variable *My.Computer.FileSystem.SpecialDirectories.CurrentUserApplicationData.* When the AkWarm application is run, all installed Library files are copied to this directory by the program, and it becomes the working Library directory for the application. (See the *AkWarmCalc.LibraryUtil.EnergyLibraryList()* method for more details.) An example full path of this directory is *C:\\Users\\Alan\\AppData\\Roaming\\Alaska Housing Finance Corporation\\AKWarm\\2.2.0.3\\LibraryFiles*. If the Library file is not deleted from this directory, it will continue to be active, and a new Library file of the same name will not overwrite it.

8.  As well as testing the new Library with actual AkWarm files, a small application is available that performs other tests of the Library data. That application is built by the *LibraryTester* Visual Studio project. After running the application, a GUI Form appears; start by selecting an Energy Library to test by clicking the “Open Energy Library” button. Three diagnostic tests can be done on the opened Library:

    1.  A test to determine whether certain data values fall outside of normal ranges. This test is initiated by the “Attribute-Based Tests” button. The tests are established by validation Attributes applied in the *EnergyLibraryEntities* project. See the *EnergyLibraryEntitites.City\_Logic.ValidateData()* routine for an example. Many of the records that fail this test are still valid but worthy of a check to determine whether data was entered properly.

    2.  A test that displays the Library records having the lowest and highest data values for a variety of tables. Sometimes those records are high or low due to data entry errors. The test is initiated by the “High / Low Tests” button.

    3.  A test that allows you to compare the current library against a prior library and identify the cities where fuel prices changed by more than a threshold amount (currently set to a 25% increase or a 20% decrease). The test is initiated by the “Fuel Price Changes” button.

9.  The new Library file needs to be posted to the Web server so it will automatically install on User’s computers (even if they do not install a new AkWarm release). The steps for posting the Library file to the web are:

    1.  Upload the *.lib* file to the proper folder on the web server, as indicated in the *AkWarm\_UI.MDImain.CheckForAkWarmUpdates()* method; the URL of that folder is currently *http://www.analysisnorth.com/AkWarm/update\_combined/*, but can be changed in the AkWarm code.

    2.  The “Library\_Info.txt” file located on the web server should be updated to include a new Energy Library. See the *AkWarm\_UI.MDImain.CheckForAkWarmUpdates() and the AkWarmCalc.LibraryUtil.CheckForUpdates()* methods for the URL of the file (currently *analysisnorth.com/AkWarm/update\_combined/Library\_Info.txt*) and other details. A sample of this file is:
        \#FILENAME MIN\_AKWARM\_VERSION
        \#-------------------------------------------------
        2009-02-09.lib 2.0
        2009-03-13.lib 2.0
        2009-04-10.lib 2.0
        2009-09-05.lib 2.0
        2010-03-24.lib 2.0
        2009-11-01.lib DELETED
        2011-02-21.lib 2.0
        2011-06-05.lib 2.1
        2011-08-25.lib 2.1.2
        2011-12-07.lib 2.1.3
        2012-02-02.lib 2.1.4
        2012-03-01.lib 2.1.4
        2012-04-06.lib 2.2.0
        2012-05-18.lib 2.2.0
        This file lists each AkWarm library file and also gives the minimum version number that that Library file is compatible with (for users running older versions, the Library will not be automatically downloaded and installed). If the minimum version number is entered as “DELETED”, the Library file will automatically be deleted from users computers; this feature is available to remove Library files that were found to be defective after release.

Adding a New Field or Table to the Energy Library <a name="add_new_field"></a>
-------------------------------------------------

If changes to the AkWarm application code require that a new field be added to an Energy Library table or perhaps an entire new table needs to be added, this section describes the steps required to make those structural modifications to the Energy Library. If a new field needs to be added, the steps are:

1.  In the MS Access database holding the Library data (for example, the *2012-05-18.accdb* file), use the Access Table Design tools to add the field to the appropriate table in the database.

2.  In that same Access database, there is a special table named *EnergyLibraryObjectFieldMapping*. In that table, a new record should be added that lists the new field. The fields in that table have the following meanings:

    1.  **ObjectType**: In the AkWarm Visual Basic application, each Library table maps to a Class. In this field, enter the name of the AkWarm class associated with the table where the new field was added. Generally, but not always, the name of the Class in the Visual Basic Application is the same as the name of the Table. The special table, *EnergyLibraryObjectTypeMapping*, give the mapping between Access table names and Visual Basic class names.

    2.  **AttributeName:** Just as each Library table maps to Class in the Visual Basic application, each field in the table maps to a Property of that class. In the *AttributeName* field*,* enter the name of the desired class Property for this new field (often the same name as the field in the Access table).

    3.  **FieldName:** This is the name of the new field added to the Microsoft Access table.

    4.  **DataTypeName:** This is a string identifying the data type of the new field. These strings should be Visual Basic data type names, except use the string “Int16” for a Visual Basic “Short” type and use “Int32” for a Visual Basic “Integer” type.

    5.  **IsNullable:** Set this Boolean field to True if the field can legitimately contain a Null value.

3.  In the Visual Studio *EnergyLibraryEntities* project, find the class associated with the Access table where the field was added. In that class, add a new Property with the name used in the **AttributeName** field described above and having a Data Type as indicated by the **DataTypeName** field described above. If you set **IsNullable** to True, make sure the data type used is nullable, such as *Nullable(Of Single)*. Add a suitable backer variable to retain the contents of the property. At this point, the new field will be available in objects returned by the *AkWarmEnergyLibrary* methods.

If you need to add an entire new Table to the Energy Library, these are the steps required:

1.  In the MS Access database holding the Library data (for example, the *2012-05-18.accdb* file), use the Create menu option to create a new table and use the Table Design tools to add the necessary fields to the table.

2.  In that same Access database, there is a special table named *EnergyLibraryObjectTypeMapping*. In that table, a new record should be added that lists the new table. The fields in that table have the following meanings:

    1.  **ObjectType:** For each table in the Access database, there is an associated class in the Visual Basic AkWarm application. In this field, enter the name of the associated Class in the VB application. The name of that class is often the same as the name of the Access table, but that equality is not required.

    2.  **TableName:** This is the name of the new table in the Access database.

    3.  **IDFieldName:** This is the name of a numeric field in the table that uniquely identifies each record; usually the name “ID” is used for this field.

    4.  **NameFieldName:** This is the name of a field in the table that is used to display a name to the AkWarm user if the table supplies choices for an AkWarm input; usually the field name “Name” is used for this.

    5.  **DescriptionFieldName:** This is the name of a field in the table that provides a more lengthy description of the record.

    6.  **IsTestObjectFieldName:** If there is a field in the table that identifies a record as being a Test record (and not a record to be used by the AkWarm application), enter the field name here. This entry is optional.

3.  For each field in the new table, a record in the *EnergyLibraryObjectFieldMapping* table must be created. Refer back to the prior list of steps for the meanings of each field in the that table.

4.  In the Visual Basic AkWarm application, a new Partial Class must be added to the *EnergyLibraryEntities* project in the *DataObjects* folder. The Class must inherit *EnergyLibraryObject* and be named with the name given in the **ObjectType** field above. Each field in the Access Table should have a corresponding property in the class, with names and data types according to the entries in the *EnergyLibraryObjectFieldMapping* table. After this step, the new table should be ready to use in the AkWarm application via *AkWarmEnergyLibrary* methods.

Notes on Editing Energy Library Data <a name="editing_notes"></a>
------------------------------------

### GENERAL INFORMATION <a name="general_info"></a>

All entries are made in *Form* or *Datasheet* view of the file “libedit.accdb”. The “libedit.accdb” file must always remain in the same folder location as the actual xxxx.accdb library file.

Every library has a few common entries:

-   **Name**: The description of the component as it will appear on the user’s screen and on the written report. Older versions were limited in the length of the description, but current versions allow for some more detail.

-   **Active** (Yes/No): **Once a component has been saved as part of the AkWarm Energy Library it should never be deleted.** If it is no longer being used in the program, it can be marked as “inactive” so that it won’t appear on the user’s screen as an option. It can still be resurrected if an AkWarm file that has used it in the past is reopened.

-   **Presentation Order**: This is the order in which the names of the components in any particular library will be displayed on the user’s screen. It is helpful to set these values in spacings of tens or more, so that future entries can be sandwiched in where they belong.

-   **Notes**: It is very important to use the Notes section to describe any relevant information about the listing: references used for descriptions, dates information changed, assumptions made, etc. Notes are included on every form or table listing.

Information specific to each library is described below.

### GENERAL LIBRARIES <a name="general_libraries"></a>

**1. CITY**

There are 286 communities listed in the City library.

-   Each is assigned an Energy Rated Homes (ERH) region and a Weatherization Program (WX) region by AHFC.

-   Each is also assigned a range on an *Improvements Costs scale*, for use in determining labor and material costs of recommended improvements. This is based on the community’s general position in relation to lowest prices (Anchorage and other easily accessible locations) and highest (where both materials and labor must be flown in.

-   **Special Hydro City** (Yes/No) Communities where the electricity is generated completely or nearly completely by hydropower. AHFC determines whether or not a community is designated a Special Hydro community.

-   **City and Borough Sales Tax** is updated from the State of Alaska Dept. of Commerce website:[ ](http://www.commerce.state.ak.us)[*http*](http://www.commerce.state.ak.us)[*://*](http://www.commerce.state.ak.us)[*www*](http://www.commerce.state.ak.us)[*.*](http://www.commerce.state.ak.us)[*commerce*](http://www.commerce.state.ak.us)[*.*](http://www.commerce.state.ak.us)[*state*](http://www.commerce.state.ak.us)[*.*](http://www.commerce.state.ak.us)[*ak*](http://www.commerce.state.ak.us)[*.*](http://www.commerce.state.ak.us)[*us*](http://www.commerce.state.ak.us)

-   **Weather City:** There are 22 communities in the Weather Library (described below) for which we have detailed weather data including monthly averages for wind, solar and temperatures. All other communities are assigned one of these “weather cities” that is closest in location.

    -   **If this community is one of the 22 “weather cities” that are part of the Weather Library, do not enter any data in any of the fields described below on the City screen.**

    -   If any of the values below are entered for a city, AkWarm makes adjustments to the weather data in the associated main weather city to make the data more appropriate for this community:

        -   Base 65 F Heating Degree Days

        -   Average Annual Temperature (dry bulb) (deg F)

        -   Heating Design Temperature (deg F) (To be precise, the outdoor design temperature is usually defined as the temperature that is equaled or exceeded for 97.5% of the time during the three coldest months of the year. Other sources define the outdoor design temperature as the temperature that is equaled or exceeded for 99% of the year. Design temperatures for many locations can be found in Chapter 24 of *ASHRAE Fundamentals*. Design temperatures for U.S. locations are[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*posted*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*online*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*by*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*the*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*International*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*Code*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[ ](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf)[*Council*](http://www2.iccsafe.org/states/virginia/Plumbing/PDFs/Appendix%20D_Degree%20Day%20and%20Design%20Temperatures.pdf); the design temperatures for ACCA's Manual J are posted at[ ](http://www.energystar.gov)[*www*](http://www.energystar.gov)[*.*](http://www.energystar.gov)[*energystar*](http://www.energystar.gov)[*.*](http://www.energystar.gov)[*gov*](http://www.energystar.gov).

        -   Average Annual Wind Speed – miles/hr

        -   Elevation above sea level (feet)

<!-- -->

-   **Utility**: All electric and gas utilities that are associated with this community must be connected to the community by selecting them from the drop-down list. This list is made up of all of the utilities described in the **Utility Library** (described below.) If there is no electric utility associated with a particular community, select “Self-generated Electricity” from the drop-down box.

<!-- -->

-   **Fuel Prices (Residential Rates)**

    -   **\#1 and \#2 Heating Oil:** This information is updated semi-annually, in July and January, via a phone/fax/e-mail survey to vendors in each community. Prices vary by vendor, quantity purchased, whether delivered or not; the survey asks for price per gallon for 300 gallons delivered as a starting point and then if that isn’t available, what is the most common customer. This *does* include sales tax until changes to AkWarm are made to automatically include the sales tax. Since it is not always possible to obtain updated information from each community twice a year, an effort is made to purge cost data that is more than one year old. **Propane:** price per gallon based on 100 lb bottle or price per gallon delivered

    -   **Birch wood, Spruce Wood: price per cord –** isn’t often updated because it is difficult to find. In remote communities people get their own and in urban areas firewood is usually a backup heating source

    -   **Note:** If the library does not contain a current price for fuel prices in a particular community, the user is asked to supply the information before AkWarm can perform final calculations.

<!-- -->

-   **Zip Codes:** list all available zip codes for the community. This list has changed over time as smaller communities either get their own post office or lose it.

**2. FUEL ESCALATION FACTORS**

Fuel and Maintenance Escalation Factors are projected out 30 years from the base year. These values are obtained from U.S. Department of Commerce “Energy Price Indices and Discount Factors for Life-Cycle Cost Analysis”, an annual supplement to NIST Handbook 135 and NBS Special Publication 709. The publication is intended to be effective for an annual span of April through March, but is sometimes not even published until September of the year in effect. It can be downloaded from the US DOE website:[ ](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*http*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*://*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*www*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*1.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*eere*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*energy*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*gov*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*/*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*femp*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*/*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*program*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*/*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*lifecycle*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*html*](http://www1.eere.energy.gov/femp/program/lifecycle.html).

“Table Ca-4. Projected fuel price indices (excluding general inflation) by end-use sector and fuel type for Census Region 4” contains the information to be entered in AkWarm’s library. Use Residential values for electricity, distillate oil (\#1 and \#2), LPG (propane), and natural gas, and the values for Coal from the Commercial category. Sometimes the factors from this table need to be adjusted so that the current year is considered to be a factor of 1.00, and future years are referenced to that value. See Alan’s spreadsheet “Fuel Price Escalation Factors.xls” for an example of this adjustment.

**3. UTILITIES**

Electric and natural gas prices are updated semi-annually, along with the fuel prices. The Utility library includes the names of each recognized electric and natural gas utility in the state, and is tied to the list of communities in the Cities Library. *When a new utility is added to the Utility library, it needs to be added to the list of utilities for each community it serves in the Cities library, in order for it to show up on the AkWarm user’s screen.*

For most utilities, price updates are acquired from their own websites. Usually the base rates are in effect for a full year and are set in either January or July. The *cost of fuel adjustment* may change monthly or quarterly, but AkWarm does not get that detailed.

**CO2 Produced**: This value has not been updated since the inception of the program. It requires determining, for each utility, the percentage of electricity produced from natural gas, fuel oil or renewable (hydro, wind) methods and then assigning a CO2 value to each of those sources and coming up with a combined average CO2 pounds per kWh. This value is a required entry and cannot be left blank.

**RCC Charge (Yes/No)**

The Regulatory Cost Charge (RCC) is a special surcharge applied to all regulated retail customer billings to pay the utility’s share of the Regulatory Commission of Alaska (RCA) expenses**. **

There are also utilities that are not RCA regulated; these include local, government-owned utilities, very small utilities, and cooperatives whose members have voted to become deregulated.

The Regulatory Commission of Alaska maintains a list of all regulated utilities on their website:[ ](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*http*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*://*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*rca*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*.*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*alaska*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*.*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*gov*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*/*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*RCAWeb*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*/*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*RCALibrary*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*/*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*RCAReports*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*.*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx)[*aspx*](http://rca.alaska.gov/RCAWeb/RCALibrary/RCAReports.aspx).

In the case of a regulated electric utility, the amount billed to customers is the RCC per kilowatt-hour times the number of kilowatt-hours billed; in the case of regulated natural gas utilities, the amount billed to customers is a regulatory cost charge rate times the amount billed for all services that month. (The RCC is updated annually in the Miscellaneous Information library, described below.)

**PCE (Power Cost Equalization Credit)** The PCE fund was established to equalize the power cost per kilowatt hour statewide at a cost close to or equal to the mean of the cost per kilowatt hour in Anchorage, Fairbanks, and Juneau by paying money from the fund to eligible electric utilities. An eligible electric utility is entitled to receive PCE for sales of power to local community facilities and for actual consumption of not more than 500 kilowatt-hours per month sold to each residential customer (this 500 kWh/month limit is changeable in the ***Miscellaneous Information*** library table). A PCE credit is applied to the bills of residential and community facilities of eligible electric utilities.

PCE rates are provided by request, from the Alaska Energy Authority (AEA). At present their spreadsheets include a base price for electricity charged by each utility and the most recent PCE rate that they have received. The PCE rates may change each month, based on the price of fuel, but we don’t have the ability to maintain a cumulative average, so use the most current monthly rate provided by AEA. Several larger utilities that service a number of small communities have determined a more consistent PCE rate and AkWarm uses their rate schedules instead of the AEA spreadsheets. These include Alaska Village Electric Cooperative (AVEC) and Alaska Power and Telephone (APT).

The Legislature established different functions for AEA and the Regulatory Commission of Alaska (RCA) under Alaska Statutes 42.45.100-170, which govern PCE program responsibilities:

-   AEA determines eligibility of community facilities and residential customers and authorizes payment to the electric utility. *Commercial customers are not eligible to receive PCE credit*. Participating utilities are required to reduce each eligible customer’s bill by the amount that the State pays for PCE.

<!-- -->

-   RCA determines if a utility is eligible to participate in the program and calculates the amount of PCE per kWh payable to the utility.

**Customer Charge**: A fixed monthly charge that a utility may assess in addition to cost of power adjustment and energy charge. It is designed to cover the costs of operating the business.

**Fuel Surcharge:** an adjustment, per kilowatt-hour of sales, related to the fluctuations in the price of fuel bought to generate power.

**Purchased Energy Adjustment**: an adjustment, per kilowatt-hour of sales, that reflects fluctuations in the cost of purchased power. This may be a charge or a credit. Sometimes this is listed as *Cost of Power Adjustment Surcharge* or *Wholesale Power Cost Rate Adjustment* (WPCRA). These adjustments may change every quarter, but AkWarm uses whatever is current at the time of update.

Some utilities, such as Golden Valley Electric, combine Fuel Surcharge and Purchased Energy Adjustment into one category called “Fuel and Purchased Power”. As far as AkWarm is concerned it doesn’t matter which category it is included here – both are treated the same. These fields can be used to cover any recurring cost (per kWh of sales)that is in addition to the base energy charge per kWh.

**Base Rate**: the current effective energy charge or base rate that a utility charges for a kilowatt of energy. Many utilities have only one rate for this energy charge and others have different charges for different blocks of energy used. The form is set up to accommodate either. *It is important to remember to leave the “Maximum Use” entry blank for the highest block in the rate structure.* If, for instance, all electricity used is charged at the same rate, the “Maximum Use” field would be left blank. If there are 3 different blocks of usage, the first two would indicate the maximum kWh use at that rate, and the highest block would have no “Maximum Use” entered. For example, the City of Petersburg has a block rate structure for residential rates. Usage from 0 to 325 kWh/month is charged $0.118/kWh, usage from 326 – 650 kWh/month is charged $0.116/kWh and any usage above 650 kWh/month is charged $0.07/kWh. The correct entries in the library would be:

> Block 1 Maximum Use = 325 kWh, Rate = $0.118 / kWh
>
> Block 2 Maximum Use = 650 kWh, Rate = $0.116 / kWh
>
> Block 3 Maximum Use should be left blank, Rate = $0.070 / kWh

**These blocks are unrelated to PCE rates** which cover only the first 500 kWh used per month, where it is in effect. AkWarm internally calculates an estimated overall energy use and assigns PCE rates to the first 500 kWh used.

**4. WEATHER**

There are 22 communities in the Weather Library (described below) for which we have detailed weather data including monthly averages for wind, solar and temperatures. All other communities are assigned one of these “weather cities” based on proximity.

### BUILDING THERMAL COMPONENTS <a name="thermal_components"></a>

The AkWarm Energy Library contains six main libraries that provide information on thermal properties of the various components of the building shell. Each entry provides a default R-value (for insulation, framing, masonry, above grade walls) or U-value (*U*-*factor*) (windows, doors) for the available options on the user screens. While there may be a number of different values publically available to describe these materials, it is always recommended to use a standard reference, such as ASHRAE Fundamentals.

**5. WINDOWS**

The thermal effectiveness of windows is affected by the characteristics of both the window glass and frame selected. To determine default values for window U-factor/R-value, AkWarm has 3 sets of libraries:

-   **Window Glass –** describes any window glass options – this creates the drop-down menu for glass in the Window Combinations screen

-   **Window Frames –** describes any window frame options - this creates the drop-down menu for frames in the Window Combinations screen

-   **Window Combinations –** builds the desired window from the glass and frame options. The rate of heat loss is indicated in terms of the **U-value (*U*-*factor***) of the window assembly. U-value should be determined from current ASHRAE or NFRC tables, *not product literature*.

-   **The Make Window Combinations is only available to the programmer.** If a new window glass or frame type is added, the *Make Window Combinations* must be executed by the programmer to develop the new frame/glass combinations possible with the new entry.

**6. DOORS**

This library contains exterior entry doors as well as revolving doors, garage doors, and hangar doors. In order to maintain the on-screen organization of the options, it is important to follow the established description procedure under *Name*: Type of door, frame material, insulation type, thickness. Note that the thermal value asked for is U-value, not R-value. Use values vetted by ASHRAE, NFRC or other approved 3rd party testing method, not simply product literature.

**7. INSULATION**

This library includes almost any kind of insulating material that has been used in buildings in Alaska – including newspapers and wood shavings seen in earlier construction, and straw bales and bio-based products seen in innovative building construction today. Each entry is described as batt, loose-fill , and whether it can also be used as cavity and/or sheathing. Sheathing here is defined as an insulating material that is not inside the framing cavity, but attached to the outside/inside of the framing. It is important to follow the established procedure in describing insulation in the *Name* and *Presentation Order* fields, to maintain the on-screen organization of options for the user.

**8. FRAMING**

In the Framing Library, the width and thickness of each *lumber* component is provided. This information helps AkWarm determine, based on user input for area and stud spacing, how much of each wall, floor or ceiling component is composed of framing material rather than insulation material.

**9. MASONRY**

Some structural walls have no lumber framing, but are concrete –based. This library includes, concrete blocks, poured concrete and insulated concrete (concrete-filled foam). The R-value of each material described is all that is required.

**10. OTHER ABOVE GRADE WALLS**

This library is a catchall for all above grade walls that cannot be “built” by simply describing framing, insulation, and sheathing. Unlike those standard walls, the R-values for these walls are for **whole wall R-value (structural material and insulation).** This library currently includes concrete and brick walls, metal stud walls, and a value for a common wall in a multi-unit building. Metal stud walls are very difficult to model and most information comes from test lab data. Although there are many more possible types than those included here, we have not found a ready resource to provide us with reliable R-values for them.

### MECHANICAL SYSTEMS <a name="mechanical_systems"></a>

**11. SPACE HEATERS**

Space heating systems are described first by the type of fuel used to create the heat, then by the type of heating equipment (hydronic boiler, air furnace, space heater without distribution, heat pump), and then by the efficiency of the heating equipment. The efficiency measure used here is AFUE (Annual Fuel Utilization Efficiency). The *Steady State -AFUE Adjustment* is the difference between the steady state efficiency and the AFUE for the heater, described as a percentage. The *Auxiliary Power/Heat Output* is the ratio of auxiliary energy use to heat output, also described as a percentage.

Older heating equipment seen in the field may have already been retrofitted with any of several different pieces of equipment, depending on whether they are furnaces or boilers. The *Upgrade Device* section of the form lists the types of upgrades that will be available to the user and describes the effects on the efficiency of the heater when added to the system, in terms of part load losses and steady state efficiency. Someone familiar with the heating efficiency calculations inside AkWarm should determine these values.

**12. HOT WATER HEATERS**

Water heating systems are described first by the type of fuel used to create hot water, then by the type of water heater (tank or tankless), and then by the efficiency of the water heating equipment.

Water heating efficiency is described by its *Energy Factor* (EF) and is entered in the AkWarm library as a decimal fraction. EF = the Rated Energy Output/Total Energy Input. The EF test results are a combination of heating input efficiency and how efficient the tank is at storing heat. Heat loss through the tank varies depending on how well it is insulated. 4-14% of the energy used is lost because of imperfect insulation.

The *Recovery Efficiency* is the energy-to-hot-water conversion ratio.

-   For an electric water heater, the RE is 100%.

-   For gas water heaters the conversion rate is typically 76-78%, with expensive high efficiency units reaching 94%. This is because some energy must be left in the combustion byproducts to assure good venting.

This information is found on the yellow energy guide label on appliances.

The[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Directory**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**of**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Certified**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Product**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Performance**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**for**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Residential**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Water**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[ ](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH)[**Heaters**](http://cafs.ahrinet.org/gama_cafs/sdpsearch/search.jsp?table=RWH) is a searchable database provided by the Air Conditioning, Heating and Refrigeration Institute. It provides information on performance and efficiency of specific water heater models.

###  RECOMMENDED IMPROVEMENTS <a name="recommended_improvements"></a>

Any improvement measure that is to be analyzed by AkWarm must be included in one of the improvement libraries. There are four different improvement libraries, dealing individually with shell, space heating, domestic water heating and miscellaneous other improvements that are available for evaluation by AkWarm. While each library contains information specific to that component, they all require the same type of information:

-   **Improvement Description**: This is the description that will be printed on the improvements report so it is important to write it as a proper full sentence. Each description contains a place holder for the Level Description (see below). Use the tilde symbol (~) where the level description should be inserted.

-   **Life**: All improvements are evaluated for their cost-effectiveness over the life of the measure. In general, AkWarm uses industry standards for average life. This information may be found from US Department of Energy sites or from other online sites.

-   **Level**: When AkWarm evaluates the cost effectiveness of making improvements to specific building components, it considers not just the basic improvement but the various steps of efficiency that are possible. It then recommends the most cost effective level for that improvement measure. The program can only evaluate the specific levels that are included here. While there are many possible levels between the existing efficiency and 100% efficient, it is more prudent to consider the most common improvement levels available. Insulation improvements are limited by building structure; heating systems have standard default efficiency levels. The Level Description that is entered here is exactly what will be inserted into the Improvement Description where the tilde symbol is located, so make sure that it makes sense grammatically.

-   **Costs**: Since the improvement options are evaluated based on their initial cost versus their energy savings over the life of the measure, it is important to provide a price for each improvement measure described.

    -   **Low Cost/High Cost:** For each improvement described, it is necessary to provide an installed cost, including materials and labor. AkWarm asks for what that cost would be in the least expensive locations in Alaska, where materials and labor are readily available, and in the most expensive areas in Alaska, where materials and labor must be flown in. The low cost figures can be obtained from local vendors and contractors and the high cost figures are obtained from weatherization contractors who work in remote locations. They can also be obtained from insurance company adjusters. Once these low/high levels are established, AkWarm relates them to the *Improvements Costs Scale* found in the **City** Library, and interpolates those costs for communities located in middle ranges on the scale. Retrofit costs are very difficult to estimate over the wide range of buildings for which they may be recommended. These costs include only materials and labor to install the new measures, not costs for removing the existing component.

    -   **Do-It-Yourself Adjustment**: This adjustment removes the effect of labor costs. It is entered as a percent and is generally a negative number. A negative number means it costs less than the overall cost entered above.

    -   **Maintenance %:** Enter the annual maintenance cost as a percentage of the installed cost. Some improvements, such as increased insulation will have no maintenance costs, while others, such as heating systems, may have maintenance costs if they are more expensive to maintain than the system they typically replace.

**13. SHELL IMPROVEMENTS:** Describe as above, noting these specifics:

-   **Component Type:** Indicate which shell component this improvement is associated with.

-   **Add or Replace:** Insulation improvements may replace the existing material or they may be added to the existing material.

-   **Detailed Description**: List here the MS Word document (Snippet) that provides detailed information about the improvement and will be included in the printout for the client.

**14. SPACE HEATING REPLACEMENTS:** Describe each replacement option with the same information as used in Space Heating Library. Check for consistency between the two libraries.

**15. DHW REPLACEMENTS:** Describe each replacement option with the same information as used in DHW Library. Check for consistency between the two libraries.

**16. MISCELLANEOUS IMPROVEMENTS:** This catch-all library includes improvement options that are not related to specific shell, space heating or water heating components, but to overall building efficiency, such as a setback thermostat, or a ventilation system.

### PROGRAM AND RATING LIBRARIES <a name="program_and_rating"></a>

**17. MISCELLANEOUS INFORMATION**

**Library Version:** Every time a change is made to the energy library for import into the AkWarm program, this field should be updated with the change date.

**Discount Rate:** This value is updated annually with the fuel escalation factors and can be obtained from U.S. Department of Commerce “Energy Price Indices and Discount Factors for Life-Cycle Cost Analysis”, an annual supplement to NIST Handbook 135 and NBS Special Publication 709. The publication is intended to be effective for an annual span of April through March, but is sometimes not even published until September of the year in effect. It can be downloaded from the US DOE website:[ ](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*http*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*://*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*www*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*1.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*eere*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*energy*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*gov*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*/*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*femp*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*/*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*program*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*/*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*lifecycle*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*.*](http://www1.eere.energy.gov/femp/program/lifecycle.html)[*html*](http://www1.eere.energy.gov/femp/program/lifecycle.html).

**Gas Regulatory Surcharge (%) and Electricity Regulatory Surcharge ($/kWH):** The Regulatory Cost Charge (RCC) is a special surcharge applied to all regulated retail customer billings to pay the utility’s share of the Regulatory Commission of Alaska (RCA) expenses**.** The Regulatory Commission of Alaska provides this information on their website:[ ](http://rca.alaska.gov)[*http*](http://rca.alaska.gov)[*://*](http://rca.alaska.gov)[*rca*](http://rca.alaska.gov)[*.*](http://rca.alaska.gov)[*alaska*](http://rca.alaska.gov)[*.*](http://rca.alaska.gov)[*gov*](http://rca.alaska.gov), and it is included on most regulated utility rate schedules. Note the difference in calculation units: gas: %, electricity: $/kWh

**kWh Limit for PCE Subsidy:** Currently**,** an eligible electric utility is entitled to receive PCE for sales of power to local community facilities and for actual consumption of not more than 500 kilowatt-hours per month sold to each residential customer.

**Percent of Full Funding for PCE Program:** The Alaska State Legislature currently funds the PCE program at 100%. In some previous years, the AEA staff was required to monitor PCE disbursements vs. available funding and notify the RCA if they recognized that the current funds would not be sufficient for that fiscal year. The RCA would then recalculate everyone’s PCE levels at an appropriately reduced (“pro rata”) level to insure that the appropriations for that fiscal year were not exceeded. The last pro rata reduction was implemented in fiscal year 2007.

**18. RATING CALIBRATION**

The rating calibration screen includes a number of parameters that affect energy rating points. **Nothing on this screen should be changed without prior approval and direction from AHFC. All of the values have been determined or approved by AHFC staff.**

-   **BEES Point Level –** a home built to the current BEES requirements would receive 83 points in the AkWarm rating program

-   **Reference Home Points –** the reference building that AkWarm builds for comparison with the tested building would receive 85 points.

-   **Ratio of Best (100 pt) Energy Use to Reference Energy Use – Space Heating and Domestic Hot Water.** In some rating systems, a building that received a rating score of 100 points would be a net-zero energy building. Its energy needs are so greatly reduced that any that were required can be supplied by onsite renewable technologies. In Alaska it is not economically feasible to build a building that consumes no “bought” energy. AkWarm’s 100 point home would have space heating requirements equal to 0.2 of the requirements of the reference 85 point house, and the domestic hot water requirements would be equal to 0.6 of the requirements of the reference house.

-   **Point Boundaries Between Star Levels** -The spread of points at each star level is not the same at all levels. A building that receives up to 68 points is still a very poorly performing building.

-   **Site To Source Multipliers -** Energy measured at the building (*site*) is useful for understanding the performance of the building but it is not a good indicator of the environmental impacts from resource consumption. Site energy is also not a good metric for comparing buildings that use different energy types, buildings with on-site energy generation, or buildings with cogeneration systems. Analyses that use *source* energy consumption typically use a fixed multiplier or source energy factor to estimate the source energy consumed to generate electricity based on national averages. The multipliers used here are in line with those used in other programs nationwide.

-   **Region Rating Items –** uses BEES tables to assign default R-values for building components in each region.

**19. AVERAGE ERH POINTS BY REGION:** *This library should not be touched without prior approval and direction from AHFC.*

**20. PASSWORD LIST:** *This library should not be touched without prior approval and direction from AHFC.*

**21. TEST FOR DATA PROBLEMS - only available to the programmer.**

**22. PROGRAMMER MENU - only available to the programmer.**
