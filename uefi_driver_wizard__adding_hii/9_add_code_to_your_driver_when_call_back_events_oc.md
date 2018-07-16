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
## Lab 9\. Add code to your driver when Call Back events occur for Interactive Items {#9-add-code-to-your-driver-when-call-back-events-occur-for-interactive-items}

In this lab, you’ll update your driver to print debug statements when the Hii browser engine calls back into your call back function. Every time the browser does anything with the interactive labeled fields there is a call made to your driver’s call back function. We can determine the item by the `quetionid` and what action based on the action passed to your call back function. Your call back function can then add code to special case when these transitions occur.

For this lab we will simply add Debug print statements. However, the use of adding call backs to a driver’s HII functions adds the capability of providing more manageability and flexibility for the interactions between the user, the browser engine, and your driver code. In a real driver firmware situation, it may be desired to implement more complex features and functionality based upon an item changing.

| Step | Action |
| --- | --- |
|  | **Update** the HiiConfigAccess.c file |
|  | **Comment** **out** the DEBUG statement with “//” in the MyWizardDriverHiiConfigAccessCallback call back function approx. line 330: |
|  | **//** |
|  |  |
|  | **Add** a switch case statement of the question ID’s to the “Action” switch case of EFI_BROWSER_ACTION_CHANGING in the call back function by **adding** a nested switch case code (as shown below at approx. line 372 ) |
|  | switch (QuestionId) { |
|  |  |
|  | **Add** another nested switch case statement of the question ID’s to the “Action” switch case of EFI_BROWSER_ACTION_CHANGED in the call back function (as show below at approx. line 388): |
|  | switch (QuestionId) { |
|  |  |
|  | **Save** MyWizardDriver.c |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | ****Now at the setup front page menu,** select** “Device Manager” |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu,** select**“My Wizard Driver Sample Formset” |
|  | **Press** “Enter” |
|  | **Observe **the Visual Studio Command Prompt – build run Window**** |
|  | **Switch back **to Visual Studio and notice the changes that you made.**** |
|  | **Notice: **when changing the “**Name of Configuration**” field**** |
|  | **Notice: **when changing the “**Enter ZY Base(Hex)**” field**** |
|  | **Notice: **when Pressing “F10”**** |
|  | **Press **“Escape” to exit**** |
|  | **Press **“Escape” to exit the “Device Manager”**** |
|  | **Select “**Continue**”** |
|  | **Press** “Enter” |
|  | **Type** “reset” ****at the Shell prompt**** |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

---
For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.9

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.

### End of Lab 9