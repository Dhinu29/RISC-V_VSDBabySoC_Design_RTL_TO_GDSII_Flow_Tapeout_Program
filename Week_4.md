# P_DINESH_WEEK_4_RISC_V_SoC_Tapeout_Program_VSD

# ⚡Analog Circuit Simulation Using Ngspice
# **ngspice - open source spice simulator**

ngspice is the open source spice simulator for electric and electronic circuits.
Such a circuit may comprise of JFETs, bipolar and MOS transistors, passive elements like R, L, or C, diodes, transmission lines and other devices, all interconnected in a netlist. Digital circuits are simulated as well, event driven and fast, from single gates to complex circuits. And you may enter the combination of both analog and digital as a mixed-signal circuit.

# Installing Ngspice on Ubuntu

**Step 1:** Update your system
```
sudo apt update
sudo apt upgrade -y
```

**Step 2:** Install Ngspice
```
sudo apt install ngspice -y
```

**Step 3:** Verify the installation
```
ngspice -v
```
<img width="1902" height="245" alt="image" src="https://github.com/user-attachments/assets/6fac2708-3042-4870-8d6c-802f7f839316" />

**Step 4:** Run a simple test

- Create a file named ```inverter.spice``` with a simple RC circuit:

```
VDD Vdd 0 DC 5        ; Supply voltage
Vin in 0 PULSE(0 5 0 1n 1n 10n 20n)  ; Input pulse: 0→5V

* NMOS Transistor
M1 out in 0 0 NMOS L=1u W=10u

* PMOS Transistor
M2 out in Vdd Vdd PMOS L=1u W=20u

* Load
Cload out 0 1p

* Model Definitions
.model NMOS NMOS (LEVEL=1 VTO=1 KP=50u)
.model PMOS PMOS (LEVEL=1 VTO=-1 KP=20u)

* Analysis
.tran 0.1n 40n
.control
run
plot v(in) v(out)
.endc

.end
```
- Open terminal and run:

```
#run
ngspice inverter.spice
```

<img width="1912" height="907" alt="ngspice_example" src="https://github.com/user-attachments/assets/f81af62b-be8a-40b4-bb82-7272f7f55ca5" />


# Step-by-Step Guide to Write Ngspice Code
**Step 1:** Understand Your Circuit

- Identify the components in your circuit (resistors, capacitors, NMOS, PMOS, voltage sources, etc.).

- Decide the nodes (connection points) for all components.

- Example: A simple CMOS inverter has `VDD`,`Vin`, `out`, `NMOS`, and `PMOS`.

**Step 2:** Create a Netlist File

- Open a text editor and save your file with .spice extension.

- Ngspice reads this netlist to simulate the circuit.

**Step 3:** Define Voltage Sources
```
VDD Vdd 0 DC 5           ; Supply voltage
Vin in 0 PULSE(0 5 0 1n 1n 10n 20n)  ; Input pulse: 0→5V
```

- VDD is the power supply.

- Vin is the input signal (pulse for switching simulation).


**Step 4:** Define Devices (Transistors, Resistors, Capacitors)
```
M1 out in 0 0 NMOS L=1u W=10u  ; NMOS
M2 out in Vdd Vdd PMOS L=1u W=20u  ; PMOS
Cload out 0 1p  ; Load capacitor
```

- M1 and M2 are transistors.

- Cload simulates the output capacitance.

**Step 5:** Add Control Commands (scripting)
```
.control
run
plot v(in) v(out)
.endc
```


**Step 6:** Save and Run

- Save the file (e.g., inverter.spice).

- Open terminal and run:
```
  ngspice inverter.cir
```

**Step 7:** Analyze Results

- Observe the input/output waveform for correct switching behavior.

- Adjust transistor parameters, supply voltage, or load capacitance to see effects.

- Document your observations for your report.

# Week 4 — Analog Circuit Simulation Using Ngspice (Sky130)

