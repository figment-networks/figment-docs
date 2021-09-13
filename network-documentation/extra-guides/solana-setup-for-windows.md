---
description: How to setup for the Solana Pathway on Windows
---

# Setup Solana on Windows

**Windows Users:** The Rust BPF toolchain _is not available for Windows_. This means that compiling Solana programs cannot be performed in a Windows development environment.

The following software is required to set up and complete the **Solana** Pathway

* [Docker Desktop](https://docs.figment.io/network-documentation/extra-guides/docker-setup-for-windows)
* [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps)

## **Install WSL on Windows**

Windows 10 Home machines must meet the following requirements to install Docker Desktop:

* Install Windows 10, version 1903 or higher. 
* Enable the WSL 2 \(Windows Subsystem for Linux\) feature on Windows. For detailed instructions, refer to the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
* The following hardware prerequisites are required to successfully run WSL 2 on Windows 10 Home:
  * 64 bit processor with [Second Level Address Translation \(SLAT\)](https://en.wikipedia.org/wiki/Second_Level_Address_Translation)
  * 4GB system RAM
  * BIOS-level hardware virtualization support must be enabled in the BIOS settings. For more information, see [Virtualization](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled).
* Download and install the [Linux kernel update package](https://docs.microsoft.com/windows/wsl/wsl2-kernel).

## **Setup the Solana ecosystem**

To access the filesystem of your [installed Linux distribution](https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-6---install-your-linux-distribution-of-choice) for WSL :

* Run the command [`wsl`](https://docs.microsoft.com/en-us/windows/wsl/reference) from a `cmd.exe` or PowerShell terminal. It is also important to make sure your PATH in the Windows Subsystem for Linux environment includes the location of the Solana release you have installed, such as `:PATH="~/.local/share/solana/install/active_release/bin:$PATH"`.
* More information on viewing and setting the PATH in Linux is [available here](https://opensource.com/article/17/6/set-path-linux).



