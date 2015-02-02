EnergyLibraryMaintenance (elmaint)

- [Summary](#summary)
- [Commands](#commands) 
- [“Help” Command](#help) 
- [“LIST-COMMANDS” Command](#list)
- [“SHOW-COMMANDS” Command](show)
- [“Convert” Command](#convert)
- [“Decrypt” Command](#decrypt)
- [“Encrypt” Command](#encrypt)
- [“Info” command](#info)
- [“Inventory” Command](#inventory)

# Summary <a name="summary"></a>

EnergyLibraryMaintenance, or elmaint, is a command-line tool used to perform certain actions on EnergyLibrary files. The program loads commands from .dlls dynamically using CommandInterface,

an interface implemented by commands contained in the CommandInterface.dll file. This file must be in the same folder as the elmaint.exe program. In addition to these commands, there are three custom commands: no arguments, LIST-COMMANDS, and SHOW-COMMAND.

If you type the elmaint.exe name without any arguments, it loads the AppSettings\>Help key of the elmaint.exe.config file (this file must also be in the same folder as the elmaint.exe program). By default the help is as follows in the example:

# Commands <a name="commands"></a>

## “Help” Command (no arguments) <a name="help"></a>

***EXAMPLE* 1:**

C:\\Example\>elmaint.exe

Type the executable name with no arguments to see help. Type LIST- COMMANDS to see a list of commands. Type SHOW-COMMAND followed by a command name to see information about a specific command.

##“LIST-COMMANDS” Command <a name="list"></a>

The LIST-COMMANDS built-in command displays a list of commands with their descriptions, thus:

***EXAMPLE* 2:**

C:\\Example\>elmaint.exe LIST-COMMANDS


- Convert: Converts an Access database to an XML energy library file. 
- Decrypt: Decrypts and saves an EnergyLibrary file without instantiating it as an EnergyLibrary
- Encrypt: Encrypts an EnergyLibrary XML file without instantiating it as an EnergyLibrary.
- Info: Gets info about an EnergyLibrary file (.lib, .xml, .accdb, or.mdb)
- Inventory: Inventories the lists contained in an EnergyLibrary file(.lib, .xml, .accdb, or .mdb) 
- Test: A testing command

*Note: The descriptions on some of the commands are slightly incorrect. More detailed and current descriptions follow.*

## “SHOW-COMMANDS” Command <a name="show"></a>

The SHOW-COMMAND built-in command displays a command, its description, and all its available parameters and switches, with descriptions, thus:

***EXAMPLE* 3:**

C:\\Example\>elmaint.exe SHOW-COMMAND Convert

- Convert: Converts an Access database to an XML energy library file.
	- Parameters:
		- source: The source file to convert
		- destination: The destination to which to save the converted file. This will not overwrite unless the /overwrite switch is called.
	- Switches:
		- overwrite: If specified, the command will overwrite the file at the destination if it exists.
		- encrypt: If specified, the command will encrypt the output file.

Commands are called by typing the program, followed by a command. Any parameters or switches are written after that, preceded by a “/”. Parameters and switches may be given in any order.

## “Convert” Command <a name="convert"></a>

The Convert command loads an EnergyLibrary file of any type and instantiates it as an EnergyLibrary. It then saves it as an EnergyLibrary XML file. Encryption/compression is optional.

The Convert command supports the following conversions:

• Access --> LIB (encrypted, compressed XML) – requires /encrypt switch

• Access --> XML (plain XML)

• XML --> LIB – requires /encrypt switch

• LIB --> XML

It takes the following parameters and switches:

- Parameters
	- source: The source file to convert
	- destination: The destination to save to. If a file already exists at the destination, the /overwrite switch must be called.
- Switches
	- overwrite: If this switch is specified, the command will overwrite a file at the destination, if it exists.
	- encrypt: If this switch is specified, the destination file will be encrypted. 
	 
You can use it thus:

***EXAMPLES* 4-6:**

C:\\Example\>elmaint.exe Convert /source:C:\\Example\\ExampleEL.accdb/destination:C:\\Example\\ExampleEL.xml

‘This will convert the ExampleEL.accdb file and save it as ExampleEL.xml, unencrypted and uncompressed

C:\\Example\>elmaint.exe Convert /source:C:\\Example\\ExampleEL.xml
/destination:C:\\Example\\ExampleEL.lib /encrypt

‘This will convert the ExampleEL.xml file and save it as

ExampleEL.lib, encrypted and compressed.

C:\\Example\>elmaint.exe /source:C:\\Example\\ExampleEL.lib

/destination:C:\\Example\\ExampleEL.xml /overwrite

‘This will convert the ExampleEL.lib file and save it as ExampleEL.xml, unencrypted and uncompressed, overwriting the previous file.

## “Decrypt” Command <a name="decrypt"></a>

The Decrypt command decrypts and decompresses a LIB file without actually deserializing and reserializing it through the EnergyLibrary code, which can cause unwanted updates and artifacts based on new code (attributes, classes) in the current version of the EnergyLibrary code. This is a method for turning old LIB files into raw XML files without touching the XML or modifying it any way by running it through the current serialization code.

It takes the following parameters and switches:

- Parameters:
	- source: The source file to convert.
	- destination: The destination to save to. If a file already exists at the destination the /overwrite switch must be specified.
- Switches:
	- overwrite: If this switch is specified, the command will overwrite a file at the destination, if it exists.

You can use it thus:

***EXAMPLE* 7:**

C:\\Example\>elmaint.exe Decrypt /source:C:\\Example\\ExampleEL.lib

/destination:C:\\Example\\ExampleEL.xml

‘This will decrypt the encrypted, compressed ExampleEL.lib file and save it as an unencrypted, uncompressed file called ExampleEL.xml

## “Encrypt” Command <a name="encrypt"></a>

The Encrypt command encrypts an XML file and turns it into a compressed, encrypted LIB file without any EnergyLibrary serialization.

It takes the following parameters and switches:

- Parameters:
	- source: The source file to convert.
	- destination: The destination to save to. If a file already exists at the destination the /overwrite switch must be specified.
- Switches:
	- overwrite: If this switch is specified, the command will overwrite a file at the destination, if it exists.

You can use it thus:

**EXAMPLE 8:**

C:\\Example\>elmaint.exe Encrypt /source:C:\\Example\\ExampleEL.xml

/destination:C:\\Example\\ExampleEL.lib

‘This will decrypt the unencrypted, uncompressed ExampleEL.xml file

and save it as an encrypted, compressed file called ExampleEL.lib

## “Info” command <a name="info"></a>

The Info command displays information like version number from the MiscellaneousInfo object in an Access, XML, or LIB EnergyLibrary file.

It takes the following parameters and switches:

- Parameters:
	- source: The source file to convert.
- Switches:
	- expand: If specified, will add a line between each item.

You can use it thus:

| ***EXAMPLE* 9:**   
   
 C:\\Example\>elmaint.exe Info /source:C:\\Example\\ExampleEL.xml

Name: 
ID: 1 
Library Version: 6/30/2010 
Description: Discount Rate: 0.03  
PCE Funding Percent: 1
PCE Kilowatt-Hour Limit: 500  
Regulatory Surcharge: 0.0035  
Regulatory Surcharge Electric: 0.000432   
Miscellaneous Notes: Inflation factors and discount rate from 2009-10 FEMP; Regulatory surcharge starting with this version is now correctly modeled as a % for gas utilities and a $/kWh for electric utilities. PCE 100% funding in effect July 2009

## “Inventory” Command <a name="inventory"></a>

The Inventory command display a summary of the library classes contained in an Access, XML, or LIB EnergyLibrary file, along with an optional count of the objects in each class.

It takes the following parameters and switches:


- Parameters:
	- source: The source file to convert.
- Switches:
	- expand: If specified, will add a line between each item.
	- showtype: If specified, will write the type of each list.
	- showcount: If specified, will write the count of each list.

You can use it thus:

***EXAMPLE* 10:**

C:\\Example\>elmaint.exe Inventory /source:C:\\Example|ExampleEL.xml
/showcount /showtype /expand

City: Count: 284
Type: System.Collections.Generic.List\`1[AkWarmEnergyLibraryEntities.City]

DHWEquipment: Count: 30
Type: System.Collections.Generic.List\`1[AkWarmEnergyLibraryEntities.DHWEquip ment]

‘Remaining lists omitted.
