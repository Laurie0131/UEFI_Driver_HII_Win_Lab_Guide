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