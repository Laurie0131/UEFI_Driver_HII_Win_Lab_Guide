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
## 11\. Adding Communication from Driver to Console through HII {#11-adding-communication-from-driver-to-console-through-hii}

In this lab, you’ll add communication from the driver to the console through HII. More specifically, you’ll add code to retrieve a string from the HII database and print the string to the console. Then, you’ll add the string in French, change the language, and test to ensure the correct language is displayed. The reason the driver should avoid direct string text to the console without the HII support is because there is no localization for text string inside the driver’s source code. By using the HII database the strings are tokenized making localization easier.

| **Step** | **Action** |
| --- | --- |
|  | For HII database library functions open the MdeModulePkg .Chm file and search on HiiLib.h functions |
|  | Select the Index tab |
|  | Type: HiiLib.h |
|  | **_Note_**: Notice the list of Hii function calls available. To get Strings the HiiGetString function can be used. |
|  | **Update** the C:\Fw\edk2\Nt32pkg\Nt32pkg.fdf file |
|  | Make your driver stand alone. **Remove** (or comment out) the include statement in the Nt32pkg.fdf file: |
|  | #INF MyWizardDriver/MyWizardDriver.inf |
|  |  |
|  | **Save** Nt32pkg.fdf |
|  | **Update** the MyWizardDriver.uni file |
|  | Add the following code to the top of the file at approx. line 14 as shown: |
|  | #langdef fr-FR &quot;Francais&quot; |
|  |  |
|  | Add the following code to the end of the file: |
|  | #string STR_LANGUAGE_TEST_STRING #language en &quot;Laurie&#039;s Test String&quot; |
|  |  |
|  | **Save** MyWizardDriver.uni |
|  | **Update** the MyWizardDriver.c file |
|  | **Add** the following local variable for StringPtr after “BOOLEAN ActionFlag;” and before “Status = EFI_SUCCESS;”(as shown below): |
|  | EFI_STRING StringPtr; |
|  |  |
|  | Add the following code after “FreePool (ConfigRequestHdr);” (as shown below) to edit the driver’s entry point with a debug and print statement by making a call to the HiiGetString for the token to print (at approx line 364): |
|  | StringPtr = HiiGetString (HiiHandle[0], STRING_TOKEN (STR_LANGUAGE_TEST_STRING), NULL); |
|  |  |
|  | **Save** the MyWizardDriver.c |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** Fs0: |
|  | **Press** “Enter” |
|  | **Type** load MyWizardDriver.efi and notice that the string’s English version is displayed: |
|  | **Type** Reset |
|  | **Press** “Enter” |
|  | **Type** build |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type exit** at the shell prompt |
|  | **Select Language** |
|  | **Press** “Enter” |
|  | **Select** “Français” |
|  | **Press** “Enter” |
|  | **Select** “Continuer” |
|  | **Press** “Enter” |
|  | At the Shell Prompt, **type** Fs0: |
|  | **Type** load MyWizardDriver.efi |
|  | **Type “reset”** |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.11

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.

Make sure you update Nt32Pkg.fdf.