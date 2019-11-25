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
