## 7\. Updating the Menu: Numeric Entry {#7-updating-the-menu-numeric-entry}

In this lab, you’ll learn how to add a numeric entry to your driver menu. This lab uses the VFR term “numeric” that prompts the user to enter a free-form numeric value. The VFR determines the minimum and maximum values with the terms “minimum” and “maximum”. Since there is also an enable/disable switch, the VFR uses the “suppressif” term to display or hide this field when disabled. Also this field displays as decimal (default) or hexadecimal with the “flags” switch.

Figure 7 : Menu with Numeric item entry

| **Step** | **Action** |
| --- | --- |
|  | **Update** the MyWizardDriver.vfr file |
|  | **Add** the following code in the location shown below at approx. Line 90 and before the “resetbutton” item: |
|  | **//** |
|  |  |
|  | **Save** MyWizardDriver.vfr |
|  | **Update** the MyWizardDriver.uni file |
|  | **Add** the following code to the bottom of the file: |
|  | #string STR_DATA_HEX_PROMPT #language en &quot;Enter ZY Base (Hex)&quot; |
|  | **Save** MyWizardDriver.uni |
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