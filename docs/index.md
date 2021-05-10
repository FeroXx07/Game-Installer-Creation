# Game Installer Creation

You can use the [editor on GitHub](https://github.com/FeroXx07/Game-Installer-Creation/edit/main/docs/index.md) to maintain and preview the content for your website in Markdown files.

## What is a Installation?
Let’s start with the basics, Installation of a computer program is **the act of making the program ready for execution**. Installation refers to the configuration of a software or hardware with a view to making it usable with the computer. A soft or digital copy of the piece of software (program) is needed to install it. 

The **process** and the **management** of these kind of activities take a **big role** in many desktop and laptop **manufacturing companies**, so for these it is important that their hardware products function more efficiently, reduce end-user support costs, and minimize end-user business disruptions. 

One such technique is **application packaging**, which is a critical component of an overall software configuration management strategy.

### TYPES OF INSTALLATIONS
**1. Attended installation**

![Attended installation](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/WizardGIF.gif)

  It's the most common form of installation. An installation process usually needs a user who attends it to make choices, such as accepting or declining an end-user license      agreement (EULA), specifying preferences such as the installation location, supplying passwords or assisting in product activation.

**2. Silent installation**

![Silent installation](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/SilentInstaller.png)

  Installation that does not display messages or windows during its progress.

**3. Unattended installation**

![Unattended installation](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/UnattendedInstallation.png)

  Installation that is performed without user interaction during its progress or with no user present at all.

**4. Network installation**

![Network installation](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/NewtorkInstaller.jpg)

  Network installation, may be done by installing a minimal system before proceeding to download further packages over the network.

## What is Packaging?
Application packaging is a process of binding the relevant files and components to build a customized application for a customer.
Packaging bundles applications and operating systems into a single file called a distribution unit, which format can vary depending on the installer and the operating system.

This process makes it easier to deploy and install them on user's computers.

### Some advantages of application packaging

-	Simplify the Installation and Un-installation Procedures.
-	Can be advertised. So that on demos and trials can take place.
-	A solid package and its deployment can prevent piracy.
-	A solid package signed with a digital signature/certificate ensure that the distribution unit cannot be corrupted purposely when on the retail or end-user.
-	Upgrading of the application can be done with ease.
-	Customize Applications to suit the user needs.

### Some Packaging formats:
-	Legacy executables `Setup.exe`
-	Microsoft Windows Installer `Setup.msi`
-	Windows store `.appx`
-	Batch/script files `Install.vbs, Install.ps1, Install.bat`
-	Loose Files / Raw Files

## Microsoft Windows Installer
Is database-driven service that resides on workstations and controls the installing, uninstalling, patching, and repairing of software. Windows Installer is an .msi formatted file.

The installer consists of two executable components:

-	a Client Install Engine that runs with user privileges `msiexec.exe`
-	a Install Service that can run with elevated administrative privileges because it is implemented as a Windows Service

![Client and service](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/MSIInstaller.jpg)

### Brief History of why Microsoft Windows Installer exists:

Some time ago, the packages used the format .exe, but this had some limitations, as software developers and software vendors who created these installation packages practiced some inconsistencies, difficulting the path to the automation of installations.

A standard was needed, and the Microsoft Windows installer emerged as one, it uses `msiexec.exe` program to process the installation packages at an end user's PC. The packages follow a standardized database structure containing the information that Windows Installer requires to install or uninstall an application and to run the user interface for the setup.

The package file contains the installation database and a summary stream. Optionally, the package file can contain additional streams with the actual file bits compressed in cabinet files `.cab`. Package files have the extension `.msi` and are associated with `msiexec.exe`, which kicks off the installation process.

### MSI Installation process

The MSI Packaged Installation usually takes place in two phases:
1. Acquisition
2. Execution

**Acquisition:** The acquisition is further divided into two phases, in which the first phase collects the information from the user and the second phase acquires the information from the MSI database. Over here, the Windows installer will generate the installation and the un-installation scripts.

**Execution:** Once when the required information is collected from the user and the database, the MSI executes the Installation script and kicks off the installation of components.
The Windows installer also has the ability to detect and restore the resources of an application, which are required to make its successful execution (verification).

## Main Packaging tools

In the industry there are many packaging tools. The top ones are the following:

-**InstallShield:** Has good release management, localization and automation features for build process automation. Best for complex products and has release flags, very valuable to conditionally exclude or include certain parts of the product from each compiled setup. It also has a well-integrated GUI. Best for small development teams.
![Install Shield](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/InstallShield.png)


-**Advanced Installer:** Feature rich. Compiles all kinds of setups and supports all new technologies. Support for App-V (Microsoft Application Virtualization) seems very extensive. Best for corporate teams.

![Advanced Installer](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/AdvanceInstaller.jpg)

-**WiX:** The main selling point is the text source files. There is no need to store the source as a binary where it is almost impossible to track changes and do proper version control. This helps a lot when working in different branches, versions, and merging. And it has Full integration in Visual Studio.

![Wix](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/WixTool.gif)

## WiX Toolset

### Prerequisites
The selected approach will be Wix, because it excels in its flexibility, extensibility, stability, and the use of XML text source. And due to its free license, every developer can view and compile the source and changes are easily tracked, reverted, or approved.

![WiXLogo](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/WiXLOGO.png)

Before starting, let’s go to the basics. You will need to install two toolsets from Wix toolset.
The first one is the “WiX Toolset build tools” that includes everything you need to create installations on your development and build machines. And the second one is the “WiX Toolset Visual Studio Extension” that provides integration for the WiX Toolset into Visual Studio.

[Download WiX Toolset build tools](https://wixtoolset.org/releases/v3.11.2/stable)

[Download WiX Visual Studio Extension](https://wixtoolset.org/releases/)

In the creation of the installer script, you will have to define properties and add directories and components. You will see this now.

## Setup and creation of the script.

In order to create the script, you will have to add a new project in the Visual Studio solution. The type of project needs to be the following: “Setup Project for WiX v3”. 

![CreationScript](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/CreationOfTheScript.gif)

This will create a generic script file `product.wxs` that will be the container of the components of our installer  (all files including assets and `.exe` of the application) and the project file itself `.wixproj`, this last one contains properties for the creation of the installer.

![AfterCreation](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/AfterSetup.PNG)

The next step to be done is the creation of a unique file that will harvest and include all our assets and `dll` files automatically, through a special internal application: **Heat.exe** (it’s a WiX tool component). This file will be named `HeatGeneratedFileList.wxs` and to enable the harvesting feature we have to put _“Heat Directory”_ properties inside `.wixproj` with the file name correctly.

![HeatFileCreation](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/HeatGeneratedFileListCreation.PNG)

![AfterHeatCreation1](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/AfterHeat2.PNG)

Below is the necessary code of the _“Heat Directory”_ to enable heat.exe:

```XML
<!--OutputFile will have the name of the file created before -->
<Target Name="BeforeBuild">
  <HeatDirectory Directory="..\Output" 
    PreprocessorVariable="var.HarvestPath" 
    OutputFile="HeatGeneratedFileList.wxs"
    ComponentGroupName="HeatGenerated" 
    DirectoryRefId="INSTALLFOLDER" 
    AutogenerateGuids="true" 
    ToolPath="$(WixToolPath)" 
    SuppressFragments="true" 
    SuppressRegistry="true" 
    SuppressRootDirectory="true" />  
</Target>
```
Now, that everything is prepared, the next step is to link **components** (.exe, assets, dll) and **directories** (program folder, desktop shortcut, start menu shortcut) inside the `product.wxs`.

Before going deep into this, it is recommended to read the documentation or the user [manual](https://wixtoolset.org/documentation/manual/v3/) provided by Wix Toolset.

Shortly explained, the script is divided by **fragments**, we use **component and directories references** to tell the framework other components and directories that **exist** in other **fragments**.

Components have **GUID** to avoid duplications in updates o reparations. You can use this [website](https://www.guidgenerator.com/online-guid-generator.aspx) to generate GUIDs or use the visual studio internal tool to generate GUIDs. The step 0 is to change the **Manufacturer** name to the name of you studio, otherwise it won’t build.

## Customization and mapping of the script.

### Step 1

**Description:**
We have to add the `.exe` file of our application as a component inside a component or component group. In this case, there is already existing a component group, so we just have to add our component inside the component group code fragment.

**CODE:**

Into the ComponentGroup fragment:
```XML
<Component Id="Game.exe" Guid="4b886816-febd-4e5c-a87f-923960027d5c">
                <File Id="Game.exe" Source="..\Build\Release\Game.exe" KeyPath="yes" Checksum="yes" />
            </Component> 
```

Into the Feature fragment:
<!-- In our case, this is already created -->
```XML
<ComponentGroupRef Id="ProductComponents" />
```
![STEP0&1](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP0ANDSTEP1.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have a silent installation, the game would be installed in the ProgramFilesFolder directory and it could be uninstalled through Control Panel.

![STEP0&1OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP0ANDSTEP1OUTCOME.PNG)

### Step 2

**Description:**
We have to add the start menu shortcut, to do so we have to first add the StartMenuShortcut component inside the ApplicationProgramsFolder directory which is inside the ProgramMenuFolder directory.
1. But first we need to notify the framework the existence of ApplicationProgramsFolder directory. In our case, we already have that fragment for the directories created.
2. Then create a fragment for the shortcuts and put the necessary code there.
3. And finally, add the component reference of the StartMenuShortcut component into the Feature fragment.


**CODE:**

Into Directory System fragment:
```XML
<Directory Id="ProgramMenuFolder">
                <Directory Id="ApplicationProgramsFolder" Name="My UPC App"/>
         </Directory>
```

Into Shortcut Component fragment:
```XML
 <DirectoryRef Id="ApplicationProgramsFolder">
      <Component Id="StartMenuShortcut" Guid="ea2fc581-b635-4278-a8f1-1a81320d803a">
        <Shortcut Id="ApplicationStartMenuShortcut"
               Name="MyInstaller"
               Description="My UPC Game Description"
               Target="[#Game.exe]"
               WorkingDirectory="INSTALLFOLDER"/>
        <RemoveFolder Id="RemoveProgramsFolder" On="uninstall"/>
        <RegistryValue Root="HKCU" Key="Software\MyCompany\MyApplicationName" Name="installed" Type="integer" Value="1" KeyPath="yes"/>
      </Component>
    </DirectoryRef>
```

Into Feature fragment:
```XML
<ComponentRef Id="StartMenuShortcut" /> 
```
![STEP2](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP2.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have a silent installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and it could be uninstalled through Control Panel.

![STEP2OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP2OUTCOME.PNG)

### Step 3

**Description:**
We have to add the desktop shortcut, do same as the previous step, but with minor changes like the different directory, in this case DesktopFolder is the directory. 

**CODE:**

Into Directory fragment:
```XML
<Directory Id="DesktopFolder" Name="My UPC App" />
```

Into Shortcut Component fragment:
```XML
 <DirectoryRef Id="DesktopFolder">
       <Component Id="DesktopShortcut" Guid="c0f4eeec-8988-4c58-8a0a-2ebac04e2a2a">
          <Shortcut Id="ApplicationDesktopShortcut" 
                 Name="My UPC aPP" 
                 Description="My UPC Game Description"
                 Target="[#Game.exe]"
                 WorkingDirectory="INSTALLFOLDER"/>
          <RemoveFolder Id="RemoveDesktopFolder" On="uninstall"/>
          <RegistryValue Root="HKCU" Key="Software\MyCompany\MyApplicationName" Name="installed" Type="integer" Value="1" KeyPath="yes"/>
       </Component>
   </DirectoryRef>
```

Into Feature fragment:
```XML
<ComponentRef Id="DesktopShortcut" />
```
![STEP3](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP3.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have a silent installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and another in the desktop, and it could be uninstalled through Control Panel.

![STEP3OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP3OUTCOME.PNG)

### Step 4

**Description:**
We have to customize the **icon** of the shortcuts. To do so, we have to create a folder assets inside the installer directory and in the `product.wxs` we have to include some code into the product fragment and some other into the shortcuts.

![STEP4BEFORE](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP4BEFORE.PNG)

**CODE:**

Into Product fragment:
```XML
<Icon Id="icon.ico" SourceFile="assets\MyIcon.ico" />
<Property Id="ARPPRODUCTICON" Value="icon.ico" />
```

Into Shortcut Id fragments:
```XML
 Icon = "icon.ico"/>
```
![STEP4](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP4.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have a silent installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and another the desktop, all with custom icons, and it could be uninstalled through Control Panel.

![STEP4OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP4OUTCOME.PNG)

### Step 5

**Description:**
We have to add dialogs so users can accept or decline **license conditions or other agreements**, and even **choose the directory of the installation**. Also so we can customize the visuals of the dialog with `.bmp` archives and add a our project’s license in `.rtf` format. But before everything, we have to include in our `.wixproj` as a **reference** the _“WixUIExtension”_ `dll` provided by Wix Toolset, once that is done then we include it as a _UIRef_ in the `product.wxs`

**CODE:**

Into Product fragment:
```XML
<Property Id="WIXUI_INSTALLDIR" Value="INSTALLFOLDER" />
    <UIRef Id="WixUI_InstallDir" />
```

```XML
<WixVariable Id="WixUIBannerBmp" Value="assets\ui_background.bmp" />
    <WixVariable Id="WixUIDialogBmp" Value="assets\ui_background.bmp" />
```

```XML
<WixVariable Id="WixUILicenseRtf" Value="assets\License.rtf" />
```


![STEP5]()

**EXPECTED OUTCOME:**
If we run the installation right now we would have an attended installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and another the desktop, all with custom icons, and it could be uninstalled through Control Panel.

![STEP5OUTCOME]()
