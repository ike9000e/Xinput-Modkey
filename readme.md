
Xinput Modkey
==========================

	Modkeys and hotkeys for gamepad buttons in games that use Xinput.
	Both Windows architectures, 32 and 64-bit.

	With Xinput Modkey, following can be achieved:

	* Remap original gamepad buttons into other buttons.
	* Simulate keyboard keys with gamepad inputs.
	* Simulate mouse buttons.
	* Navigate with mouse cursor using analog thumbsticks.
	* Apply deadzones in games that doesn't do this (default only).
	* Remap simultaneously pressed, two or more, gamepad buttons into:
	  * another gamepad button,
	  * keyboard key or
	  * mouse button.

	In current version, configuration must be done manually,
	by editing configuration INI file. Please see self documented
	"documented_xinput_modkey.ini" file.

	Filter DLL is a windows module file that needs to be attached to the
	target process durning its startup. This is the module that,
	once configured, works independently by starting itself every
	time the game/program starts.
	
	For more details please see "Manual Install" and "Manual Uninstall" below.



Using Filter DLL - Manual Install
--------------------------------------------------

	Determine the architecture of your target game/program executable (.exe).
	See section "How to check if a file is 32-bit or 64-bit" below.

	Copy "xinput_modkey.dll" and "xinput_modkey.ini" into the same
	directory the target game executable file is located in.
	DLL architecture must be the same as the game.

	Use one of the following methods to start the game.

	How to start game process with DLL module attached?
	-------------------------------------------------------

		Possible ways to do this:

		1. Use forwarder DLL that comes with Xinput Modkey project.
		   Modules to corresponding architecture are located under following
		   paths:
		       "release64/xinput_dll_forwarder.dll"
		       "release32/xinput_dll_forwarder.dll"
		   
		   In the game/program directory, remame "xinput_dll_forwarder.dll"
		   to "xinput1_3.dll". Note that "xinput1_3.dll" is the most common name.
		   All possible different names are: 
				"xinput9_1_0.dll", 
				"xinput1_1.dll", 
				"xinput1_2.dll", 
				"xinput1_3.dll" and 
				"xinput1_4.dll".
		   
		   To determine which one to use, examine the loaded modules 
		   of the running process|game.

		2. Use the loader program to start the game executable with
		   the filter DLL module attached, "xinput_modkey.dll".

		3. Use PE editor programs, such as CFF Explorer VIII, to edit
		   the game file and add "xinput_modkey.dll" into its import table.



Manual Uninstall
----------------------------

	1. Go to the game/pogram directory and locate files that start with
	   "xinput" text, for example "xinput1_3.dll".
	2. Open file properties and go to the Details tab.
	3. If the column named "File descriptopm" says
	   "Xinput Modkey - Forwarder DLL", then delete this file.
	4. Delete file named "xinput_modkey.dll".



Logging Configuration
----------------------------
	
	By default no log information is saved.
	
	It can be enabled by creating empty "xinput_modkey.log" file
	in one of the following 2 locations:
		
		1. The same directory where the "xinput_modkey.dll" file is.
		2. The "C:\Temp" directory.
	
	First file that exitst is used. Otherwise logging is disabled.

	The log will contain information such as:
	
		* Names of EXE and DLL files used.
		* Any configuration errors that were detected when parsing the INI file.



Build instructions
--------------------------

	Instructions for building filter DLL only.
	Instructions for building forwarder DLL not provided. They should be standard, deduced from the source code.

	Software needed:

	* MS Visual C++ Compiler   - tested with Visual Studio
	                             2017 (aka. MSVC2017), should work with
	                             older versions.

	* Windows SDK              - tested with v7.1 (typically, install
	                             Windows SDK with MSVC).

	* Detours Software Package - tested with v4.0.1.


	Source code must be compiled separatelly for 32 and 64-bit
	Windows architectures.

	Use the following compile time options:

		/EHsc
		/Os
		/O1
		/D WIN32_LEAN_AND_MEAN
		/D _WIN32_WINNT=0x501
		/D HXDW_NO_ADVAPI32_LIB
		/D HXDW_NO_GDI32_LIB
		/D HXDW_NO_SHELL32_LIB


	Use the following link time options:

		/dll



