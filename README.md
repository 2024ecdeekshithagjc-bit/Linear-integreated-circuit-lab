# Linear-integreated-circuit-lab
S# Experiment – 1  
## DC, Transient and AC Analysis of Common Source Amplifier using 180nm NMOS in LTspice

---

## AIM :

To design a Common Source (CS) amplifier using 180nm NMOS technology in LTspice and to perform DC, Transient and AC analysis as per the given specifications.

---
## Design Specifications

| Parameter              | Symbol | Value        | Unit | Notes                     |
|------------------------|--------|-------------|------|----------------------------|
| Supply Voltage         | VDD    | 2           | V    | Power supply               |
| Power Constraint       | P      | ≤ 1.2       | mW   | Maximum allowable power    |
| Load Capacitance       | CL     | 10          | pF   | Output load capacitor      |
| Channel Length         | L      | 480         | nm   | MOSFET channel length      |
| Technology Node        | —      | 180 nm TSMC | —    | CMOS process technology    |

## Components Used

The following components were used to design and simulate the circuit:

- **NMOS Transistor** (180 nm technology model)
- **Drain Resistor (RD)**
- **DC Power Supply (VDD)**
- **AC Signal Source** (Input)
- **Load Capacitor (1 pF)**
- **Ground and Interconnecting Wires**

---

## Circuit Diagram Description

The Common Source amplifier was designed and simulated in **LTspice** using a 180 nm NMOS technology model.

In this configuration:

- The drain resistor (Rd = 5k) is connected between the supply voltage (VDD = 2V) and the drain terminal of the NMOS transistor.
- The input AC signal of 0.9V is applied to the gate terminal.
- The output is taken from the drain terminal.
- The source terminal is connected to ground.
- 
![Image description](https://github.com/2024ecdeekshithagjc-bit/Linear-integreated-circuit-lab/blob/main/CS%20amplifier%20without%20capacitor.png?raw=true)
This setup represents a basic Common Source amplifier configuration without capacitor.

# Common Source (CS) Amplifier – LTspice Simulation

## Theory

A Common Source (CS) amplifier is one of the fundamental MOSFET amplifier configurations.  
In this configuration:

- The **source** terminal is grounded  
- The **input** is applied at the gate  
- The **output** is taken from the drain  

The CS amplifier provides **voltage gain** with a **180° phase inversion** between input and output.

For proper amplification, the MOSFET must operate in the **saturation region**.  
To ensure this, the operating point (Q-point) is selected such that:

```
VDS ≈ VDD / 2
```

This allows maximum symmetrical output voltage swing.

---

## Circuit Parameters

| Parameter | Value |
|------------|--------|
| Technology | 180 nm |
| VDD | 2 V |
| RD | ≈ 5 kΩ |
| NMOS L | 480 nm |
| NMOS W | 1.11 µm |
| Power Constraint | ≤ 0.5 mW |

---

## Procedure

### Model Inclusion
The 180 nm NMOS model file was included in LTspice using:

```
.include tsmc018(7).lib
```

---

###  Circuit Construction
The Common Source amplifier was designed with:
- VDD = 2V  
- RD ≈ 5 kΩ  
- NMOS: L = 480 nm, W = 1.11 µm  

---
### Given Parameters (From tsmc018.lib)
 
- Vth = 0.366 V  //threshold voltage
- Tox = 4.1 × 10⁻⁹ m  //oxide thickness
- μn (U0) = 273.80 cm²/V·s  //Electron mobility
- εr (SiO₂) = 3.9  //relative permitivity
- ε0 = 8.854 × 10⁻¹² F/m  //Permitivity of free space
- Power constraint: P ≤ 1.2 mW  

Since the input DC bias at the gate is 0.9 V,

VGS = 0.9 V  

As VGS > Vth (0.9 V > 0.366 V),  
In the above condition NMOS operates in saturation region.

### Step 1: Calculate Drain Current Using Power Constraint

Using:

P = V × I  

1.2 × 10⁻³ = 2 × ID  

ID = (1.2 × 10⁻³) / 2  

ID ≈ 0.6 × 10⁻⁴ A  

ID ≈ 0.6 mA  

let me consider Id = 0.2mA so we will get the power (p = I x V ) = 0.2m x 2 = o.4mW therefore the power is greater than the given power

### Step 2: Fix Q-Point

For maximum symmetrical swing:

VDS = VDD / 2  

VDS = 2 / 2  

VDS = 1 V  

### Step 3: Calculate Drain Resistor (RD)

RD = (VDD − VDS) / ID  

RD = (2− 1) / (0.2 × 10^-3)  

RD ≈ 5 kΩ  

### Step 4: Calculate Oxide Capacitance (Cox)

First calculate oxide permittivity:

εox = εr × ε0  

εox = 3.9 × (8.854 × 10⁻¹²)  

εox ≈ 3.45 × 10⁻¹¹ F/m  

Now,

Cox = εox / Tox  

Cox = (3.45 × 10⁻¹¹) / (4.1 × 10⁻⁹)  

Cox ≈ 8.41 × 10⁻³ F/m²  

### Step 5: Calculate Process Transconductance Parameter (kn')

Convert mobility to SI units:

μn = 273.80 cm²/V·s  
= 0.02738 m²/V·s  

Now,

kn' = μn × Cox  

kn' = 0.02738 × (8.41 × 10⁻³)  

kn' ≈ 230.6u A/V²  

### Step 6: Calculate Required Transistor Width (W)

Using MOSFET saturation equation:

ID = (kn'/2) × (W/L) × (VGS − Vth)²  

Given:

VGS = 0.9 V  
Vth = 0.366 V  

(VGS − Vth) = 0.534 V  

L = 180 nm = 180 × 10⁻⁹ m  

Substituting:

0.2 = (0.0002306 / 2) × (W / 180 × 10⁻⁹) × (0.534)²  

Solving,

W ≈ 1.11 µm  

After simulation tuning to obtain accurate Q-point:

Final selected width:

W = 3.92 µm  


### DC Operating Point from LTspice

ID ≈ 0.2 mA  
VDS ≈ 1 V  

Thus, the Q-point is successfully fixed near mid-supply.

###  DC Analysis (Q-Point Calculation)

To determine the operating point:

```
.op
.dc
```

The value of RD was adjusted to achieve:

```
VDS ≈ VDD / 2
```

---

###  Power Constraint Adjustment

The drain resistor (RD) and W/L ratio were tuned to obtain the required drain current while satisfying:

```
P ≤ 1.2 mW
```
The image shown below is the design of CS amplifier using TSMC 180nm technology library .LT spice is used to analyze the operating point,gain,and output characterstics.

![Image description](https://github.com/2024ecdeekshithagjc-bit/Linear-integreated-circuit-lab/blob/main/operating%20point.png?raw=true)
---
initially we have W = 1.11um that we have found before for that width we will be getting the value of current nearly equal to 150mA that is lessen than 200mA so in order to fix Id nearly equal to 200mA we should increase the width of the channnel because we know that width is directly propotional to the Id.if we increase the width then automatically current will increase so,
in the above image, we have got the value I(R1) = 0.000201416A for the width W = 3.92um

### Transient Analysis

To observe time-domain behavior:

```
.tran 5m
```

Input signal used:

```
SINE(0.9 10m 1k)
```

To obtain gain and bandwidth:

```
.ac dec 10 0.1 100G


- 180nm TSMC Model (tsmc018.lib)
- 