## Overview
Week 4 focused on **analog circuit simulation** using **Ngspice** with the **Sky130 PDK models**.  
The tasks covered NMOS device behavior, CMOS inverter characteristics, and robustness evaluation under variations in device parameters and power supply.

---

## Week 4 Tasks

### Day 1 — Basics of NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)
- Introduction to Circuit Design and SPICE simulations
  - Why do we need SPICE simulations?
  - Basic elements in circuit design – NMOS
  - Strong inversion and threshold voltage
  - Threshold voltage with positive substrate potential
- NMOS resistive and saturation regions
  - Resistive region with small Vds, drift current theory
  - Drain current model for linear region
  - Pinch-off region and saturation current
  - SPICE lab exercises with Sky130 models
- Introduction to SPICE
  - Basic SPICE setup, circuit description, and technology parameters
  - First SPICE simulation with Sky130 models

### Day 2 — Velocity Saturation and Basics of CMOS Inverter VTC
- Velocity saturation effect
  - SPICE simulation for lower nodes
  - Drain current vs gate voltage for long and short channel devices
  - Velocity saturation drain current model
  - Labs with Sky130 Id-Vgs and threshold voltage
- CMOS voltage transfer characteristics (VTC)
  - MOSFET as a switch, standard MOS parameters
  - PMOS/NMOS drain current vs drain voltage
  - Stepwise construction of VTC curves from SPICE simulations

### Day 3 — CMOS Switching Threshold and Dynamic Simulations
- Voltage Transfer Characteristics (VTC)
  - SPICE deck creation and inverter simulation
  - Labs with Sky130 CMOS inverter simulation
- Static behavior evaluation
  - Switching threshold Vm calculation and analysis
  - Effect of (W/L)p and (W/L)n on Vm
  - Static and dynamic simulations of CMOS inverter
  - Applications in clock network and STA

### Day 4 — CMOS Noise Margin Robustness Evaluation
- Noise margin concepts
  - Introduction and voltage parameters
  - Noise margin equations and summary
  - Variation with PMOS width
  - Sky130 SPICE lab exercises

### Day 5 — CMOS Power Supply and Device Variation Robustness Evaluation
- Power supply variation
  - Effect on inverter switching behavior
- Device variation
  - Impact on static behavior and performance

---


# Conclusion

Week 4 successfully demonstrated NMOS device characteristics, CMOS inverter behavior, and robustness evaluation using Ngspice with Sky130 models.
Simulation results provide a solid understanding of analog circuit operation and prepare for advanced design verification in future weeks.


# LAB REPORTS

Download workshop Collaterals from below link
```
#clone the repository
git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop/
```
## DAY 1 :
**FILE NAME** : day1_nfet_idvds_L2_W5.spice
<img width="1917" height="697" alt="day1_nfet_idvds_L2_W5_spice_compile" src="https://github.com/user-attachments/assets/0e43c1c8-1a15-4e5d-9b7d-89f1821ee802" />
<img width="1918" height="910" alt="day1_nfet_idvds_L2_W5_spice_vin#branch" src="https://github.com/user-attachments/assets/8d4f98dd-84be-4a27-872c-f34244be2778" />
<img width="1918" height="910" alt="day1_nfet_idvds_L2_W5_spice_vdd#branch" src="https://github.com/user-attachments/assets/d68dd2fd-c987-466a-974f-9c20acc5e7a6" />

**FILE NAME** : day2_nfet_idvgs_L015_W039.spice
<img width="1918" height="885" alt="day2_nfet_idvgs_L015_W039_spice_compile" src="https://github.com/user-attachments/assets/fef0d251-dbfa-4cf2-b271-a8c250ce1915" />
<img width="1918" height="898" alt="day2_nfet_idvgs_L015_W039_spice_vdd#branch" src="https://github.com/user-attachments/assets/62c329fd-f5eb-4c78-89dc-e85ad90b39cd" />

