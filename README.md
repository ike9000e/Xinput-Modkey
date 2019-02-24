
 Xinput Modkey
==========================

	Modkeys and hotkeys for gamepad buttons in games that use Xinput.
	Windows 32 and 64-bit architectures.

	Xinput Modkey is a DLL file that needs to be attached to the
	target process durning its startup.

	Configurable through INI file located in the same
	directory the game and the DLL is in.


Using Filter DLL
------------------------

	Copy "xinput_modkey.dll" and "xinput_modkey.ini" into the same
	directory the target game executable file (.exe) is located in.
	DLL architecture must be the same as the game.
	Use one of following methods to start the game.

	How to start game process with DLL module attached?
	-------------------------------------------------------

		Possible ways to do this:

		1. Use the loader program to start the game executable with
		   desired DLL module attached to it, in this case "xinput_modkey.dll".

		2. Use PE editor programs, such as CFF Explorer VIII, to edit
		   the game file and add "xinput_modkey.dll" into its import table.

		3. Use Xinput DLL file wrapper named "xinput1_3.dll" - copy it into
		   the game directory and edit its inport table; the same way as
		   described in #2.


Build instructions
--------------------------

	Software used:
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

	Use the following link time options:

		/dll


How to check if a file is 32-bit or 64-bit
---------------------------------------------

	1. Right-click on the executable file you want to check
	2. Select “Properties”
	3. Click the tab “Compatibility”
	4. In the section "Compatibility mode" put a check in the box under
	   "Run this program in compatibility mode for"
	5. Open the drop-down menu that lists operating systems.
	   If the list of operating systems includes Windows XP, then the
	   file is 32-bit, otherwise it's 64-bit.
	6. Press Cancel to Close “Properties".

	Reference: https://www.techsupportalert.com/content/how-find-out-if-program-or-executable-file-64-bit-or-32-bit.htm

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

