## 8\. Updating your Driver for Interactive Call Backs {#8-updating-your-driver-for-interactive-call-backs}

In this lab, you’ll update your driver for interactive call backs. Call backs are a way to communicate changes the user is making in “real time” where your driver needs to intervene as the changes are made and before the user exits the current menu being displayed. These would be exception cases that the driver could interrupt the normal browser engine process.

To add call backs, the file HiiConfigAccess.c of your driver will be updated in the function MyWizardDriverHiiConfigAccessCallback. This function is called whenever any VFR items have a flag for INTERACTIVE set. So far, the previous labs did not have any call back items.

We can see this because there was a “Debug” call made in the MyWizardDriverHiiConfigAccessCallback function that never gets called:

HiiConfigAccess.c (line 331)

DEBUG ((DEBUG_INFO, &quot;\n:: START Call back ,Question ID=0x%08x Type=0x%04x Action=0x%04x&quot;, QuestionId, Type, Action));

### _a._ Add the Case statements to the Call back routine {#a-add-the-case-statements-to-the-call-back-routine}

| **Step** | **Action** |
| --- | --- |
|  | **Update** the HiiConfigAccess.c file |
|  | **Add** the following code before return status; to include a “case” statement in the call back routine for the “action” passed. |
|  | switch (Action) { // Start switch and passed param Action |
|  |  |
|  | **Save** HiiConfigAccess.c |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | Now at the setup front page menu, **select** “Device Manager” |
|  | **Press** “Enter” |
|  | Inside the Device Manager menu, **select** “My Wizard Driver Sample Formset” |
|  | **Press** “Enter” |
|  | **Notice** the debug messages in the Visual Studio Command Prompt – build run Window (**No Debug messages for Call back**) |
|  | **Press** “Escape” to exit |
|  | **Press** “Escape”to exit the “Device Manager” |
|  | **Select “**Continue**”** |
|  | **Press** “Enter” |
|  | **Type** “reset”at the Shell prompt |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

### _b._ Update the Menu for Interactive items {#b-update-the-menu-for-interactive-items}

|  | **Update** the MyWizardDriver.vfr file |
| --- | --- |
|  | Now, you’ll add the flag characteristic INTERACTIVE to the string item’s flags by using keyword INTERACTIVE and questionid. **Add** the following code in the location shown below: |
|  | questionid = 0x1001, |
|  | flags = INTERACTIVE, |
|  |  |
|  | Include the numeric item by adding the following code in the location shown below, Approx. line 97 and line 100 |
|  | questionid = 0x1111, |
|  | | INTERACTIVE |
|  |  |
|  | **Save** MyWizardDriver.vfr |
|  | In the Visual Studio Command Prompt, **type** build |
|  | **Press** “Enter” |
|  | **Type** build run |
|  | **Press** “Enter” |
|  | **Type** exit |
|  | **Press** “Enter” |
|  | ****Now at the setup front page menu,** select** “Device Manager” |
|  | **Press** “Enter” |
|  | ****Inside the Device Manager menu,** select**“My Wizard Driver Sample Formset” |
|  | **Press** “Enter” |
|  | ****Take a moment and** review **the Visual Studio build run command prompt window**** |
|  | ****In the NT32 emulation window,** click **on “Name of Configuration” and “Enter ZY Base(Hex)”**** |
|  | **Notice **the following in the Visual Studio Command Prompt window:**** |
|  | **Press **“Escape” to exit**** |
|  | **Press **“Escape” to exit the “Device Manager”**** |
|  | **Select “**Continue**”** |
|  | **Press** “Enter” |
|  | **Type** “reset” ****at the Shell prompt**** |
|  | **Press** “Enter” to return to the Visual Studio Command Prompt |

For any build issues copy the solution files from C:\Fw\LabSolutions\LessonE.8

NOTE: Del Directory C:\fw\edk2\Build\NT32IA32\DEBUG_VS2010x86\IA32\MyWizardDriver before the Build command to build the MyWizardDriver Clean.