**FILE NAME** : day2_nfet_idvds_L015_W039.spice
<img width="1917" height="881" alt="day2_nfet_idvds_L015_W039_spice_compile" src="https://github.com/user-attachments/assets/18f63ff3-a508-49a2-b63a-4e8c7a350555" />
<img width="1917" height="915" alt="day2_nfet_idvds_L015_W039_spice_vdd#branch" src="https://github.com/user-attachments/assets/21d334b0-6b91-4c54-b9e6-2fd5c3ca0589" />

**FILE NAME** : day3_inv_vtc_Wp084_Wn036.spice
<img width="1918" height="911" alt="day3_inv_vtc_Wp084_Wn036_spice_compile" src="https://github.com/user-attachments/assets/4219a540-8e73-4a24-be87-f78abc10c4c5" />
<img width="1918" height="882" alt="day3_inv_tran_Wp084_Wn036_spice_out_vs_in" src="https://github.com/user-attachments/assets/8f13501f-79b8-4dd9-ac61-f8043d6ec31a" />

**FILE NAME** : day3_inv_tran_Wp084_Wn036.spice
<img width="1917" height="867" alt="day3_inv_tran_Wp084_Wn036_spice_compile" src="https://github.com/user-attachments/assets/b24fda60-a1a8-4703-8e13-938b90e6e9e3" />
<img width="1917" height="911" alt="day3_inv_tran_Wp084_Wn036_spice_out_vs_time_in" src="https://github.com/user-attachments/assets/26399234-d908-4f10-9e65-e4b0591b3a1e" />


**FILE NAME** : day4_inv_noisemargin_wp1_wn036.spice
<img width="1915" height="865" alt="day4_inv_noisemargin_wp1_wn036_spice_compile" src="https://github.com/user-attachments/assets/51b907c8-0d69-45d4-8333-48b23228ec34" />
<img width="1918" height="916" alt="day4_inv_noisemargin_wp1_wn036_spice_out_vs_in" src="https://github.com/user-attachments/assets/524de155-85d3-40d3-af2a-33f3063abbe4" />

**FILE NAME** : day5_inv_devicevariation_wp7_wn042.spice
<img width="1918" height="882" alt="day5_inv_devicevariation_wp7_wn042_spice_compile" src="https://github.com/user-attachments/assets/d7e82aa6-bc50-41cf-bd86-fca25ff4cae7" />
<img width="1918" height="902" alt="day5_inv_devicevariation_wp7_wn042_spice_out_vs_in" src="https://github.com/user-attachments/assets/5834d999-38ba-42a6-be2d-be4e4f3a1ea0"/>

**FILE NAME** : day5_inv_supplyvariation_Wp1_Wn036.spice
<img width="1917" height="907" alt="day5_inv_supplyvariation_Wp1_Wn036_spice_compile" src="https://github.com/user-attachments/assets/ab3b3cb8-6f53-43e6-b7ca-7ff28fba93f9" />
<img width="1918" height="907" alt="day5_inv_supplyvariation_Wp1_Wn036_spice_char" src="https://github.com/user-attachments/assets/232bfadc-8664-47a4-a6c0-73b60de65cc1" />




# Conclusion

Week 4 successfully demonstrated analog circuit simulation using Ngspice with Sky130 PDK models.

- NMOS transistor behavior was analyzed, showing correct operation in both the resistive and saturation regions.

- CMOS inverter characteristics were studied through Voltage Transfer Characteristics (VTC), switching thresholds, and dynamic simulations.

- Robustness analysis was performed, including noise margin evaluation, power supply variation, and device parameter variations.

- Ngspice simulations provided clear visualization of circuit behavior, validating theoretical concepts and reinforcing understanding of device-level and inverter-level operation.

This week’s exercises laid a solid foundation for analog circuit verification and prepared for more advanced simulations in subsequent weeks.






