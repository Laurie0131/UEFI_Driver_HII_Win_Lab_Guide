## 5\. Updating the Menu: Pop-up Box {#5-updating-the-menu-pop-up-box}

In this lab, you’ll learn how to add a _pop-up box_ to your driver’s form menu by using the “**oneof**” VFR term. We will also only update the MyWizardDriver.vfr and MyWizardDriver.uni files.

Figure 5 My Wizard Driver with a pop-up box

| Step | Action |
| --- | --- |
|  | **Illegal nested table :** ValueDisplayString token0500 HexSTR_ONE_OF_TEXT31480 HexSTR_ONE_OF_TEXT22400 HexSTR_ONE_OF_TEXT1 |
|  | **Update** the MyWizardDriver.vfr file |
|  | **Add** the following code before the “resetbutton” statement (approximately line 53) |
|  | // |
|  |  |
|  | **Save** the MyWizardDriver.vfr file |
|  | **Update** the MyWizardDriver.uni file |
|  | **Add** the following code to the end of the file (as shown below): |
|  | **#string STR_ONE_OF_PROMPT #language en &quot;Select Base Address&quot;** |
|  |  |
|  | **Save** MyWizardDriver.uni |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | ****Now at the setup front page menu press the** down arrow **to** “Device Manager”** |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu press the down arrow to** “My Wizard Driver Sample Formset”** |
|  | ****Down Arrow to “Select Base Address”**** |
|  | **Press** “Enter” **Notice** the Pop up menu |
|  | **Select** “480 Hex” |
|  | **Press** “Enter” |
|  | **Observe: **Notice the “**Configuration changed**” message at the bottom**** |
|  | ****Test the** “grayoutif” **by selecting “Enable My XYZ Device” then press the “Space” bar to toggle off or “Disabled”.**** |
|  | **Notice **the “Select Base Address”** **is now grayed out and not selectable**** |
|  | **Press **“Space” again to Enable**** |
|  | **To Exit Press **“Escape” then “Y” or “F10” then “Escape”**** |
|  | **To Exit the “Device Manager” Page: Press **“Escape”**** |
|  | **Press Up Arrow to “**Continue**”** |
|  | **At the Shell Prompt type: dmpstore -all** |
|  |  |
|  | File MyWizardDriverNVDataStruc.h |
|  | **Type “reset” **at the Shell prompt**** |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.5

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.