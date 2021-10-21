---
description: How to setup for the Solana Pathway on Windows
---

# Setup Solana BPF Toolchain on Windows

The Rust BPF toolchain is _not available_ for Windows.\
This means that compiling Solana programs cannot be performed in a Windows development environment. The following software is required to set up and complete the **Solana** Pathway on a computer running the Microsoft Windows operating system:

* [Docker Desktop](https://docs.figment.io/network-documentation/extra-guides/docker-setup-for-windows)
* [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps)

## **Install Docker Desktop**

{% content-ref url="docker-setup-for-windows.md" %}
[docker-setup-for-windows.md](docker-setup-for-windows.md)
{% endcontent-ref %}

## **Install WSL on Windows**

Windows 10 Home machines must meet the following requirements to install Docker Desktop:

* Install Windows 10, version 1903 or higher.&#x20;
* The following **hardware** prerequisites are required to successfully run WSL2 on Windows 10 Home:
  * 64 bit processor with [Second Level Address Translation (SLAT)](https://en.wikipedia.org/wiki/Second\_Level\_Address\_Translation)
  * 4GB system RAM
  * BIOS-level hardware virtualization support must be enabled in the BIOS settings. For more information, refer to the [Virtualization](https://docs.docker.com/desktop/windows/troubleshoot/#virtualization) troubleshooting topic.
* Enable the WSL2 feature on Windows. For detailed instructions, refer to the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
* Download and install the [Linux kernel update package](https://docs.microsoft.com/windows/wsl/wsl2-kernel).

## **Setup the Solana ecosystem**

To access the filesystem of your [installed Linux distribution](https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-6---install-your-linux-distribution-of-choice) for WSL :

* Run the command [`wsl`](https://docs.microsoft.com/en-us/windows/wsl/reference) from a `cmd.exe` or PowerShell terminal. Once you have logged in, install the [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools) with the command: `sh -c "$(curl -sSfL https://release.solana.com/v1.7.11/install)"`
* It is also important to make sure your PATH in the WSL environment includes the location of the Solana release you have installed, such as `:PATH="~/.local/share/solana/install/active_release/bin:$PATH"`
* More information on viewing and setting the PATH in Linux is [available here](https://opensource.com/article/17/6/set-path-linux).

Once WSL is installed and you can access it through the Windows command prompt, you can continue to follow the [setup instructions for the Rust toolchain](https://learn.figment.io/tutorials/deploy-solana-program#set-up-the-solana-c-l-i) in the Solana Pathway. This will enable you to compile Solana programs on a computer running Microsoft Windows, within the WSL environment.

Happy building! 😁

