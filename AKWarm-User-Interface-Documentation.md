-   [Introduction](#introduction)
-   [Help File Integration](#help_file)
-   [List of Files and Associated Descriptions](#file_list)
    -   [Primary Forms](#primary_forms)
    -   [Dialog Forms](#dialog_forms)
    -   [Generic User Controls](#user_controls)
    -   [Residential Inputs Controls](#residential_inputs)
    -   [Commercial Inputs Controls](#commercial_inputs)
    -   [Shell Component Controls](#shell_component)
    -   [Residential Lights & Appliances Controls](#residential_lights)
    -   [Commerical Electrical Loads Controls](#commercial_electric)
    -   [Commercial Scheduling Controls](#commercial_scheduling)
    -   [Stand-alone Modules](#stand_alone)

# AKWarm User Interface Project Documentation

Introduction <a name="introduction"></a>
-------------

The AkWarm User Interface is structured as a MDI (Multiple Document Interface) application. The main form (MDImain.vb) is a MDI container and can open and contain Home forms (Home.vb) and Building forms (Building.vb), but provides little functionality on its own. The Home form (Home.vb) handles the majority of the user interface for Residential data entry and rating results presentation, but calls a number of other forms and user controls to handle specific tasks.  The Building form (Building.vb) is the corresponding primary form for Commercial projects. A number of general functions that are used throughout the user interface are found the the module UI\_Helpers.vb.


Data entry controls in the Home and Building forms are bound directly to the underlying AkWarmCalc objects with Windows Forms databinding. The databinding is established in the 'New' event procedure of the form object where the routine SetControlProperties is called repeatedly to set up the databinding, tooltips, help topic, and value lists for combo and list boxes.


Combo and List Boxes in the UI are assigned their value lists either from entries in the Energy Library or directly from Enum types. The UI\_Helpers module has routines that are used for both cases, and contains a class definition for a AkWarmListboxValue type that is used for elements of the list of values supplied to the list control. For lists based on Enum values, the displayed text can come either from the text of the enum field, or from a special attribute property that is added to the enum using a type that is defined in the DataAttributes project.

 
The data entry portion Home and Building forms' interface is centered around a tab control that has pages for  groupings of the information that is collected. Most of the flow of the interface is fairly simple and straightforward, but there are a few areas to note:

-   The page for 'Shell Components' initially displays a grid showing summary information for all shell components. When a shell component is selected or created, the display switches to a view where the summary grid is made small and the right pane of the form displays a usercontrol with data entry elements for the specific component. A shell component usercontrol is loaded and bound to its data each time a row is selected in the shell component summary grid, and is removed when a different shell component is selected.

-   On the residential ‘Home’ Heater page, there is a tab control that switches between the primary and secondary heating systems. Only one set of controls exist, but when the selected page changes, the controls are moved to the active tab and their databinding is updated to link them to the appropriate data element on the AkWarmCalc.HomeInputs object.

-   The 'Calculate' button on the form initiates code to perform energy calculations, and switches the display between the data entry tabs and a set of results tabs that are contained in the CalculationResultsControl UserControl.


The user interface contains several layers of data validation. First, wherever possible the data entry controls are set to limit inputs to only the allowable values. Next, after every update to a data-bound control, a data validation routine is run to check the validity of all of the inputs. Any controls that are bound to a property with an invalid or missing value are flagged through an ErrorProviderControl with a red dot. Finally, when the 'Calculate' button is clicked, a more thorough routine to check for errors in the inputs is run and a list of all problems and warnings is displayed for the user.


Wherever possible the code attempts to avoid cases that might cause errors, or to trap them explicitly, but unhandled errors are also trapped by a more generic error handler. Errors are logged to an application log file which will be located in the same directory as the executable file, and a form is displayed that encourages the user to allow the file to be emailed to the developers so the error can be resolved. The text of the error message is saved in the AkWarm file and can be displayed by pressing Ctrl-D from anywhere in the Home form.

The approaches used in the user interface have evolved and improved over the course of AkWarm development. One of the more recent modules is the ResidentialLightsAndApplinaces interface, which is a reasonably good model for future UI development.

Help File Integration <a name="help_file"></a>
---------------------

The AkWarm interface is integrated with a help document (AkWarm.chm) and most controls are setup so that pressing F1 will take the user directly to the applicable help topic. When new features are added to AkWarm, corresponding topics should be added to (or updated in) the help document. The AkWarm.CHM file can be updated with Microsoft HTML Help Workshop (a free download) or with any number of third party .CHM editors (which may be easier to use). To avoid impacts on the existing F1 functionally, the filename and location of the help document and names of existing pages should not be changed, and existing pages should not be removed without verifying that they are no longer referenced within the interface. Within the project, F1 functionality is implemented with .NET HelpProvider controls. On the Home and Building forms, the help associations are set up with calls to the SetControlProperties routine.

List of Files and Associated Descriptions <a name="list_file"></a>
-----------------------------------------

The files in the AkWarmUI project are listed below with short descriptions of their purpose. The files are categorized by function.

### Primary Forms <a name="primary_forms"></a>

**Forms/MDImain.vb** - MDI container, opens Home forms, but little functionality of its own.

**Forms/Home.vb** - Primary form for Residential data entry and results presentation

**Forms/Building.vb** - Primary form for Commercial data entry and results presentation


----------

### Dialog Forms  <a name="dialog_forms"></a>

**Forms/AboutBox.vb** - Informational screen that can be displayed at any time from MDImain

**Forms/SplashScreen.vb** - Informational screen that is displayed while the application is opening

**Forms/Password.vb** - Dialog to allow entry of a password when a rating is saved as 'official'

**Forms/WhichLibraryDialog.vb** - When a file that was saved with an old version of the energy library is re-opened, this dialog presents the option of opening the file with either the old version or the new version of the energy library.

**Forms/LibraryUpdateStatus.vb** - Progress dialog shows the status of a library update operation

**Forms/FuelPrices.vb** - Dialog to allow user entry of fuel prices if they don't exist in the energy library

**Forms/DialogMessageList.vb** - Dialog to present error or warning messages found during an attempt to calculates results for a home or building

**Forms/EditTextPopup.vb** - Popup dialog to allow viewing and editing text values that are too long to fit on their primary form.

**Forms/ErrorReportingForm.vb** - Dialog that is displayed if an unhandled error is encountered

**Forms/EmailFile.vb** - Dialog to allow a file to be emailed to the developers after an unhandled error is encountered and if the automatic upload fails

**Forms/DebugDialog.vb** - Displays any saved debug information when Ctl-D is pressed.

**Forms/ReferenceCityDialog.vb** - Dialog to select a reference city if more than one is available for the entered zip code

**Forms/AddShellComponentDialog2.vb** - Dialog to select which shell component type to add based on a visual representation

**Forms/AreaCalculator.vb** - *Removed*

**Forms/AreaCalculator2.vb** - Dialog to enter information to define geometric shapes and calculate their areas

**Forms/FlatToSlopedCalculator.vb** - Dialog to compute slope multipliers for surface areas

**Forms/AboveGradeWallWizard.vb** - Wizard to streamline inputs for standard above grade walls

**Forms/CathedralCeilingWizard.vb** - Wizard to streamline inputs for standard ceiling types

**Forms/GarageWizard.vb** - Wizard to add shell components for standard garages

**Forms/DialogAdjustCost.vb** - Dialog to adjust Residential improvement costs

**Forms/DialogSelectHeater.vb** - Dialog to select a Residential heater or water heater from available values in the energy library

**Forms/ImprovementInputsDialog.vb** - Dialog to enter inputs needed to an improvement. Currently only used for Residential heater upgrade devices.

**Forms/DialogHeatDistribution.vb** - Dialog to provide inputs for Residential heating system heat distribution

**Forms/UpdateGargageShellComponents.vb** - Dialog to identify garage shell components in old files to support design heat loss calculations

**Forms/HeatPlantDetailDialog.vb** - Dialog to enter Commercial heating plant details

**Forms/PumpsAndFansDialog.vb** - Dialog to enter Commercial Pump and Fan details

**ScheduleUI/ScheduleDetailsForm.vb** - Popup form to edit or view schedule details.


----------

### Generic User Controls <a name="user_controls"></a>

**OtherUserControls/ArithExpressionControl.vb** - User interface for the AkWarmCalc ArithExpression object

**OtherUserControls/NumericTextBox.vb** - Custom Text box that limits entry to numeric values

**OtherUserControls/RadioGroupBox.vb** - Displays a group of radio buttons and provides for data binding

**OtherUserControls/DropDownControl.vb** - Custom base class for dropdown controls. It can be inherited to implement a dropdown. Currently used by DropDownTreeControl.

**OtherUserControls/DropDownTreeControl.vb** - Works similar to a combo box control, but displays the dropdown results in a tree format to allow easier viewing of a long list of results. Inherits from DropDownControl.

**OtherUserControls/ImageLinkControl.vb** - Displays a thumbnail of an embedded image along with its source path and associated notes

**OtherUserControls/ImageLinkListControl.vb** - Displays a list of ImageLinkControls with the ability to add and delete

**OtherUserControls/ValueWithSourceControl.vb** - Custom double input control that provides a numeric text box input for a value and a combo box input for its source

**OtherUserControls/FlowPanelControl.vb** - Similar to the built-in FlowLayoutPanel, but simpler logic and can be used with visual inheritance (unlike the built-in version)

**OtherUserControls/BaseUserControl.vb** - Provides basic functionality for AkWarm data binding, data validation and status bar updating. Inherited by many of the AkWarm inputs controls. Should be inherited by any new inputs controls.


----------

### Residential Inputs Controls <a name="residential_inputs"></a>

**OtherUserControls/BoilerplateSelectionControl.vb** - Control to select from available reporting boilerplate options

**OtherUserControls/ImprovementInputsControl.vb** - Control to provide data entry to improvement inputs

**OtherUserControls/HealthSafetyApplianceControl.vb** - Control used to describe an appliance that is entered in the Health and Safety section.

**OtherUserControls/HealthSafetyApplianceListControl.vb** - Displays a list of the HealthSafetyApplianceControls in the Health and Safety section.

**OtherUserControls/HeaterSelectionControl.vb** - Control to select a heater

**OtherUserControls/CalculationResultsControl.vb** - Displays results of the rating calculation

**OtherUserControls/CalculationResultsImprovementsControl.vb** - *Removed*

**OtherUserControls/CalculationResultsImprovementsControl2.vb** - Display improvements information within the calculation results

**OtherUserControls/DesignHeatLossControl.vb** - Control to collect the inputs for the Design Heat Load calculation.

----------

### Commercial Inputs Controls <a name="commercial_inputs"></a>

The following controls provide user inputs for AkWarm Commercial buildings. Most inherit from BaseUserControl:

**OtherUserControls/ActualVsModeledControl.vb -** Control to display the graphs that compare actual fuel use versus modeled fuel use.

**OtherUserControls/AirLeakageControl.vb -** Control to collect the inputs necessary for calculation of natural air leakage.

**OtherUserControls/AnyFuelLoadListControl.vb -** Displays a list of CookingControls or DryerControls.

**OtherUserControls/BldgSpaceControl.vb -** Control to describe a space (e.g. office, classroom, etc.) in the building.

**OtherUserControls/BldgSpaceListControl.vb -** Displays a list of BldgSpaceControls.

**OtherUserControls/CalculationResultsControlComm.vb -** The main container control that allows the user to select and display each calculation result screen.

**OtherUserControls/CookingControl.vb -** Control to collect the inputs describing a cooking appliance.

**OtherUserControls/CoolingPlantControl.vb -** Control to collect the inputs describing a cooling plant (a chiller or air conditioning unit that produces cooling).

**OtherUserControls/CoolingPlantListControl.vb -** Control to display a list of CoolingPlantControls.

**OtherUserControls/DHWsystemControl.vb -** Control to collect the inputs describing a Domestic Hot Water storage and distribution system.

**OtherUserControls/DistributionControl.vb -** Control to collect the inputs for a space heating and/or cooling distribution system.

**OtherUserControls/DistributionListControl.vb -** Displays a list of DistributionControls.

**OtherUserControls/DryerControl.vb -** Control to collect the inputs that describe a clothes drying system.

**OtherUserControls/FuelUse.vb -** Control to collect actual monthly fuel use data for a year for a particular fuel type.

**OtherUserControls/FuelUseListControl.vb -** Control to display and manage a list of FuelUse controls.

**OtherUserControls/HeatPlantControl.vb -** Control to collect the inputs describing a heating plant, such as a boiler or furnace.

**OtherUserControls/HeatPlantDetailControl.vb -** Control to collect detailed inputs about a heating plant, inputs that do not affect the actual energy use calculation but are useful data for archiving. This control is displayed by clicking a “Details...” button on the HeatPlantControl.

**OtherUserControls/HeatPlantListControl.vb -** Control to display a list of HeatPlantControls.

**OtherUserControls/NameAddrControl.vb -** Control to collect name and address information for a person. Used for collecting building owner, contact, and auditor information.

**OtherUserControls/PumpFanControl.vb -** Control to collect the inputs describing a pump or fan.

**OtherUserControls/PumpFanListControl.vb -** Control to display a list of PumpFanControls.

**OtherUserControls/VentilationControl.vb -** Control to collect the inputs describing a ventilation system that delivers fresh outside air to the building.

**OtherUserControls/VentilationListControl.vb -** Control to display a list of VentilationControls.

----------


### Shell Component Controls <a name="shell_component"></a>

**ShellComponentControls/ShellComponentsListControl.vb** - Not yet used, but eventually should replace the controls on the Home and Building forms to reduce code duplication

**OtherUserControls/InsulationInputControl.vb** - Control to select insulation type and thickness, used for shell components

**ShellComponentControls/ShellComponentControl.vb** - Generic shell component control for data entry. All other shell component controls inherit from this

The following user controls provide inputs specific to each shell component type and inherit from ShellComponentControl:

**ShellComponentControls/ShellAboveGradeFloorControl.vb**

**ShellComponentControls/ShellAboveGradeWallControl.vb**

**ShellComponentControls/ShellBelowGradeFloorCenter.vb**

**ShellComponentControls/ShellBelowGradeFloorPerimeter.vb**

**ShellComponentControls/ShellBelowGradeWallControl.vb**

**ShellComponentControls/ShellCeilingAtticControl.vb**

**ShellComponentControls/ShellCeilingCathedralControl.vb**

**ShellComponentControls/ShellDoorControl.vb**

**ShellComponentControls/ShellGarageDoorControl.vb**

**ShellComponentControls/ShellWindowControl.vb**

 

----------


### Residential Lights & Appliances Controls <a name="residential_lights"></a>

**ResidentialLightsAndAppliances/LightsAndAppliancesControl.vb** - List control for residential lights and appliances. This is currently used on the Home form.

**ResidentialLightsAndAppliances/AddLightOrApplianceDialog.vb** - Dialog that is initiated by the LightsAndAppliancesControl to allow a user to add a light or appliance.

**ResidentialLightsAndAppliances/LightOrApplianceControl.vb** - Basic control to display and edit information for a residential light or appliance, including both pre and post retrofit versions and upgrade costs.

**ResidentialLightsAndAppliances/LightOrApplianceEquipmentControl.vb** - Control to display and edit information about a residential light or applinace (either pre or post retrofit). This is used twice within the LightOrAppilance control, once for the pre-retrofit information and once for the post-retrofit information.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionControl.vb** - Control to display and edit all consumption information for a residential light or appliance. This is used within the LightOrApplinaceEquipmentControl.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionByRateInputsControl.vb** - Control to display and edit ‘by rate’ consumption inputs for one consumable commodity for a residential light or appliance. This is used within the LightOrApplianceConsumptionControl.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionPerTimePeriodInputsControl.vb** - Control to display and edit ‘by time period’ consumption inputs for one consumable commodity for a residential light or appliance. This is used within the LightOrApplianceConsumptionControl.

**ResidentialLightsAndAppliances/LightOrApplianceConsumptionPerUseInputsControl.vb** - Control to display and edit ‘per use’ consumption inputs for one consumable commodity for a residential light or appliance. This is used within the LightOrApplianceConsumptionControl.

----------


### Commerical Electrical Loads Controls <a name="commercial_electric"></a>

**Electrical Loads/ElectricalLoadsControl.vb -** List control to manage electrical loads for a building. It employs the same look and feel as the shell components list.

**Electrical Loads/AddElectricalLoadDialog.vb -** Dialog (form) to add a new electrical load to a building.

**Electrical Loads/LightingControlControl.vb -** UserControl used to specify electrical controls applied to a load. Despite the name, this is used for all types of electrical loads.

The following commercial Electrical Load usercontrols make use of Visual Inheritance from ElectricalLoadControl to ElectricalHourlyLoadControl to the specific load controls. This approach is clean in terms of code re-use, but there were enough difficulties with the implementation in VisualStudio that we haven’t used Visual Inheritance in subsequent AkWarm modules.

**Electrical Loads/ElectricalLoadControl.vb -** Base usercontrol for Electical loads. It is inherited by ElectricalHourlyLoadControl.

**Electrical Loads/ElectricalHourlyLoadControl.vb -** Base usercontrol for hourly loads. Inherited from ElectricalLoadControl and inherited by LightingLoadControl, RefrigerationLoadControl and OtherLoadControl.

**Electrical Loads/LightingLoadControl.vb -** Usercontrol for lighting loads.

**Electrical Loads/OtherLoadControl.vb -** Usercontrol for “Other” electrical loads.

**Electrical Loads/RefrigerationLoadControl.vb -** Usercontrol for refrigeration loads.

----------


### Commercial Scheduling Controls <a name="commercial_scheduling"></a>

**ScheduleUI/ScheduleChooserControl.vb** - Dropdown control for selecting a schedule from the list of existing schedules and/or adding new schedules.

**ScheduleUI/ScheduleControl.vb** - Primary control for viewing and editing schedules. This control is displayed on the ScheduleDetailsForm.

**ScheduleUI/ScheduleSeasonControl.vb** - Control for viewing and editing schedule season information. This is use one or more times on the ScheduleControl.

**ScheduleUI/ScheduleDaysControl.vb** - Control for viewing and editing schedule day-of-the-week information. This is used one or more times on the ScheduleSeasonControl.

**ScheduleUI/ScheduleTimesControl.vb** - Control for viewing and editing schedule time-of-day information. This is used one or more times on the ScheduleDaysControl.

**Electrical Loads/DataGridViewCalendarColumn.vb** - Calendar column type for use in a DataGridView control. This is used by the ScheduleSeasonControl

----------


### Stand-alone Modules <a name="stand_alone"></a>

**AkWarm\_UI/UI\_Helpers.vb** - A number of general functions that are used throughout the user interface
