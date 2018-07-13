## 10\. Adding an Additional Form Page {#10-adding-an-additional-form-page}

In this lab, you’ll learn how to add another form page to your My Wizard Driver menu by using the “goto” VFR term along with the “form” and “formid” VFR statements. Additionally, use “surpressif” or “grayoutif” to conditionally allow the user to enter your additional forms.

In addition, this lab will show how the “time” and “date” VFR terms are used within the VFR language to special case how the browser engine checks the time instead of your driver manually checking (e.g. leap year).

Figure 10: Second setup page

| Step | Action |
| --- | --- |
|  | **Update** the MyWizardDriverNVDataStruc.h file |
|  | **Add** the following date and time fields to the configuration typedef (to to the location shown below): |
|  | EFI_HII_TIME Time; |
|  |  |
|  | **Save** MyWizardDriverNVDataStruc.h |
|  | **Update** the MyWizardDriver.uni file |
|  | **Add** the following code to the end of the file to update the second page’s string: |
|  | #string STR_FORM2_TITLE #language en &quot;MyWizardDriver Second Setup Page&quot; |
|  | **Save** MyWizardDriver.uni |
|  | **Update** the MyWizardDriver.vfr file |
|  | **Add** the “goto” VFR item to allow browser to ender another form by adding the following code before the &quot;**endform”** at approx. line 114 |
|  | grayoutif ideqval MWD_IfrNVData.MyWizardDriverChooseToEnable == 0x0; |
|  |  |
|  | **Add** the following code between “**endform”** at approx. line 120 and “**endformset”** (the code continues for three pages in this lab guide): |
|  | form formid = 2, // SecondSetupPage, |
|  | grayoutif TRUE; // TIME – WINDOWS TIME |
|  | date // My Wizard Driver Date |
|  | **Save** MyWizardDriver.vfr |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | ****Now at the setup front page menu,** select **“Device Manager”**** |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu,** select **“My Wizard Driver Sample Formset”**** |
|  | **Press** “Enter” |
|  | **Select** “Enter Page 2” |
|  | **Press** “Enter” |
|  | **Test **by trying to enter the date 02/30/2013, then try a valid leap year date: 02/29/2012.**** |
|  | **Press** “Down Arrow” to return to Page 1 |
|  | ****Test the “grayoutif” by going to “Enable My XYZ Device”**** |
|  | ****Press the “Spacebar” to toggle off/disable**** |
|  | **Notice **the**** “Select Base Address” , “Name of Configruation” and the “Enter Page 2” ****fields are now grayed out and not selectable**** |
|  | **Press **“Space bar” again to Enable**** |
|  | **Press **“F10” then “Escape” to save and exit**** |
|  | **Press **“Escape” to exit “Device Manager”**** |
|  | **Select “**Continue**”** |
|  | **Press** “Enter” |
|  | **Type** “reset” |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.10

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.