How to check if a file is 32-bit or 64-bit
---------------------------------------------

	Other than using a third party application that can do this,
	following method can be used:

		1. Right-click on the executable file you want to check
		2. Select “Properties”
		3. Click the tab “Compatibility” tab
		4. In the section "Compatibility mode" put a check in the box under
		   "Run this program in compatibility mode for"
		5. Open the drop-down menu that lists operating systems.
		   If the list of operating systems includes Windows XP, then the
		   file is 32-bit, otherwise it's 64-bit.
		6. Press Cancel to Close “Properties".

		Tested on Windows 7 and Windows 10.

		Reference: https://www.techsupportalert.com/content/how-find-out-if-program-or-executable-file-64-bit-or-32-bit.htm



Changelog
----------------------

	v1.1

		* Initial release.
		* No GUI manager, only filter for mnual install.

	v1.2

		* Possibility to emulate mouse motion.
		* Can emulate keyboard keys and mouse buttons.
		* Thumbstick input interpreted as circular, rather than as square region.
		* Option to reinterpolate analogue inputs ("bADZReinterpolate").
		  Used with "bEnforceAPIDeadzones".

	v2.1

		* Application is now split into multiple projects.
		* GUI Application to manage installations.
		* Filter DLL.
		* Forwarder DLL.
		* Installer works with different architectures by
		  executing appropriate process that examines binary files.
		* Using FLTK GUI library.

	v2.2

		* Better compatibilty for keyboard simulated keys, enabled by INI
		  setting bKeysUseSC=1. Should be always used with games/programs
		  that use Direct Input to read keyboard states. (Note: this is only
		  for DInput keyboard not gamepad.)
		* Filter DLL INI file - better documentation.
		* Added startup sound that plays when Filter DLL is started.
		  Use INI bNoStartupSnd=1 to disable.
		* Fixes when parsing keyboard key names - added more key names.

	v2.3

		* Fix for dedzones implementation used with bEnforceAPIDeadzones=1.
		  Application recieves own values, rather than mixed with internal logic.
		* More precise mouse movement emulation. Possibly sub-pixel precision.
		* Ability to turn-off file logging, bNoLogFile=1 (NOTE: removed in later version).
		* Ability to enable Xinput for applications that doesn't use Xinput
		  at all (bXiEnabled=1 in "s_internal_xinput" section).

	v2.3.1

		* Routine auto-repeat option for gamepad buttons ('szAutoRepeat').
		* Routine disabling by 'bRDisabled' INI option.
	
	v2.3.2

		* Mouse wheel simulation. Mouse button names m4 and m5 correspond to wheel forward and back.
	
	v2.4.1
	
		* Improvements for loading filter DLL on Windows 10.
		* Option to show message box on startup that provides simple visual notification. INI value name: bShowStartupMBox=1.
		  Note that this itself pauses the initialization and may crash the application.
		* Option to delay initialization of the DLL by time in milliseconds.
		  INI value name: nInitDelayMs=4000 (eg.: 1000 stands for 1 second).
		* Removed GUI Manager from the project. Use the manager from older version or install manually.

	v2.5.1
		
		* Added configuration reset hotkey. 
		  INI value name: 'szReinitHotkey' in the "[s_main]" section.
		  Set to the following buttons, by default: LSh+RSh+BACK+Y (Left shoulder, Right shoulder, Back and Y).
		* Added macro functionality. A mini script that lists buttons and time intervals.
		  INI value name: 'szMacroScr' in the routine ("[routine:#]") section.
		* Macro: added option to specify what to do when macro activates again.
		  INI value name: 'szMBubbleAction' (in the routine section).
		* Macro: added option to play system asterisk notification when macro starts and/or stops.
		  INI value names: "bMBAsterisk" and "bMEAsterisk" (in the routine section).
		* Removed INI configuration: "bNoLogFile".
		  User control of where to save the log has been changed.
		  Please the "Logging Configuration" section.
		  


Online Resources
----------------------

	Project Website:
	https://github.com/ike9000e/Xinput-Modkey

	CFF Explorer VII and Explorer Suite:
	https://ntcore.com/?page_id=388

	Detours software package:
	https://github.com/Microsoft/Detours

	Guide - Attach DLL to Archive.exe using CFF Explorer VII
	https://www.nexusmods.com/skyrimspecialedition/articles/927
