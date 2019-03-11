
Xinput Modkey
=============


	Modkeys and hotkeys for gamepad buttons in games that use Xinput.
	Comes with simple GUI Manager. Both Windows architectures,
	32 and 64-bit.

	With Xinput Modkey, following can be achieved:

	* Remap original gamepad buttons into other buttons.
	* Simulate keyboard keys with gamepad inputs.
	* Simulate mouse buttons.
	* Navigate with mouse cursor using analog thumbsticks.
	* Apply deadzones in games that doesn't do this. Default only.
	* Remap simultaneously pressed two or more gamepad buttons into:
	  * another gamepad button,
	  * keyboard key or
	  * mouse button.

	It's split into three main components:

	* Gui Manager
	* Filter DLL - configurable via INI file.
	* Forwarder DLL - enables non modyfying installations.

	In current version, configuration must be done manually,
	by editing configuration INI file. Please see self documented
	"documentated_xinput_modkey.ini" file.

	Filter DLL is a windows module file that needs to be attached to the
	target process durning its startup. This is the module that,
	once configured, works independently by starting itself every
	time the game/program starts.
	Unless it is desired to do this manually, GUI manager will
	attempt install procedure and will display any messages if something went wrong.
	Installation doesn't modify any of existing game files, namelly
	executables; It only copies two or more files off of which,
	one is a proxy that enables Xinput Modkey to be attached to the
	game/program every time it starts, untill uninstalled.
	For more details please see Manual Installation and Uninstallation below.



Using Filter DLL - Manual Install
--------------------------------------------------

	Determine architecture your target game/program executable (.exe).
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
		   to "xinput1_3.dll".

		2. Use the loader program to start the game executable with
		   desired DLL module attached to it, in this case "xinput_modkey.dll".

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




Build instructions
--------------------------

	Software needed:

	* MS Visual C++ Compiler   - tested with Visual Studio
	                             2017 (aka. MSVC2017), should work with
	                             older versions.

	* Windows SDK              - tested with v7.1 (typically, install
	                             Windows SDK with MSVC).

	* Detours Software Package - tested with v4.0.1.

	* FLTK Fast Light Tool Kit - tested with v1.3.5.


	Source code must be compiled separatelly for 32 and 64-bit
	Windows architectures.

	Use the following compile time options:

		/EHsc
		/Os
		/O1
		/D WIN32_LEAN_AND_MEAN
		/D _WIN32_WINNT=0x501

	Use the following link time options:

		/dll


How to check if a file is 32-bit or 64-bit
---------------------------------------------

	1. Right-click on the executable file you want to check
	2. Select ?Properties?
	3. Click the tab ?Compatibility?
	4. In the section "Compatibility mode" put a check in the box under
	   "Run this program in compatibility mode for"
	5. Open the drop-down menu that lists operating systems.
	   If the list of operating systems includes Windows XP, then the
	   file is 32-bit, otherwise it's 64-bit.
	6. Press Cancel to Close ?Properties".

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
		* Added startup sound that plays when Filter DLL gets loaded.
		  Use INI bNoStartupSnd=1 to disable.
		* Fixes when parsing keyboard key names - added more key names.



Online Resources
----------------------

	Project Website:
	https://github.com/ikk00/Xinput-Modkey

	CFF Explorer VII and Explorer Suite:
	https://ntcore.com/?page_id=388

	Detours software package:
	https://github.com/Microsoft/Detours

	Guide - Attach DLL to Archive.exe using CFF Explorer VII
	https://www.nexusmods.com/skyrimspecialedition/articles/927

	FLTK Fast Light Tool Kit
	https://www.fltk.org/

