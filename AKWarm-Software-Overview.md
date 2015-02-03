-   [Introduction](#Introduction)
-   [User Interface](#user_interface)
-   [Application Data Storage and Storage to File](#data_storage)
-   [Energy Library](#energy_library)
-   [Calculations](#calculations)
-   [Reporting](#reporting)
-   [Web Server Functions](#web_server)
-   [Tasks Involved when Adding a New Input](#new_input)
-   [List of Visual Basic Projects and Associated Descriptions](#vb_projects)
    -   [Main AkWarm Application](#main_app)
    -   [AkWarm’s Setup/Installer Program](#installer)
    -   [Utilities to Create and Test Energy Libraries](#test_utilities)
-   [Developer Software Requirements](#developer_requirements)
-   [Developer Contact Information](#developer_contact)

Introduction <a name="Introduction"></a>
------------

The purpose of this document is to provide a general overview of the AkWarm software application so that a software developer can more easily maintain and enhance the application. The intended audience for this document is software developers.

AkWarm is a software application that has three main purposes:

1.  To provide a Home Energy Rating of an Alaskan residence. The AkWarm Energy Rating is approved by the Alaska Housing Finance Corporation and a number of other home financing institutions.

2.  To estimate the energy use and design heat load of Alaskan residences and small-to-medium size commercial buildings.

3.  To estimate the energy savings and financial characteristics of energy-efficiency improvements that are possible to apply to those residential and small/medium commercial buildings.

While this document provides a general overview of the application, there is more specific developer-oriented documentation available, including:

1.  Documents that describe in more detail most of the major Visual Basic projects found in the AkWarm solution.

2.  A document titled “Energy Library Developer Documentation” that gives details on data entry and file conversion procedures for the database that supplies read-only information to the AkWarm application.

3.  Approximately 20,000 lines of comments are embedded in the source code and provide detailed low-level documentation of the application.

The AkWarm application is written in the Visual Basic .NET programming language. The versions currently in use are Visual Basic 2008 for the programming language, .NET 3.5 for the .NET framework, and Visual Studio 2008 for the development environment. Software versioning and revision control software has been used since AkWarm 2.x development began in 2008. The revision control software currently used is SVN version 1.5.7. The current AkWarm version is 2.2.0.3.

The application consists of approximately 54,000 developer-written lines of code, not counting blank lines, comment lines, and code-generated lines. There are an additional 41,000 automatically-generated lines of code primarily associated with the Windows Forms user interface.

Previously, AkWarm was split into two separate applications: AkWarm-Residential and AkWarm-Commercial. In June of 2011, the Residential and Commercial programs were integrated into one application. There is some code shared between the Residential and Commercial components (e.g. Energy Library code, shell component description and analysis code) but the user interfaces and calculations are largely distinct.

The following sections describe the major components of the AkWarm application.

<a name="user_interface"></a> User Interface 
--------------

The user interface for AkWarm is a Multiple Document Interface (MDI) application utilizing Windows Forms. Multiple home and/or commercial building files can be open simultaneously. The open files need not be all of the same type (Residential or Commercial). The main project that holds the AkWarm user interface is the *AkWarm\_UI* project. The document describing that project is the next place to go for learning more details about the user interface development.

Windows Forms data binding is used to move the user-entered data on the input forms into the underlying object model that stores and processes the data. The data entry controls are often configured to limit the user input to acceptable values. For those controls that do not fully restrict user input, validation of the input data is implemented through a system of attributes attached to the properties of the objects in the underlying object model and specially-marked data validation routines. The data validation attribute system is contained in the *DataAttributes* project and is more thoroughly described in the documentation for that project.

Context-sensitive Help is available in the AkWarm application. The Help file is a Microsoft HTML Help file. The procedure for updating the file and linking topics to the AkWarm application is further described in the “AkWarm Help System” document.

<a name="data_storage"></a> Application Data Storage and Storage to File
--------------------------------------------

For one particular AkWarm analysis, which is either one residential building or one commercial building, the data for that analysis is stored in an object hierarchy (a root object containing other objects, which in turn contain objects, etc). For a residential analysis, the root object in the object model is of the type *Project,* a class found in the *AkWarmCalc* project. The hierarchy of objects starting with the root *Project* object describe the inputs to the residential home analysis and also hold a number of the calculated results. For an analysis of a commercial building, the root object is of the type *ProjectComm.* A similar hierarchy of objects is contained within that root object. Further details on the residential and commercial object models are found in the document describing the *AkwarmCalc* project.

When a user saves an AkWarm analysis to the user’s hard drive, each individual analysis occupies a separate file on disk. The application does *not* utilize a database system to store multiple AkWarm analyses within one database. AkWarm uses the .NET System.Xml.Serialization libraries to serialize the *Project* or *ProjectComm* object hierarchy into an XML document that is compressed and lightly encrypted before being stored on disk as an *.hm2* (residential) or *.hmc* (commercial) AkWarm file. See the *Project.SerializeToFile()* and *Project.ToByteArray()* methods for details on the serialization process.

<a name="energy_library"></a> Energy Library
--------------

The *Energy Library* is a database of information that the AkWarm application uses in a read-only fashion to performs its tasks. Examples of the information contained in the Energy Library are:

-   Weather Data for the Alaskan cities that AkWarm can model buildings in

-   Fuel Prices and Utility Rates by city

-   Types of Insulations and their thermal characteristics

-   Possible energy-efficiency improvements and their costs and energy characteristics

New versions of the Energy Library are released as information in the library is updated. Fuel price changes are generally updated in the Library every six months, so a new library release occurs at least that often. Energy Libraries are installed when the AkWarm application is installed. However, new Energy Libraries can also be installed independently and automatically through a Web update process described in a subsequent section.

An AkWarm installation on a user’s computer contains the most current Energy Library but also all prior Energy Library releases. These older libraries are kept available because it is often necessary to open an older AkWarm file that used an older Library version when it was created. AkWarm allows the user to work with that file using the original Library. Doing so helps ensure that the user can replicate the original calculated results that were produced when the file was first created. However, obtaining the original calculated results requires that the original Energy Library be used *and* that the original calculation algorithms be used as well. We have generally tried to maintain older calculation algorithms in the code so that they can be used with older files to maintain original results. As an example of maintaining both the old and new energy calculation algorithms, see the *AkWarmCalc.Sh\_BelowFloorCenter.UpdateTotalR(*) method, which selects between two versions of a below-grade heat loss algorithm depending on the age of the Energy Library being used in the analysis.

An Energy Library begins as a Microsoft Access database but is converted to a compressed and lightly-encrypted XML-serialized Visual Basic dictionary of generic lists for use with the AkWarm application. A separate document titled “AkWarm Energy Library” describes this process in more detail. Inside the AkWarm application, the *AkWarmEnergyLibrary* and *AkWarmEnergyLibraryEntities* projects contain the code that read and make available Energy Library information to the rest of the AkWarm application.

<a name="calculations"></a> Calculations
------------

As mentioned before, three different calculations are performed on a residential building--the energy use calculation, the home energy rating calculation, and the improvement analysis calculation. For commercial buildings, the same calculations are performed with the exception that the energy rating calculation is not performed. The calculations are initiated by the user clicking the “Calculate” button on the main input screen. The actual calculation code is found in the *AkWarmCalc* project. The energy use calculation is performed by the *Calculate()* method found in the *EnergyCalc* class for the residential analysis and the same-named method in the *EnergyCalcComm* class for the commercial analysis. Energy use is calculated on a monthly basis and includes space heating, space cooling, water heating, and lights and appliances energy use.

For the residential analysis, the Home Energy Rating calculation is performed by comparing the energy use of the residential building being analyzed against the energy use of a “reference” building built with components of a prescribed level of energy efficiency. That home energy rating calculation is performed by the *Rate()* method of the *BEESrating* class in the *AkWarmCalc* project. Because the rating process involves a comparison of energy use, the previously-described energy use calculation is used by and is of central importance to the rating calculation.

Both the residential and commercial modules analyze possible energy efficiency improvements to the building. The improvement analysis is performed by modeling the energy use of the building *without* the improvement applied and then modeling the building *with* the improvement applied. The difference in total energy use of the building between those two configurations is the energy savings attributable to the improvement. Because the *total* energy use of the building is used in the improvement savings calculation, the improvement’s impacts on all energy uses (space heating, space cooling, etc.) are accounted for.

Efficiency improvements interact with each other in the sense that the application of one improvement can affect the savings realized by a different improvement. For example, adding insulation to an attic saves more energy when the home uses an inefficient heating system than when the home uses an efficient heating system. Therefore, implementation of a heating system improvement will diminish the savings from an attic insulation improvement.

Because of the issue of interaction between improvements, an order of implementing improvements must be established. AkWarm applies improvements in order of cost-effectiveness, applying the most cost-effective measure first. If there are ten improvements to analyze, AkWarm analyzes all ten improvements to determine the most cost-effective improvement to apply. After determining that improvement and applying it to the building, AkWarm re-analyzes the remaining nine improvements (because interaction may have changed their cost-effectiveness) to determine the next most cost-effective improvement. This process continues until all of the improvements are applied. Because each improvement is re-analyzed many times, the analysis of improvements is clearly the most time-consuming portion of the AkWarm calculations. The number of energy calculations required goes up as the square of the number of improvements. Buildings with a large number of improvements can take a significant amount of time to calculate, particularly for commercial buildings where energy calculations are more computationally intensive.

The improvement analysis for the residential analysis is performed by the *AkWarmCalc.ImprovementAnalyzer.AnalyzeImprovements()* method. For the commercial analysis, the method is *AkWarmCalc.ImprovementAnalyzerComm.Calculate()*. The general structure for analyzing improvements for commercial buildings is much cleaner than the structure used in the older residential analysis, although both produce the same results. Code structure would be improved and would be more consistent if the residential improvement analysis code were restructured to match the commercial code.

After AkWarm performs the calculations above, some of the results of the calculations are stored in the object model so that those results are serialized into the AkWarm file. None of the calculated results *need* to be stored in the AkWarm file, since the calculated results can always be reproduced from the user input values, which are stored in the file. However, the data in the AkWarm file is ultimately loaded into the ARIS (Alaska Retrofit Information System) database, and the calculated results are essential for producing ARIS reports and analyses. A very large number of calculated values are available, and only the most important values are saved in the AkWarm file.

<a name="reporting"></a> Reporting
---------

A number of reports are available in AkWarm. The reports generally display calculated results, but there is also a report that summarizes all of the input values entered by the user. The report showing all of the inputs is available from the File menu in the application, but all of the other reports depend on calculated values and are therefore only available from the *Reports* tab on the output screen of AkWarm. The code used for reporting in AkWarm can be found in the *AkWarmReporting* project.

A number of different reporting technologies are used in AkWarm. The relatively low-level System.Drawing library is used to create the *Home Energy Rating* certificate because of the precise placement afforded by that library. The *Energy Features* and *Energy Flows* report also use that library. Other reports are created in Rich Text Format (RTF), for example the *Home Inputs* report. The most recent report, the *Design Heat Loss Report*, was created using HTML, which we hope to use for most future reports. Finally, reports that are customizable by the user are created as Microsoft Word documents using Word Automation. Examples are the residential *Improvement Options Report* and the commercial *Long Audit Report.* After those reports are created, the user is able to edit and augment the report by using standard Microsoft Word editing tools.

<a name="web_server"></a> Web Server Functions
--------------------

A web server is used to perform a number of important functions in AkWarm, including:

1.  Provide web pages where users can download the current version of AkWarm and view the change log for all versions of Akwarm.

2.  Provide a source code repository if multiple independent developers are working on the project.

3.  When a user initially starts AkWarm, the AkWarm application downloads a file from the web server that indicates the version number of the most current AkWarm release. If the user’s AkWarm version is older than that, a pop-up message alerts the user to the existence of a more recent version. For the code that performs this task, see *AkWarm\_UI.MDImain.CheckForAkWarmUpdates()*.

4.  When a user initially starts AkWarm, AkWarm checks to see if more recent Energy Library files are available from the web server. If so, AkWarm automatically downloads and installs those Library files. For the code that performs this task, see *AkWarm\_UI.MDImain.CheckForAkWarmUpdates()*.

5.  When unhandled errors occur in AkWarm, the user is given the option to upload a stack trace of the error message and the actual AkWarm file that triggered the error. That upload is posted to the web server. For the code that performs that task, see *AkWarm\_UI.ApplicationEvents.MyApplication\_UnhandledException()*.

The *analysisnorth.com* web server is currently used for the above purposes. However, changing a few URLs in the code would allow the use of any web server. The posting of unhandled exceptions does utilize a short CGI script on the web server. That script is currently written in the Python scripting language but could be rewritten in a different language if no Python support is available on the new web server.

<a name="new_input"></a> Tasks Involved when Adding a New Input
--------------------------------------

When a new user input value needs to be added to AkWarm, there are a number of tasks that must be completed. The list below summarizes those tasks:

1.  Add a visual input control to the user interface in the AkWarm\_UI project to accept the user’s input. Set the Tab Order setting to put the control in the proper position in the tab sequence.

2.  Add a property at the appropriate position in the Project or ProjectComm Object Model to hold the input data. Once a new property is established in the object model, it will automatically be included in the serialized AkWarm file. When older files are opened that do not include the new property, the default value for the new property will automatically be used.

3.  In the Form.New() method where the control was added, set a number properties of the control including the Status Text message (which appears at the bottom of the form), any Help Topic that may be associated with the control, and the Data Binding that links the control to the underlying Property established in Step 2 above. The AkWarm\_UI.Home.SetControlProperties() method is used to perform these tasks for many AkWarm Residential input controls.

4.  Add data validation tests for the new input by assigning custom attributes from the DataAttributes project to the new object property and/or adding code to a special data validation method, such as the AkWarmCalc.HomeInputs.ValidateDataHm() method.

5.  If a non-binding warning should be given to the user for certain input values, add that code in the AkWarmCalc.HomeInputs.WarningCheckHome() method (AkWarm Residential; for Commercial, the method is AkWarmCalc.BuildingInputs.WarningCheckBldg()).

6.  Add code to print out the new input in the AkWarmReporting.HomeInputsReport (Residential) or the AkWarmReporting.BuildingInputsReport.

7.  Include the new input in any calculations and reports relevant to the input.

<a name="vb_projects"></a> List of Visual Basic Projects and Associated Descriptions
---------------------------------------------------------

Below are brief descriptions of each Visual Basic Project in the AkWarm application. Separate documents provide more detailed developer information for the major projects in this list. The projects are categorized below by the part of the AkWarm system they apply to.

<a name="main_app"></a> ### Main AkWarm Application

***AkWarm\_UI* -** This project contains the Windows Forms, User Controls, and other code related to AkWarm’s user interface.

***AkWarmCalc* -** This project contains that classes that model all of the residential and commercial building components and contains classes that perform the energy, rating, and improvement calculations.

***AkWarmEnergyLibrary -*** This project contains classes that open from disk and make available the information held in the Energy Library.

***AkWarmEnergyLibraryEntities -*** This project contains a class for each table in the Energy Library, describing the properties (fields) of the rows in the table. Also, some of the classes have business logic added through partial classes to further manipulate the data in the tables.

***AkWarmReporting -*** This project contains all of code associated with creating AkWarm’s reports.

***BoilerplateLib -*** This project manages the “Boilerplate” items that can be inserted into an Improvement Options Report by a user. Each Boilerplate snippet is a separate Microsoft Word document and is categorized by the building components the snippet applies to.

***DynamicQuery -*** This project is used by the Energy Library project (specifically the *AkWarmEnergyLibrary.EnergyLibrary.SortAndFilterList()* method) to allow for flexible filtering and sorting of Energy Library lists without having to specifying the datatype of the list beforehand.

***DataAttributes -*** This project provides a data validation system used by AkWarm to validate input data. The classes in this project define special attributes that can be attached to properties and validation methods in the AkWarm object model.

***Experiments -*** This is a project that is used to run test code and various code experiments related to AkWarm. It is currently not necessary for building AkWarm or any other AkWarm-related tools.

<a name="installer"></a> ### AkWarm’s Setup/Installer Program

***Akwarm2Setup -*** This project creates the setup program (installer) for AkWarm.

<a name="test_utilities"></a> ### Utilities to Create and Test Energy Libraries

***CommandInterface -*** This project is only used for the command-line utilities that prepare Energy Libraries. This particular project holds a Visual Basic Interface that must be supported by each command line utility.

***EnergyLibraryMaintenance -*** This project creates the command line utility that is used to convert the Energy Library from Microsoft Access to the format used by AkWarm. Conversion to XML format is also possible with the utility.

***EnergyLibraryMaintenanceCommands -*** This project implements the specific commands available in the command line utility created by the *EnergyLibraryMaintenance* project.

***EnergyLibraryUtility -*** This project was used to test aspects of the various Energy Library projects. It is currently not necessary for building AkWarm or any other AkWarm-related tools.

***LibraryTester -*** The project contains a small GUI application that performs some validation tests on the data found in an Energy Library. These tests are used to review and identify data entry errors in an Energy Library before releasing the library.

<a name="developer_requirements"></a> Developer Software Requirements
-------------------------------

The following development tools are being used for AkWarm development:

1.  Microsoft Visual Basic .NET 2008.

2.  Microsoft .NET Framework 3.5.

3.  Microsoft Visual Studio 2008 integrated development environment.

4.  Microsoft Visual Basic Power Packs 3.0, for use of the Line and Shape controls in that package.

5.  Microsoft Chart Controls for .NET Framework 3.5.

# Developer Contact Information <a name="developer_contact"></a>
-----------------------------

The following people have had extensive involvement with the development of the source code, Energy Libraries, and Help file for AkWarm:

> **Alan Mitchell**
> Analysis North
> 11400 Mountain Lake Dr
> Anchorage, AK 99516
> 907-310-9124
>
> **Ian Moore**
> Alaska Map Science
> 15585 Newell Drive
> Anchorage, AK 99516
> 907-348-0237
>
> **Ginny Moore**
> Flattop Technical Services
> 14530 Echo Canyon Road
> Anchorage, AK 99516
> 907-345-1355
