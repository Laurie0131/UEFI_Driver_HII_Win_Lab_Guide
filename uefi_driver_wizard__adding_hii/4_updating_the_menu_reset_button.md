## 4\. Updating the Menu: Reset Button {#4-updating-the-menu-reset-button}

In this lab, you’ll learn how to add a resetbutton to your driver’s form menu. It’s time to add more configuration fields to your menu, enabling users to modify more fields now that you’ve built a driver that 1) saves data from forms into NVRAM 2) updates data from the .VFR forms and 3) builds into the platform drivers.

The next set of labs will update .VFR, MyWizardDriver.vfr, and UNI MyWizardDriver.uni string files to incrementally add a reset button (Lab 4), pop-up box (Lab 5), string name (Lab 6), and numeric hex value (Lab 7) to your driver’s form menu:

| **Step** | **Action** |
| --- | --- |
|  | **Update** the MyWizardDriver.vfr file |
|  | **Add** the following code (as shown below after the “GUID” definition Apprx. Line 29): |
|  | defaultstore MyStandardDefault, |
|  |  |
|  | **Add** the folowing code before the “endform” (as shown below Approx. Line 55): |
|  | resetbutton |
|  |  |
|  | **Save** MyWizardDriver.vfr |
|  | **Update** the MyWizardDriver.uni file |
|  | **Add** the following strings at the end of the file to support the “**STR_**“ referenced added in the .vfr file: |
|  | #string STR_STANDARD_DEFAULT_PROMPT #language en &quot;Standard Default&quot; |
|  | **Save** MyWizardDriver.uni |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | Now at the setup front page menu press the **down arrow** to **“Device Manager”** |
|  | **Press** “Enter” |
|  | Inside the Device Manager menu press the down arrow to **“My Wizard Driver Sample Formset”** |
|  | **Access** the My Wizard Driver menu and **notice** the item “Reset to Standard Default” |
|  | **Press Down Arrow to “**Reset to Standard Default” |
|  | **Press** “Enter |
|  | **Notice** the “**Configuration changed**” message at the bottom of the menu |
|  | **To Exit Press** “Escape” then “Y” |
|  | **To Exit the “Device Manager” Page: Press** “Escape” |
|  | **Press** Up Arrow to **“**Continue**”** |
|  | **Observe:** Notice that since this change requires a reset, the Nt32 will exit out completely. |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.4

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.