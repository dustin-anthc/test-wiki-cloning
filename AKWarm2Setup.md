-   [Introduction](#introduction)
-   [Installed Files and Locations](#installed_files)
-   [Procedure for Releasing a New Version of AkWarm](#release_procedure)

<a name="introduction"></a> 
Introduction
------------

The AkWarm2Setup project is a standard Visual Studio 2008 Setup Project that creates a Windows Installer application. That Installer application is capable of installing AkWarm on the user’s computer. This document gives an overview of the files installed by the application and the target location on the user’s computer for those files. Also, a step-by-step procedure is given for preparing a new AkWarm release.

<a name="installed_files"></a> 
Installed Files and Locations
-----------------------------

The list below gives the files installed and the default locations for those files on the user’s computer:

1.  **Compiled DLL and EXE Files associated with the Application:** The default installation location for these files is the *Program Files\\AHFC\\AkWarm* folder (or the *Program Files (x86)\\AHFC\\AkWarm* folder). As a shorthand, this folder is referred to as the *\<application folder\>* in the text below.

2.  **Online Help File:** The Microsoft HTML Help File that provides online help for the application is named *AkWarm.chm* and is stored in the *\<application folder\>* folder.

3.  **Microsoft Word Report Templates:** These MS Word files are used as templates to generate the reports utilizing MS Word Automation (e.g. residential Improvement Options Report). They are installed in the *\<application folder\>\\Reports* folder.

4.  **Microsoft Word Improvement Description and Boilerplate Files:** These MS Word files are used to provide improvement descriptions and added boilerplate text in the residential Improvement Options Report and in the commercial Long Audit Report. They are stored in the *\<application folder\>\\Descriptions* and the *\<application folder\>\\Snippets* folders, respectively.

5.  **Energy Library Files:** The Energy Library files are stored as a separate file for each Library version, and they are located in the *\<application folder\>\\LibraryFiles* folder. Library files end in the extension *.lib*. When the AkWarm application first runs on the user’s computer, it transfers the installed library files from this folder to a folder that has less restrictive permissions, so that automatic Energy Library downloads from the Internet can occur into the folder. That less restrictive folder is in the user’s Application data folder, which is given by the special .NET variable *My.Computer.FileSystem.SpecialDirectories.CurrentUserApplicationData.* See the *AkWarmCalc.LibraryUtil.EnergyLibraryList()* method for more details.

6.  **Sample Files and Data Collection Form:** The sample files for the residential and commercial software as well as a data collection form for the residential software is stored in the user’s *My Documents/AkWarm/Sample Files* folder.

7.  **Application Shortcuts:** Shortcuts for starting the AkWarm application are installed on the user’s Desktop and under the *AkWarm* group on the Start menu.

<a name="release_procedure"></a> 
Procedure for Releasing a New Version of AkWarm
-----------------------------------------------

This section describes the steps involved for releasing a new version of AkWarm.

1.  If a new Energy Library is being released, add the Energy Library file to the *AkWarmEnergyLibrary* project in the *LibraryFiles* folder. On the “File Properties” settings for the file, set the “Build Action” property to “Content”, and set the “Copy to Output Directory” property to “Copy Always”.

2.  Run the AkWarm test files through the new version of AkWarm, ensuring that no errors occur and calculated Rating Point and Energy Use values are reasonable.

3.  If any changes have been made to the MS Word template files used to create the residential Improvement Options Reports and the commercial Audit reports, increment the version number in the name of these files. For example, change *improve\_rpt\_Rate02.doc* to *improve\_rpt\_Rate03.doc*. The reason for doing this is: if the user already has AkWarm installed and if they have edited the Word template files (to perhaps add their logo), the installer will not overwrite the template file. By changing the name of the new template file, it will certainly be installed. Note that the AkWarm code that refers to the template file does not need to be changed as it knows to use the template file with the highest version number in its name.

4.  Increase the “Assembly Version” and “File Version” numbers of each VB Project involved in the AkWarm application. The version numbers to use should be the desired version number of the AkWarm release. These version settings are reached by right-clicking on the Project in the Visual Studio Solution Explorer and selecting “Properties”. On the “Application” tab, click “Assembly Information” and edit the settings. A screenshot is shown below for the AkWarmCalc project:
    ![](media/image1.png)
    The Projects involved with the AkWarm application are: *AkWarm\_UI, AkWarmCalc, AkWarmEnergyLibrary, AkWarmEnergyLibraryEntities, AkWarmReporting, BoilerplateLib, DataAttributes,* and *DynamicQuery.* Updating all of the version numbers is important so that new versions of the projects will certainly be copied to the user’s machine. Relying on newer file dates alone to ensure install has proven to be unreliable.

5.  In the *AkWarm2Setup* installer project, the Version number should be updated. The Version number is found on the Properties sheet for the Project. It is a 3-part dotted number, so we have typically translated the 4 digit Akwarm version code into three digits by combining the last two numbers; thus, 2.2.0.3 become a setup Version number of 2.2.03. When you the change the Version number, Visual Studio will ask if you want to change the ProductCode as well. Say “Yes” to the request, which will cause Visual Studio to generate a new ProductCode.

6.  Open, Calculate, and Re-Save the sample files so that they contain the version information from the current version. The sample files are located in *AkWarmUI/Sample Homes* and the *AkWarmUI/Sample Buildings* folders in the Visual Studio Solution Explorer.

7.  Select the *Build, Configuration Manager* menu item, and change the “Active solution configuration” item to “Release” instead of “Debug”. Choose “Any CPU” for “Active Solution Platform”. Force an entire rebuild of the solution by right-clicking on the “Solution ‘AkWarm’” item in Solution Explorer and selecting “Rebuild Solution”. This will rebuild the AkWarm projects and rebuild the Setup project, which creates the Windows installer.

8.  Use the Microsoft Signtool Wizard to sign the two executable files created by the Setup project with your Code Signing certificate: *AkWarm.msi* and *setup.exe*. These files are found in the *Akwarm2Installer\\Release* folder. An economical place to purchase a Code Signing certificate is from the Tucows Author Resource Center. On my Windows 7 machine, the Microsoft Signtool wizard can be executed by running:
    *"C:\\Program Files\\Microsoft SDKs\\Windows\\v6.0A\\Bin\\signtool.exe" signwizard
    *The timestamp server URL for the Tucows code signing certificates is:
    *http://timestamp.comodoca.com/authenticode
    *

9.  Create a self-extracting Zip file from the two Setup files (*AkWarm.msi* and *setup.exe)* so that users have one file to download for installing AkWarm. This self-extracting Zip file is the installation file available for download from a AkWarm installation web page. To create the file, use the *WinZip Self-Extractor* product. Important settings are:

    1.  Despite the description, use the “Standard self-extracting Zip file” option instead of the “Self-extracting Zip file for Software Installation” option, as we discovered permission problems when installing on some machines with the latter option.

    2.  Leave the “Unzip To” folder blank.

    3.  For the command to issue after the unzip operation, use “.\\setup.exe” .

    4.  For the icon to display in the self-extracting zip file, use the AkWarm icon found at *AkWarm\_UI\\Icons\\AkWarm\_Original.ico .*

    5.  Select “Default to overwrite files without prompting” and “Unzip automatically”. Also select “Run as administrator”.

10. Once the self-extracting Zip file is created, use the Signtool Wizard to digitally sign the self-extracting zip file. Test the installer from your local hard drive to make sure it correctly installs the new AkWarm version. Post the file to a web server that is available to users. Test the installer download process from the web server.

11. There are other web server tasks that are required:

    1.  The “Version\_Info.txt” file needs to be updated to hold the version number of the new release. See the *AkWarm\_UI.MDImain.CheckForAkWarmUpdates()* method for the URL of the file (currently *analysisnorth.com/AkWarm/update\_combined/Version\_Info.txt*) and other details. Everytime a user starts AkWarm, AkWarm downloads this file to determine if the user’s version of AkWarm is up to date. A sample of this file is:
         \#LATEST\_VERSION
         2.2.0.3

    2.  The “Library\_Info.txt” file should be updated to include a new Energy Library entry, if one was released with the software. See the *AkWarm\_UI.MDImain.CheckForAkWarmUpdates() and the AkWarmCalc.LibraryUtil.CheckForUpdates()* methods for the URL of the file (currently *analysisnorth.com/AkWarm/update\_combined/Library\_Info.txt*) and other details. A sample of this file is:
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
        Also, the new Energy Library itself (the *.lib* file) should be uploaded to the web server (currently the *analysisnorth.com/AkWarm/update\_combined/* folder) so the it is available for automatic download by AkWarm.

    3.  Update the actual HTML page that the users go to for downloading AkWarm, currently *analysisnorth.com/AkWarm/AkWarm2download.htm*l . The link on this page to the installer file must be updated to point to the new installer posted to the web server in step 10.

    4.  Update the HTML page that lists the changes that occurred in the new AkWarm release. This page is currently *analysisnorth.com/AkWarm/AkWarm2changeLog.html* .

12. Commit the Source Code used to compile the release to the Source Code Repository and in the commit message indicate that this was the code for release X.X.X.X. Also, copy that commit revision to the *tags* folder of the Source Code repository where all release revisions are tagged and are easily accessible.

13. Send the e-mail to AHFC announcing the new release!
