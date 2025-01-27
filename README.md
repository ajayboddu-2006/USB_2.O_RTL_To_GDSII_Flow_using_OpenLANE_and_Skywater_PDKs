# RTL to GDSII Flow

## Overview
This repository demonstrates the implementation of the RTL-to-GDSII flow for a High-Speed USB 2.0 device. The USB CoreV design includes features such as a fully-compliant USB 2.0 protocol implementation, support for high-speed (480 Mbps) and full-speed (12 Mbps) modes, an efficient packet processing engine, and a customizable architecture. The project utilizes the open-source tool OpenLANE to cover all critical steps of the ASIC design flow, including synthesis, floorplanning, placement, routing, and signoff, resulting in the final GDSII layout. This implementation highlights the integration of industry-standard USB 2.0 specifications into a structured and efficient open-source design methodology.

## Objectives
- Understand and implement the RTL to GDSII flow.
- Optimize the design for area, power, and performance.
- Generate clean GDSII files with successful DRC and LVS signoff.

  
## OpenLANE Design Stages

OpenLANE flow consists of several stages. By default, all flow steps are run in sequence. Each stage may consist of multiple sub-stages. We can run Openlane in interactive mode also.

1. **Synthesis**
    - **yosys**: Performs RTL synthesis.
    - **abc**: Handles technology mapping.
    - **OpenSTA**: Performs static timing analysis on the resulting netlist to generate timing reports.

2. **Floorplan and PDN**
    - **init_fp**: Defines the core area for the macro, the rows (used for placement), and the tracks (used for routing).
    - **ioplacer**: Places the macro input and output ports.
    - **pdn**: Generates the power distribution network.
    - **tapcell**: Inserts welltap and decap cells in the floorplan.

3. **Placement**
    - **RePLace**: Performs global placement.
    - **Resizer**: Performs optional optimizations on the design.
    - **OpenPhySyn**: Performs timing optimizations on the design.
    - **OpenDP**: Performs detailed placement to legalize the globally placed components.

4. **CTS**
    - **TritonCTS**: Synthesizes the clock distribution network (the clock tree).

5. **Routing**
    - **FastRoute**: Performs global routing to generate a guide file for the detailed router.
    - **CU-GR**: Another option for performing global routing.
    - **TritonRoute**: Performs detailed routing.
    - **SPEF-Extractor**: Performs SPEF extraction for post-routing analysis.

6. **GDSII Generation**
    - **Magic**: Streams out the final GDSII layout file from the routed DEF and performs DRC and antenna checks.
    - **KLayout**: Streams out the final GDSII layout file as a backup option and provides additional DRC checks.

7. **Checks**
    - **Magic**: Performs DRC checks and antenna checks.
    - **KLayout**: Performs additional DRC checks.
    - **Netgen**: Performs LVS checks.
    - **CVC**: Verifies circuit validity.


## Directory Structure
```
RTL-to-GDSII-Flow/
├── README.md          
├── docs/              
├── RTL/               
├── Synthesis/         
├── Floorplan/         
├── Placement/
├── CTS      
├── Routing/         
├── Signoff/           
├── Results/               
```


## How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/RTL-to-GDSII-Flow.git
   cd RTL-to-GDSII-Flow
   ```
2. Install the required tools (Yosys, OpenLane, Magic, etc.).
3. Follow the step-by-step instructions in the `docs/` folder for each stage of the flow.


## Documentation
Detailed documentation for each step of the flow is available in the `docs/` folder, including:
- Tool installation and setup
- Command sequences for synthesis, placement, and routing
- Flow diagrams and explanations

## Acknowledgments
- I used the Verilog code from the open-source USB CoreV repository (https://github.com/avakar/usbcorev) as the foundation for this project
- OpenLane project by efabless
- SkyWater PDK for the 130nm process
- Open-source EDA tools community

## Contributions
Contributions are welcome! Feel free to fork this repository, submit issues, or open pull requests to enhance the flow.

