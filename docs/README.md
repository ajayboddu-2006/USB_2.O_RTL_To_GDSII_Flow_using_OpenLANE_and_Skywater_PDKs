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











config.tcl                            sky130A_sky130_fd_sc_hs_config.tcl
runs                                  sky130A_sky130_fd_sc_ls_config.tcl
sky130A_sky130_fd_sc_hd_config.tcl    sky130A_sky130_fd_sc_ms_config.tcl
sky130A_sky130_fd_sc_hdll_config.tcl  src
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/usb$ ls -1
config.tcl
runs
sky130A_sky130_fd_sc_hd_config.tcl
sky130A_sky130_fd_sc_hdll_config.tcl
sky130A_sky130_fd_sc_hs_config.tcl
sky130A_sky130_fd_sc_ls_config.tcl
sky130A_sky130_fd_sc_ms_config.tcl

├── scripts/              
├── configuration/               
├── flow.tcl         
├── clean_runs.tcl/         
├── Placement/
├── CTS/
├── Routing/         
├── Signoff/           
│   ├── DRC/           # Design Rule Check reports and files
│   ├── LVS/           # Layout vs Schematic check reports and files
│   ├── STA/           # Static Timing Analysis reports and files
│   ├── Antenna/       # Antenna check reports
│   └── SPEF/          # Extracted Standard Parasitic Exchange Format files
├── Results/
```

