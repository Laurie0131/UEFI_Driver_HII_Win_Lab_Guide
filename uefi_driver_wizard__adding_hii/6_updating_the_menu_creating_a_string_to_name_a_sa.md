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
## 6\. Updating the Menu: Creating a String to Name a Saved Configuration {#6-updating-the-menu-creating-a-string-to-name-a-saved-configuration}

In this lab, you’ll create a string to name a saved configuration that will be stored into the NVRAM variable space. This lab uses the VFR term “string” to prompt the user to enter a string value. The VFR can determine the minimum and maximum number of characters of the string length with the terms “minsize” and “maxsize”. Since there is also an enable/disable switch, the VFR can use the “grayoutif” term again to allow or disallow changes to this field.

Figure 6 : Menu with a string item

| Step | Action |
| --- | --- |
|  | **Update** the MyWizardDriver.vfr file |
|  | **Add** the following code to the location at approx. line 77 and before the “resetbutton” item (as shown below): |
|  | // |
|  |  |
|  | **Save** MyWizardDriver.vfr |
|  | **Update** MyWizardDriver.uni |
|  | **Add** the following code to the bottom of the file: |
|  | #string STR_MY_STRING_PROMPT #language en &quot;Name of Configuration&quot; |
|  |  |
|  | **Save** MyWizardDriver.uni |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | ****Now at the setup front page menu,** select “Device Manager”** |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu,** select**“My Wizard Driver Sample Formset” |
|  | **Select **“Name of Configuration”**** |
|  | **Press** “Enter” |
|  | **Notice **the string text pop up menu gets displayed**** |
|  | **Test** the “minsize” by only **typing** your choice of a two character string. |
|  | **Press** “Enter” |
|  | **Press** “Enter” to clear the message |
|  | **Press** “Enter” again to re-enter pop up menu |
|  | **Test **by** typing **more than “maxsize” of 20 characters**** |
|  | **Press** “Enter” |
|  | **Test** the grayoutif ****by** selecting **“Enable My XYZ Device”**** |
|  | ****Press the “Spacebar” to toggle off/disable**** |
|  | **Press **“Space” again to Enable**** |
|  | **Press **“F10” to save**** |
|  | **Press **“Escape” to exit**** |
|  | **Press **“Escape”** **to exit the “Device Manager”**** |
|  | **Select “**Continue**”** |
|  | **Press **“Enter”**** |
|  | At the Shell Prompt, **type dmpstore -all** |
|  |  |
|  | **Type “reset” **at the Shell prompt**** |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.6

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.