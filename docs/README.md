# Game Installer Creation

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

-**NSIS:** Nullsoft Scriptable Install System, is a small and fast package bundler, it has some of the best compression methods like LZMA and it is fully customizable, from interfaces to wizards. Also, it is compatible with all Windows versions. It is mainly script based and supports plug-ins.

![NSIS](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/NSIS.jpg)

-**Inno Setup:** Very extensive in sense of features, it is also fully customizable. Inno also supports digital signing and uses 7-zip LZMA/LZMA2 file compression. It is mainly script based.

![Inno Setup](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/INNOSETUP.png)

-**WiX:** The main selling point is the text source files. There is no need to store the source as a binary where it is almost impossible to track changes and do proper version control. This helps a lot when working in different branches, versions, and merging. And it has Full integration in Visual Studio.

![Wix](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/WixTool.gif)

# WiX Toolset

## Prerequisites
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

# Customization and mapping of the script.

## Step 1

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

## Step 2

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

## Step 3

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

## Step 4

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

|       WiX      |       ICON     |     SIZES     |
| -------------  | -------------  | ------------- |
| Icon           | icon.ico       | 16×16         |
| Icon           | icon.ico       | 32 * 32       |               
| Icon           | icon.ico       | 48 * 48       |              
| Icon           | icon.ico       | 256 * 256     |              


![STEP4](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP4.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have a silent installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and another the desktop, all with custom icons, and it could be uninstalled through Control Panel.

![STEP4OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP4OUTCOME.PNG)

## Step 5

**Description:**
We have to add dialogs so users can accept or decline **license conditions or other agreements**, and even **choose the directory of the installation**. Also so we can customize the visuals of the dialog with `.bmp` archives and add a our project’s license in `.rtf` format. But before everything, we have to include in our `.wixproj` as a **reference** the _“WixUIExtension”_ `dll` provided by Wix Toolset, once that is done then we include it as a _UIRef_ in the `product.wxs`

![STEP5BEFORE](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/STEP5.gif)

**CODE:**

Into Product fragment:
```XML
<Property Id="WIXUI_INSTALLDIR" Value="INSTALLFOLDER" />
    <UIRef Id="WixUI_InstallDir" />
```

```XML
<WixVariable Id="WixUIBannerBmp" Value="assets\TopBanner.bmp" />
    <WixVariable Id="WixUIDialogBmp" Value="assets\BackgroundBanner.bmp" />
```

```XML
<WixVariable Id="WixUILicenseRtf" Value="assets\License.rtf" />
```

|       WiX     |       BMP     |     SIZES    |
| ------------- | ------------- |------------- |
|WixUIBannerBmp | Top banner    | 493 × 58     |
|WixUIDialogBmp | Background bitmap used on the welcome and completion dialogs | 493 × 312     |


![STEP5](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP5.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have an attended installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and another the desktop, all with custom icons, and it could be uninstalled through Control Panel.

![STEP5OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/STEP5INSTALLER.gif)

## Step 6

**Description:**
Finally, the installer is almost completed, we have to just include the final line so that `Product.wxs` gets the assets and dlls from `HeatGeneratedFileList.wxs.` Also, we have to define in the properties of our project a **preprocessor variable: <<HarvestPath=..\Output>>**

![STEP6BEFORE](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/STEP6BEFORE.gif)

**CODE:**

Into Feature fragment:
```XML
 <ComponentGroupRef Id="HeatGenerated" />
```

![STEP6](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/images/STEP6CODE.PNG)

**EXPECTED OUTCOME:**
If we run the installation right now we would have an attended installation, the game would be installed in the ProgramFilesFolder directory with a shortcut in the start menu and another the desktop, all with custom icons, and it could be uninstalled through Control Panel.

![STEP6OUTCOME](https://raw.githubusercontent.com/FeroXx07/Game-Installer-Creation/main/docs/gifs/STEP6FINAL.gif)

# Digital signing

We use **digital signatures** when we want to distribute data, and we want to assure recipients that it does indeed come from us. 
Signing data does not alter it; it simply generates a digital signature string you can bundle with the data.

Digital signatures are created using a public-key signature algorithm such as the RSA public-key cipher. 
A public-key algorithm actually uses two different keys: the public key and the private key (called a key pair). 
The private key is known only to its owner, while the public key can be available to anyone.
SignTool.exe, SignTool is a command line tool that is used to sign an application package or a batch of applications with a certificate.

The tool is installed with [Microsoft Windows Software Development Kit (SDK)](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/) installation path. Then we need Microsoft Windows SDK to be able to work with SignTool.exe.

1. On the development computer, install the certificate that you want to sign the file with.

2. Open a Visual Studio command prompt throught visual studio tools.

3. Change to the directory that contains the `.msi` file.

4. Sign the `.msi` file by using the following command:

```CMD
signtool sign /sha1 CertificateHash SetupNameFile.msi
```
# Testing on Virtual Machines

Virtual machines are one of the easiest ways of testing software on simulated, yet full operating systems, we’ll be working with Virtual Box, you can download it by clicking [here](https://www.virtualbox.org/wiki/Downloads). Also, we’ll need VirtualBox windows `.iso` files that can be downloaded from [here](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/).

-The process is simple, once the VirtualBox and its drivers are installed:

-Click NEW to create a new virtual machine and follow the process of disk space and ram allocation.

-After that, the wizard will ask you to choose a `.iso` file to boot the operating system of our choice.

-Finally, before anything else take a “snapshot” through the machine option, it will work like a backup. And to import files from our PC to the simulated operating system just change drag and drop feature to bidirectional through the devices option in the top bar.

More detailed information of the process can be found [here.](https://az792536.vo.msecnd.net/vms/release_notes_license_terms_8_1_15.pdf) 

# Possible Improvements/Innovations
The lack of and GUI is noticed a lot, specially for newcomers into this tool. There are third party visual studio extensions like [IsWix](http://iswix.com/projects/) or tools like [Wax](https://github.com/tom-englert/Wax) that supply this lack of user interface.

# Documentation Links and References
- [Application packaging](https://community.broadcom.com/symantecenterprise/communities/community-home/librarydocuments/viewdocument?DocumentKey=1b1b89b8-c3a0-4bbd-a498-44f76a777eb9&CommunityKey=41d8253b-a238-4563-8718-ed7623beafbc&tab=librarydocuments)
- [MSI/Setup package for C# with WiX Toolset](https://www.mesta-automation.com/create-an-installer-for-c-sharp-with-wix/)
- [MSI/Setup package for C# with WiX Toolset VIDEO](https://www.youtube.com/watch?v=-wyUxQux7xY)
- [About Windows Installer Service](http://www.installsite.org/pages/en/w2k_aboutmsi.htm)
- [About Windows Installer](https://docs.microsoft.com/en-US/windows/win32/msi/windows-installer-portal)
- [Basics of Application packaging](https://www.dell.com/downloads/global/power/ps4q05-20050175-Kouletsis.pdf)
- [Installation wikipedia](https://en.wikipedia.org/wiki/Installation_(computer_programs))
- [Software Deployment](https://www.sumologic.com/glossary/software-deployment/)
- [Differences between InstallShield, WiX, Wise, Advanced Installer...](https://stackoverflow.com/questions/1544292/what-installation-product-to-use-installshield-wix-wise-advanced-installer/1546941#1546941)
- [WiX Improvements Proposals](https://wixtoolset.org/development/wips/)
- [GUID generator](https://www.guidgenerator.com/online-guid-generator.aspx)
- [Digital signing](https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537361(v=vs.85))
- [Signtool basics](https://docs.microsoft.com/es-es/windows/win32/seccrypto/signtool)
- [Signtool with msi](https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2010/ee290833(v=vs.100))
- [Certificates generator](https://certificatetools.com/)
- [NSIS](https://nsis.sourceforge.io/Main_Page)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

