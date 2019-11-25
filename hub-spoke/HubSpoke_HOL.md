# OCI Terraform Asset - Hub Spoke Network Topology

## Table of Contents

[Overview](#overview)

## Overview

This architecture shows how to implement a hub-spoke network topology in OCI. The hub is a virtual cloud network (VCN) that is connected to your on-premises network, and the spokes are VCNs that peer with the hub and allow you to isolate workloads. This architecture also demonstrates how to include shared services in the hub that the spokes can then use. You can connect your hub VCN and on-premises network via a VPN connection or Oracle FastConnect.
