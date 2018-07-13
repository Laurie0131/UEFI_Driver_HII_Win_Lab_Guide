<!--- @file
 README.md file for Lab_setup

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
# Lab Setup {#lab-setup}

| **Step** | Action |
| --- | --- |
|  | Download the [UEFI Training Materials](https://github.com/Laurie0131/Lab_Material_FW) (accept any security notifications) |
|  | **Click** “Open” |
|  | Unzip the file to C: which will take a few minutes |
|  | Copy the C:\fw\NASM directory to C: |

### Pin Visual Studio Command Prompt for Windows {#pin-visual-studio-command-prompt-for-windows}

| **Step** | **Action** |
| --- | --- |
|  | Visual Studio Command Prompt for [Windows](../microsoft_windows_10__visual_studio_command_prompt.md) 10 |
|  | **Pin “Visual Studio Command Prompt (201_n_)”** to the Task bar |

### Preparing for the BUILD Command {#preparing-for-the-build-command}

**_Note_**_: You’ll need to repeat this step each time you exit the Visual Studio Command Prompt window. It is recommended that you keep your command prompt open during the training._

| **Step** | **Action** |
| --- | --- |
| **4** | **Open** Visual Studio Command Prompt |
|  | **Type CD c:\fw\edk2** |
|  | Press “Enter” |
|  | **Type edksetup** |
|  | Press “Enter” |

### Configuring Build Tools {#configuring-build-tools}

**_Note_**_: You only need to edit Target.txt and/or Tools_Def.txt once after the first_ **edksetup** _command after downloading the Training materials .zip file._

| **Step** | **Action** |
| --- | --- |
|  | **Open** Notepad or other text editor that supports UNICODE |
|  | **Open** C:/fw/edk2/Conf/Target.txt |
|  |  |