<!--- @file
 file b-edit-driver-for-adding-hii


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
## b. Edit Driver for adding HII {#b-edit-driver-for-adding-hii}

1. **Open** C:\fw\edk2\MyWizardDriver 
2. **Open** the following files for updating: 
  -  MyWizardDriverNVDataStruc.h
  - MyWizardDriver.vfr
  - MyWizardDriver.uni
  - MyWizardDriver.h
  - MyWizardDriver.c
  - MyWizardDriver.inf
3.  **Update** the MyWizardDriverNVDataStruc.h file by copying and pasting the following GUID as shown below: This GUID is used to communicate to the HII Database and Browser Engine
```c
  #define MYWIZARDDRIVER_FORMSET_GUID \
  { \
0x5481db09, 0xe5f7, 0x4158, 0xa5, 0xc5, 0x2d, 0xbe, 0xa4, 0x95, 0x34, 0xff \
}
```
![](/media/image8.png)
4. **Save** MyWizardDriverNVDataStruc.h 
5. **Update** the **MyWizardDriver.vfr** file. **Delete** its contents and **replace** it with the following by copying and pasting: You’re adding a reference to the GUID and to the NVRAM storage where the configuration will be saved. In fact, you’re replacing most of the original .vfr.
```
#include "MyWizardDriverNVDataStruc.h"
formset
  guid     = MYWIZARDDRIVER_FORMSET_GUID,
  title    = STRING_TOKEN(STR_SAMPLE_FORM_SET_TITLE),
  help     = STRING_TOKEN(STR_SAMPLE_FORM_SET_HELP),
  classguid = EFI_HII_PLATFORM_SETUP_FORMSET_GUID,

  //
  // Define a Buffer Storage (EFI_IFR_VARSTORE)
  //
    varstore MYWIZARDDRIVER_CONFIGURATION,  // This is the data structure type
    //varid = CONFIGURATION_VARSTORE_ID,      // Optional VarStore ID
    name  = MWD_IfrNVData,                  // Define referenced name in vfr
    guid  = MYWIZARDDRIVER_FORMSET_GUID;    // GUID of this buffer storage
```
6.  Continue **adding** the remaining code to MyWizardDriver.vfr. This is a Enable/ Disable question for the setup menu in the form of a Check box.
<pre>

 form formid = 1, title = STRING_TOKEN(STR_SAMPLE_FORM1_TITLE);
    subtitle text = STRING_TOKEN(STR_SUBTITLE_TEXT);

    subtitle text = STRING_TOKEN(STR_SUBTITLE_TEXT2);
 
  //
  // Define a checkbox to enable / disable the device
  //
      checkbox varid   = MWD_IfrNVData.MyWizardDriverChooseToEnable,
                 prompt   = STRING_TOKEN(STR_CHECK_BOX_PROMPT),
                 help     = STRING_TOKEN(STR_CHECK_BOX_HELP),
                 //
                 // CHECKBOX_DEFAULT indicate this checkbox is marked with 
	      //   EFI_IFR_CHECKBOX_DEFAULT
                 // 
                 flags    = CHECKBOX_DEFAULT ,
                 key      = 0,
                 default  = 1,
     endcheckbox;

   endform;

endformset;
</pre>
7. **Save** MyWizardDriver.vfr 
8. Now onto the MyWizardDriver.uni file. You’ll add new strings to support the forms. **Delete** the file’s content and **replace** it with the following by copying and pasting: 

```
  #langdef en "English"

  #string STR_SAMPLE_FORM_SET_TITLE      #language en  "My Wizard  Driver Sample Formset"
  #string STR_SAMPLE_FORM_SET_HELP       #language en  "Help for Sample Formset"
  #string STR_SAMPLE_FORM1_TITLE         #language en  "My Wizard Driver"

  #string STR_SUBTITLE_TEXT              #language en "My Wizard Driver Configuration"
  #string STR_SUBTITLE_TEXT2             #language en "Device XYZ Configuration"
  #string STR_CHECK_BOX_PROMPT           #language en "Enable My XYZ Device"
                                      
  #string STR_CHECK_BOX_HELP             #language en "This is the help message for the enable My XYZ device. Check this box to enable this device."

```
9. **Save** MyWizardDriver.uni 
10. Now update the MyWizardDriver.h file. **Add** the following HII libraries starting at approximately line 41 (as shown below) by copying and pasting: 


```
// Added for HII
#include <Protocol/HiiConfigRouting.h>  
#include <Protocol/FormBrowser2.h>  
#include <Protocol/HiiString.h> 
#include <Library/DevicePathLib.h>
```
![](/media/image9.png)

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
```

You’ve completed the first lab and added strings and forms to setup HII for user configuration. However, **the data is not saved to NVRAM**. In the next lab, you’ll learn how to update HII to save data to NVRAM.

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.1A