---
description: "How to download and Install Docker \U0001F433 Desktop on Windows"
---

# Docker Setup for Windows

## **How to download and Install Docker 🐳 Desktop on Windows**

Note - Before we proceed further please note that steps for installing Docker 🐳 are slightly different for Windows Home edition and Windows Pro/Student edition. Here we’re describing the Windows Home edition \(because it’s used by most of the people\). For Windows Pro/Student edition please refer - [Check Here](https://docs.docker.com/docker-for-windows/install/)

{% embed url="https://youtu.be/q6MpbiqvpgA" caption="Docker Setup for Windows \| How to download & Install Docker 🐳 Desktop on Windows" %}

## **System Requirements**

Windows 10 Home machines must meet the following requirements to install Docker Desktop:

* Install Windows 10, version 1903 or higher. 
* Enable the WSL 2 \(Windows Subsystem for Linux\) feature on Windows. For detailed instructions, refer to the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
* The following hardware prerequisites are required to successfully run WSL 2 on Windows 10 Home:
  * 64 bit processor with [Second Level Address Translation \(SLAT\)](https://en.wikipedia.org/wiki/Second_Level_Address_Translation)
  * 4GB system RAM
  * BIOS-level hardware virtualization support must be enabled in the BIOS settings. For more information, see [Virtualization](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled).
* Download and install the [Linux kernel update package](https://docs.microsoft.com/windows/wsl/wsl2-kernel).

## **Install Docker Desktop on Windows**

1. Download Docker from Docker Hub - [Click Here](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
2. Double-click Docker Desktop Installer.exe to run the installer. If you haven’t already downloaded the installer \(Docker Desktop Installer.exe\), you can get it from [Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows/). It typically downloads to your Downloads folder, or you can run it from the recent downloads bar at the bottom of your web browser.
3. When prompted, ensure the Enable Hyper-V Windows Features option is selected on the Configuration page.
4. Follow the instructions on the installation wizard to authorize the installer and proceed with the install.
5. When the installation is successful, click Close to complete the installation process.
6. If your admin account is different to your user account, you must add the user to the docker-users group. Run Computer Management as an administrator and navigate to  Local Users and Groups &gt; Groups &gt; docker-users. Right-click to add the user to the group. Log out and log back in for the changes to take effect.
7. Docker Desktop does not start automatically after installation. To start Docker Desktop, search for Docker, and select Docker Desktop in the search results.

More details and official Docker documentation - [Check Here](https://docs.docker.com/docker-for-windows/install-windows-home/)

