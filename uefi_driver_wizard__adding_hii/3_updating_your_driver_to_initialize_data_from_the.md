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
## 3\. Updating your driver to initialize data from the VFR data to the HII Database {#3-updating-your-driver-to-initialize-data-from-the-vfr-data-to-the-hii-database}

In this lab, you’ll learn how to update your driver to initialize the data according to the defaults set in the .VFR file. Thus when the user enters your driver’s menu for the first time, the values will display the defaults according to the .VFR file settings. You will also learn the rich set of HII function calls that are part of the `MdeModulePkg` in the `HiiLib` by reviewing the “MdeModulePkg Document.chm”.

### _a._ Add HII Library Calls to Your Driver {#a-add-hii-library-calls-to-your-driver}

For this lab you will update the following files: MyWizardDriver.inf, MyWizardDriver.h, and MyWizardDriver.c
1. **Update** the MyWizardDriver.inf file 
2. **Add** the following package (as shown below):  <br>The HII Library in the MdeModulePkg has many functions to help with Communication to/from the Hii Database and Hii forms. One function call HiiSetToDefaults will compare the default settings from the .VFR file and update the driver’s configuration buffer according to the settings in the .VFR file.        <br>

```
MdeModulePkg/MdeModulePkg.dec

```
![](/media/image38.png)
**_Note_**: For other functions from the HII Library, open the .chm file “MdeModulePkg Document.chm” and search for `HiiLib.h`. 
3. **Add** the following library class (as shown below): <br>
`HiiLib` <br>
![](/media/image39.png)
4. **Save** MyWizardDriver.inf 
5. **Update** the MyWizardDriver.h file 
6. **Add** the following code (as shown below):                <br> `#include <Library/HiiLib.h>`<br>
![](/media/image40.png)
7. **Save** MyWizardDriver.h 
8. **Update** the MyWizardDriver.c file 
9. **Add Locals:** first add 2 locals for your drivers configuration buffer and a boolean flag from the Hii Library calls <br>Add the following at Approx. Line 190. 
`  MYWIZARDDRIVER_CONFIGURATION     *Configuration;`
`  BOOLEAN                          ActionFlag;`<br>
![](/media/image41.png)
10.  **Add** the following to the MyWizardDriverDriverEntryPoint entry point funtion to line 319, approximately after “`BufferSize =`” as shown below 
```
// Begin code
  
  //
  // Initialize configuration data
  //
  Configuration = &PrivateData->Configuration;
  ZeroMem (Configuration, sizeof (MYWIZARDDRIVER_CONFIGURATION));
  
  //
  // Try to read NV config EFI variable first
  //
  ConfigRequestHdr = HiiConstructConfigHdr (&mMyWizardDriverFormSetGuid, mIfrVariableName, mDriverHandle[0]);
  ASSERT (ConfigRequestHdr != NULL);
// End code
```
![](/media/image42.png)

|  | // |
|  |  |
|  | Modify the following lines: |
|  | **FROM TO** |
|  | **Add** the following code to the MyWizardDriverDriverEntryPoint entry point code at approximately line 349 before |
|  | // |
|  |  |
|  | Note the “}” on line 361 is still matching the initial if statement. Make sure you do not have a duplicate “}” |
|  | **Save** the MyWizardDriver.c file |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | At the UEFI Shell prompt, **type** fs0: |
|  | **Press** “Enter” |
|  | **Type** Load MyWizardDriver.efi |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | Now at the setup front page menu **select** “Device Manager” |
|  | **Press** “Enter” |
|  | Inside the Device Manager menu press the down arrow to **“My Wizard Driver Sample Formset”** |
|  | **Press** “Enter” . |
|  | **Press** “Escape” to exit |
|  | To Exit the “Device Manager” Page: **Press** “Escape” |
|  | **Press** Up Arrow to **“**Continue**”** |
|  | **Press** “Enter” |
|  | **Type** Reset |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.3

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean

### _b._ Add your Driver to the platform {#b-add-your-driver-to-the-platform}

As of now, your driver needs to be soft loaded each time from the shell prompt. In this lab, you’ll update the platform .FDF file to force your driver to load as part of the platform UEFI driver.

| **Step** |  |
| --- | --- |
|  | **Open **to update:**** C:\fw\edk2\Nt32PkgNt32Pkg.Fdf |
|  | INF MyWizardDriver/MyWizardDriver.inf |
|  | **Save** Nt32pkg.fdf |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
| 

 | **At the Shell prompt type: **exit**** |
|  | **Press** “Enter” |
|  | ****Now at the setup front page menu press the down arrow to** “Device Manager”** |
|  | **Press** “Enter” |
|  | **Notice** that the My Wizard Driver Sample Formset is added without having to issue the “Load” command from the shell prompt. |
|  | **Press **“Escape”**** |
|  | **Press **Up arrow to “Continue”**** |
|  | **Press “Enter”** |
|  | **Type** Reset |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |