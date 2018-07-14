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

---

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.3

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean


#### End of Lab 3
