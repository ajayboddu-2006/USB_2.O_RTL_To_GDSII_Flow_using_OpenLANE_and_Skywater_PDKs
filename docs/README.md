# RTL-to-GDSII Flow for High-Speed USB 2.0 Device

## Introduction
This document outlines the complete RTL-to-GDSII flow implemented for a **High-Speed USB 2.0 device**. The project demonstrates how open-source tools, primarily **OpenLANE**, can be used to implement a structured ASIC design flow, covering all stages from RTL design to the final GDSII layout.

## Objectives
- To implement the ASIC design flow for a **High-Speed USB 2.0 device** while adhering to USB 2.0 specifications.
- To demonstrate each step of the flow, including **synthesis**, **floorplanning**, **placement**, **routing**, and **signoff**.
- To showcase the integration of open-source tools like **OpenLANE**, **Yosys**, **Magic**, and **KLayout** into a comprehensive design pipeline.

## OpenLane Project Directory Structure

The **OpenLane** project directory is organized to facilitate the complete ASIC design flow. Below is a typical directory structure with a brief explanation of each component:
```
Openlane/
├── Designs/
│   ├── usb/
│   |   ├── config.tcl
│   |   ├── sky130A_sky130_fd_sc_hs_config.tcl
│   |   ├── sky130A_sky130_fd_sc_ls_config.tcl
│   |   ├── sky130A_sky130_fd_sc_ms_config.tcl
│   |   ├── sky130A_sky130_fd_sc_hd_config.tcl
│   |   ├── sky130A_sky130_fd_sc_hdll_config.tcl
│   |   ├── src/
│   |   |   ├── usb_2p0_core.v
├── configuration/
│   ├── checkers.tcl
│   ├── cts.tcl
│   ├── floorplan.tcl
│   ├── general.tcl
│   ├── lvs.tcl
│   ├── placement.tcl
│   ├── routing.tcl
│   ├── synthesis.tcl
│   ├── README.md
├── flow.tcl         
├── clean_runs.tcl
```

To start the OpenLANE flow, first open the terminal, and get into the openlane directory as shown below:
#####################
To start the OpenLANE flow, type **docker** inside the openlane directory. You can check your current directory which is shown as **OpenLANE_flow**

In OpenLane, designs can be run in two primary modes:

1. Interactive Mode
This mode allows users to execute each stage of the design flow step by step, providing flexibility and control over the process.
Useful for debugging and understanding the design flow.
