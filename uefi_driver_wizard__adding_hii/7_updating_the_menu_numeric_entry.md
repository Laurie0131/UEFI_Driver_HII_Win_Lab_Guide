<!--- @file
 file

Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

Redistribution and use in source (original document form) and 'compiled'
forms (converted to PDF, epub, HTML and other formats) with or without
modification, are permitted provided that the following conditions are met:

1) Redistributions of source code (original document form) must retain the
above copyright notice, this list of conditions and the following
disclaimer as the first lines of this file unmodified.

2) Redistributions in compiled form (transformed to other DTDs, converted to
PDF, epub, HTML and other formats) must reproduce the above copyright
notice, this list of conditions and the following disclaimer in the
documentation and/or other materials provided with the distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
EVENT SHALL TIANOCORE PROJECT BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->
## Lab 7\. Updating the Menu: Numeric Entry {#7-updating-the-menu-numeric-entry}

In this lab, you’ll learn how to add a numeric entry to your driver menu. This lab uses the VFR term “numeric” that prompts the user to enter a free-form numeric value. The VFR determines the minimum and maximum values with the terms “minimum” and “maximum”. Since there is also an enable/disable switch, the VFR uses the “suppressif” term to display or hide this field when disabled. Also this field displays as decimal (default) or hexadecimal with the “flags” switch.
![](/media/image68.png)
###### Figure 7 : Menu with Numeric item entry

1. **Update** the MyWizardDriver.vfr file 
2.  **Add** the following code in the location shown below at approx. Line 90 and before the “`resetbutton`” item: 
```
//
// Define a numeric free form menu item 
//
  suppressif  ideqval MWD_IfrNVData.MyWizardDriverChooseToEnable == 0x0;
   numeric varid   = MWD_IfrNVData.MyWizardDriverHexData,                          
            prompt  = STRING_TOKEN(STR_DATA_HEX_PROMPT),
            help    = STRING_TOKEN(STR_NUMERIC_HELP),
            flags   = DISPLAY_UINT_HEX ,     // Display in HEX format (if not specified, default is in decimal format)
            minimum = 0,
```
PIC__69
3. **Save** MyWizardDriver.vfr 
4. **Update** the MyWizardDriver.uni file 
5. **Add** the following code to the bottom of the file: 

```
//Begin code
#string STR_DATA_HEX_PROMPT            #language en "Enter ZY Base (Hex)"

#string STR_NUMERIC_HELP               #language en "This is the help for entering a Base address in Hex. The valid range in this case is from 0 to 250."

//End code

```
6). **Save** MyWizardDriver.uni 



|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | Now at the setup front page menu, **select** “Device Manager” |
|  | **Press** “Enter” |
|  | Inside the Device Manager menu, **select** “My Wizard Driver Sample Formset” |
|  | **Select** “Enter ZY Base(Hex)” |
|  | **Press** “Enter” |
|  | **Test** by typing a “M” character |
|  | **Notice** that only Numeric characters are allowed and also only values 00 to 0FA Hex. When values outside the range or none numeric characters are entered the red **“!!”** sting is displayed at the bottom of the menu. |
|  | **Press** “Enter” again |
|  | **Test** by typing a value of ‘99’ Hex |
|  | **Press** “Enter” |
|  | **Test the “surpressif”** by pressing the “spacebar” to “Enable My XYZ Device” then press the “Space” bar to toggle off or “Disabled”. |
|  | **Notice the “Select Base Address” and “Name of Configuration”** fields are now grayed out and not selectable and the “**Enter ZY Base(Hex)**” does not appear at all. |
|  | **Press** “Space bar” again to “Enable My XYZ Device” and the“**Enter ZY Base(Hex)**” is displayed again |
|  | **Press** “F10” then “Escape” to exit |
|  | **Press** “Escape” to exit the “Device Manager” |
|  | **Select “**Continue**”** |
|  | **Press** “Enter” |
|  | At the Shell Prompt, **type** dmpstore –all |
|  | Notice by modifyingMyWizardDriverNVDataStruc.h our data structure stored in NVRAM is named **MWD_IfrNVData** of type MYWIZARDDRIVER_CONFIGURATION. |
|  | **Type “reset”** at the Shell prompt |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.7

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.