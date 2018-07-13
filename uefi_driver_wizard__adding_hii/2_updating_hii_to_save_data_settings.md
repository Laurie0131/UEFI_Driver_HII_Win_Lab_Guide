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

## 2\. Updating HII to Save Data Settings {#2-updating-hii-to-save-data-settings}

In this lab, you’ll learn how to modify and update your driver’s HII code to save the users settings into NVRAM. The UEFI Driver Wizard created the protocols for your driver to update and interface with the HII browser engine and database. The HII configuration access Protocol functions for MyWizardDriver are in the file C:\fw\edk2\MyWizardDriver\HiiConfigAccess.c. This next lab will install these protocols and update them to save the user data from the HII menus into NVRAM.

1. **Update** the` MyWizardDriver.c `file <BR> Your driver will need to keep track of the consumed protocols in it’s own data structure so it will need to declare local pointers to these and then store them in its own private context data structure.
2. **Add** the following local variable declarations in the function `MyWizardDriverDriverEntryPoint` Entry Point (as shown below Approx. line 185 ): 
```
EFI_HII_STRING_PROTOCOL         *HiiString;
EFI_FORM_BROWSER2_PROTOCOL      *FormBrowser2;
EFI_HII_CONFIG_ROUTING_PROTOCOL *HiiConfigRouting;
```
![](/media/image27.png)
3. **Add** the following code to locate and store consumed protocols **before** the `// Publish sample Fromset and config access`  comment (as shown below Approx. line 227): <br> The reason is to Locate the Hii Database, Hii String, Hii Form browser and config routing protocols and store their pointers into the Private context data structure for your driver to access.

```
//Begin code
 //
  // Locate Hii Database protocol
  //
  Status = gBS->LocateProtocol (&gEfiHiiDatabaseProtocolGuid, NULL, (VOID **) &HiiDatabase);
  if (EFI_ERROR (Status)) {
    return Status;
  }
  PrivateData->HiiDatabase = HiiDatabase;

  //
  // Locate HiiString protocol
  //
  Status = gBS->LocateProtocol (&gEfiHiiStringProtocolGuid, NULL, (VOID **) &HiiString);
  if (EFI_ERROR (Status)) {
    return Status;
  }
  PrivateData->HiiString = HiiString;
  
  //
  // Locate Formbrowser2 protocol
  //
  Status = gBS->LocateProtocol (&gEfiFormBrowser2ProtocolGuid, NULL, (VOID **) &FormBrowser2);
  if (EFI_ERROR (Status)) {
    return Status;
  }
  PrivateData->FormBrowser2 = FormBrowser2;
  
  //
  // Locate ConfigRouting protocol
  //
  Status = gBS->LocateProtocol (&gEfiHiiConfigRoutingProtocolGuid, NULL, (VOID **) &HiiConfigRouting);
  if (EFI_ERROR (Status)) {
    return Status;
  }
  PrivateData->HiiConfigRouting = HiiConfigRouting;

//End code
```
![](/media/image28.png)
4. Since the Hii Database Protocol was located earlier in the code with the previous code insertion and is no longer necessary,** comment out **the old OpenProtocol code with the “`//`” (approx. lines 289-298, as shown below) and** add the comment **"`//`" Done above <br> Make sure not to comment out the second “` if (!EFI_ERROR (Status)) {`”
![](/media/image29.png)<br> **Note**:  The earlier `LocateProtocol` code already found the pointer to the Hii Database protocol and stored it to the local pointer variable `HiiDatabase`. <br> When we added the driver-consumed protocols, we searched via `LocateProtocol` for the Hii Database pointer function. Since we did it above we’re now commenting out this code.
5. **Comment out** the matching “`}`” with “`//`” to the if statement (as shown below at approx. line 310): 
![](/media/image30.png)
6. **Save** MyWizardDriver.c
|  | **Open** C:\fw\edk2\MyWizardDriver\HiiConfigAccess.c**.** |
|  | **Add** the following extern statements for the form GUID and the NVRam variable (as shown below) these are global to the driver module only hence the beginning lower case “m” is the standard for a global for a module : |
|  | extern EFI_GUID mMyWizardDriverFormSetGuid; |
|  |  |
|  | **Locate** MyWizardDriverHiiConfigAccessExtractConfig and **replace** line 108, “**return EFI_NOT_FOUND**”, with the following code spread over **two** pages: |
|  | FROM: TO: |
|  | EFI_STATUS Status; |
|  | if (EFI_ERROR (Status)) { |
|  | Now **locate** MyWizardDriverHiiConfigAccessRouteConfigand **replace** line at approx. 228, “**return EFI_NOT_FOUND**”, with the following code: |
|  | FROM: TO: |
|  | **EFI_STATUS Status;** |
|  | Lastly**, locate** MyWizardDriverHiiConfigAccessCallback and **replace **at approx.**** line 326, “**return EFI_UNSUPPORTED**;”, with the following code: |
|  | FROM: TO: |
|  | MYWIZARDDRIVER_DEV *PrivateData; |
|  | **Save** HiiConfigAccess.c |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **At the UEFI Shell prompt, type** fs0: |
|  | **Press** “Enter” |
|  | **Type** Load MyWizardDriver.efi |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | **Now at the setup front page menu press the down arrow to “Device Manager”** |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu** select **“My Wizard Driver Sample Formset”**** |
|  | **Press** “Enter” . |
|  | **_Note_**: Once you hit “Enter”, notice that your form is now displayed with a choice to enable your Device. Also notice the titles and help strings that are in the .UNI file you edited. |
|  | Test by **Press** the space bar to Enable and Disable the “Enable My XYZ Device” to change its value from**:** [X] to [ ] |
|  | **Note**: Notice the “Configuration changed” message at the menu bottom. |
|  | **Press** “F10” |
|  | **Press **“Escape” to exit**** |
|  | **Press **“Escape” to exit** **the “Device Manager” Page**** |
|  | **Press **Up Arrow to “Continue”**** |
|  | **Press** “Enter” |
|  | ****At the Shell Prompt** type **dmpstore -all**** |
|  | **Notice** that enable is selected and saved in NVRam as the value of 0x00: |
|  | **Type** Reset |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.2

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean