# WPF Application Installer using WiX Toolset

This project demonstrates the creation of an MSI installer for a WPF application using the **WiX Toolset**. The installer includes custom actions, application icons, and shortcuts, and supports upgrading and uninstalling the application.

## Overview
This repository contains a setup project built with **WiX (Windows Installer XML)**, an open-source toolset that creates MSI installation packages for Windows. The project is designed to bundle a WPF application into an installer.

**Prerequisites:**
- [Download WiX Toolset v3](https://wixtoolset.org/docs/wix3/) Launch the downloaded installer and follow the on-screen instructions to finish the installation.

**Steps to Create an MSI Setup Installer:**


**1. Set Up Your WPF Application**

- **Create the WPF Application:**
  - Open Visual Studio.
  - File > New > Project > Select "WPF App".
  - Set the name and target framework for your project.

**2. Install WiX Toolset**

- **Download WiX Toolset:**
  - Go to WiX Toolset official site and download the latest version.
  - Install the toolset following the installer instructions.

**3. Create WiX Installer Project**

- **Add a WiX Setup Project:**
  - In Visual Studio, add a new project to your solution.
  - Search for the "WiX Setup Project" template and create it.
  - The project comes with a default Product.wxs file, which contains essential structure like Product, Package, and Feature elements.

**4. Link WPF Application to the WiX Installer**

- **Add Project Reference:**
  - Right-click the WiX setup project in Solution Explorer.
  - Select Add > Reference > Add the WPF application project.
  - This ensures your WPF app will be packaged and deployed with the installer.

**5. Modify the WiX Project Configuration**

- **Unload and Edit .wixproj:**
  - Right-click the WiX project > Unload Project.
  - Right-click again > Edit .wixproj.
  - Modify default configurations like OutputPath, DefineConstants, and ensure the WiX targets are properly imported.

**6. Configure Harvesting**

- **Harvest Files from WPF Application:**
  - Use the HeatDirectory task to gather files from the WPF publish directory and generate a .wxs file that lists files to be installed.
  
  **Example Harvesting in .wixproj**

  ```
    <Target Name="BeforeBuild">
        <HeatDirectory OutputFile="$(ProjectDir)\ProductInstallFiles.wxs" RunAsSeparateProcess="true"
                       Directory="$(HarvestDirectory)" ComponentGroupName="ProductFilesComponentGroup"
                       DirectoryRefId="INSTALLFOLDER" AutogenerateGuids="true" SuppressRegistry="true" />
    </Target>
  ```
- **Set Harvesting Path**
  ```
  <PropertyGroup>
      <HarvestDirectory>..\WPFSampleApplication\bin\Release\net8.0-windows\publish</HarvestDirectory>
  </PropertyGroup>
  ```
**7. Add WiX Toolset References**

- **Add References to WiX DLLs:**
  - Add references to WixUIExtension.dll and WixUtilExtension.dll from the WiX Toolset binaries in the installation directory.

**8. Configure Product.wxs**
- Update your Product.wxs file to include configuration for the installer directory, program menu, shortcut, app icon and custom actions for launching the application.

**9. Build and Verify the MSI Installer**

- **Build the Solution:**
  - Verify the Product.wxs and all WiX configurations.
  - Build the solution, which will generate the MSI installer.


**10. Verify Installation**
- Check the Control Panel to ensure the application appears under Programs and Features.
- Verify that shortcuts are created on the Desktop and in the Program Menu.
    
