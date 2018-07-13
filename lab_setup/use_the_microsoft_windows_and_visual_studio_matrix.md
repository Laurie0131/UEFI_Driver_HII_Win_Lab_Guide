## Use the [Microsoft Windows and Visual Studio Matrix](../reference.md) {#use-the-microsoft-windows-and-visual-studio-matrix}

File: C:/fw/edk2/conf/target.txt

**Modify** **TOOL_CHAIN_TAG** to match your version of Visual Studio.

**Example:**

for Windows 7 64 bit OS and Visual Studio 2013 modify the following in Target.txt

From:

**TOOL_CHAIN_TAG = MYTOOLS**

to:

**TOOL_CHAIN_TAG = VS2013x86**

OPTIONAL: Update the MAX_CONCURRENT_THREAD_NUMBER **Save** and **close** the text file C:/fw/edk2/conf/target.txt