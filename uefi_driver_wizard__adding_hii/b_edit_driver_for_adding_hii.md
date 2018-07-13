## b. Edit Driver for adding HII {#b-edit-driver-for-adding-hii}

| Step | Action |
| --- | --- |
|  | **Open** C:\fw\edk2\MyWizardDriver |
|  | **Open** the following files for updating: |
|  | **Update** the MyWizardDriverNVDataStruc.h file by copying and pasting the following GUID as shown below: |
|  | #define MYWIZARDDRIVER_FORMSET_GUID \ |
|  |  |
|  | **Save** MyWizardDriverNVDataStruc.h |
|  | **Update** the **MyWizardDriver.vfr** file. **Delete** its contents and **replace** it with the following by copying and pasting: |
|  | #include &quot;MyWizardDriverNVDataStruc.h&quot; |
|  | Continue **adding** the remaining code to MyWizardDriver.vfr. |
|  | form formid = 1, title = STRING_TOKEN(STR_SAMPLE_FORM1_TITLE); |
|  | **Save** MyWizardDriver.vfr |
|  | Now onto the MyWizardDriver.uni file. You’ll add new strings to support the forms. **Delete** the file’s content and **replace** it with the following by copying and pasting: |
|  | #langdef en &quot;English&quot; |
|  | **Save** MyWizardDriver.uni |
|  | Now update the MyWizardDriver.h file. **Add** the following HII libraries starting at approximately line 41 (as shown below) by copying and pasting: |
|  | // Added for HII |
|  |  |
|  | To add a data structure for HII routing and access, **add** the following code at approximately line 75 by copying and pasting after the “extern” statements: |
|  | #define MYWIZARDDRIVER_DEV_SIGNATURE SIGNATURE_32 (&#039;m&#039;, &#039;w&#039;, &#039;d&#039;, &#039;r&#039;) |
|  |  |
|  | **Save** MyWizardDriver.h |
|  | Now onto the MyWizardDriver.c file. |
|  | //HII support |
|  | **Locate** EFI_STATUS within the function MyWizardDriverDriverEntryPoint in the MyWizardDriver.c file (approx. Line 184) and **add** HII local definitions by copying and pasting (as shown below): |
|  | // HII Locals |
|  |  |
|  | **Locate** the **ASSERT_EFI_ERROR (Status);** statement and the line: **// Retrieve HII Package List Header on ImageHandle** (approximately line 202). Now, **add** the following code to install the configuration access protocol (produced) by copying and pasting (as shown below) before the line:**// Retrieve HII Package List Header on ImageHandle** |
|  | // |
|  |  |
|  | Next, **add** code to register a list of HII packages in the HII Database with the HII device path. This requires you to **replace** existing code (see below) by copying and pasting the new code at approx. line 265. |
|  | **Old Code** |
|  | mDriverHandle[0], |
|  | **New Code** |
|  | Next, you’ll **add** code to initialize the My Wizard Driver NVRAM variable by copying and pasting the following code **before** the // Install Driver Supported EFI Version Protocol onto ImageHandle comment (as shown below at approximately line 273): |
|  | PrivateData-&gt;HiiHandle[0] = HiiHandle[0]; |
|  |  |
|  | **Save** MyWizardDriver.c |
|  | Now onto the final file, MyWizardDriver.inf. **Add** the following protocols in the [protocols] section that are being used by copying and pasting (as shown below): |
|  | gEfiHiiStringProtocolGuid ## CONSUMES |
|  |  |
|  | **Save** the MyWizardDriver.inf file. All the files should be saved at this point. |
|  | **Re-Open** the Visual Studio Command Prompt |
|  | **Add** MyWizardDriver.inf to the Nt32Pkg.dsc(See Lab 2building MyWizardDriver from the Driver Porting Lab) |
|  | **Type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **At the UEFI Shell prompt,type** fs0: |
|  | **Press** “Enter” |
|  | **Type** Load MyWizardDriver.efi |
|  | **Press** “Enter” This will load your driver into memory |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | ****Now at the setup front page menu,** select **“Device Manager”**** |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu** press **the down to “My Wizard Driver Sample Formset”**** |
|  | **_Note_:** Notice that your form is now displayed with a choice to enable your device. Also notice the titles and help strings that are in the .UNI file you edited. |
|  | **Press** the space bar to Enable and Disable the “Enable My XYZ Device” |
|  | **Press** F10 to attempt to save |
|  | **Press **“Enter”**** |
|  | **Press **“Escape”, and then “Y” to exit**** |
|  | ****To Exit the “Device Manager” Page: Press “Escape”**** |
|  | **Press **Up Arrow to “Continue”**** |
|  | **Press** “Enter” |
|  | ****At the Shell prompt** type **Reset**** |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

You’ve completed the first lab and added strings and forms to setup HII for user configuration. However, **the data is not saved to NVRAM**. In the next lab, you’ll learn how to update HII to save data to NVRAM.

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.1A