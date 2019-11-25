# OCI Terraform Asset - Hub Spoke Network Topology

## Table of Contents

[Overview](#overview)

## Overview

This architecture shows how to implement a hub-spoke network topology in OCI. The hub is a virtual cloud network (VCN) that is connected to your on-premises network, and the spokes are VCNs that peer with the hub and allow you to isolate workloads. This architecture also demonstrates how to include shared services in the hub that the spokes can then use. You can connect your hub VCN and on-premises network via a VPN connection or Oracle FastConnect.

![](media/image1.jpg)

This hub-spoke topology can help you reduce costs by centralizing services shared by multiple workloads, overcome service limits by peering VCNs from different tenancies with a central VCN, and separate operations between central IT and workloads. This architecture is typically used for workloads run in different environments (production, testing, development, etc.) that share services, workloads that share services but do not require connectivity, and enterprises that require central control over security aspects in the hub yet separate management of the workloads in the spokes.

## Introduction

In this lab, we will install Terraform on your machine, install the Oracle Cloud Infrastructure CLI (Command Line Interface) on your machine, and set up the hub VCN in OCI using the Terraform CLI.

## Objectives

- Install the Terraform CLI
- Install the OCI CLI
- Create a VCN using Terraform CLI

## Required Artifacts

- If running from Windows: [Putty and PuttyGen](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
- Access to an OCI tenancy
- IntelliJ IDEA from JetBrains. The community version of this IDE can be downloaded [here](https://www.jetbrains.com/idea/).

# Install Terraform on your local machine

You will need to install Teraform to use the Terraform CLI to create resources in OCI.

### **STEP 1**: Download Terraform

- Go to the Terraform [website](https://www.terraform.io/)

![](media/image2.png)

- Click the link for your computer's operating system.

![](media/image3.png)

- Open up a new Finder window and go to the “Downloads” folder. Verify that a zip file starting with “terraform…” is there.

![](media/image4.png)

### **STEP 2**: Install Terraform

- Copy the zip file from the “Downloads” folder. Create a new folder in your User folder called “Terraform”. Paste the zip file in this new folder and unzip it. A new executable file called “terraform” should appear.

![](media/image5.png)

- Open a new Terminal window. Open the _.bash_profile_ file by typing the following:

  ```
  open ~/.bash_profile
  ```

  This command should open the file in your computer’s default text editor. Add the line shown below to the file, substituting the user _crlamb_ for your own username.

  ![](media/image6.png)

  Save and close the file. Enter the following command in the terminal:

  ```
  source ~/.bash_profile
  ```

  Terraform now should be executable system-wide from any directory. Confirm that you can all the `terraform` command by typing the following in your terminal:

  ```
  terraform
  ```

  The result should look like this:

  ![](media/image7.png)

### **STEP 3**: Install Oracle Cloud Infrastructure CLI

- In the terminal window, enter the following command:

  ```
  bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
  ```

  This command downloads and runs the OCI CLI installer script

  **NOTE**: If you do not have a compatible version of Python installed, you must upgrade your computer’s version of Python. If you are a Mac user, the script will not install it for you. You can download the most recent version of Python [here](https://www.python.org/downloads/).

  When prompted to upgrade the CLI to the newest version, respond with Y to overwrite an existing installation. When prompted to update your PATH, respond with Y to be able to invoke the CLI without providing the full path to the executable. This will add _oci.exe_ to your PATH. Respond with Y with any other prompts the installation script may present.

  ![](media/image8.png)

  Your terminal window should look like the above screenshot after a successful installation.

### **STEP 4**: Set up the config file

- Set up the config file with the following command:

  ```
  oci setup config
  ```

  **NOTE**: Use the default location for the config file.

- Enter the user's OCID. You can find the user's OCID in the Console on the page showing the user's details. To get to that page, open the **Profile** menu and click your username. Make a note of the user OCID. You will need it in a future step.

  ![](media/image9.png)

  ![](media/image10.png)

- Enter the tenancy OCID. It can be found from the **Profile** menu by clicking on the tenancy name. Make a note of the tenancy OCID. You will need it in a future step.

  ![](media/image11.png)

  ![](media/image12.png)

- Enter the home region of your tenancy in the format specified. You can find the tenancy’s home region on the **Tenancy Information** page. Make a note of this region. You will need it in a future step.

  ![](media/image13.png)

- Generate a new RSA key pair. Use the default location and names for the key pair. Leave the passphrase for the private key empty.

  ![](media/image14.png)

  The config file is now set up.

### **STEP 5**: Create a compartment
