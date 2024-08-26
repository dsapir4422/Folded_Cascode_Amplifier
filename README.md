# Folded_Cascode_Amplifier
In This project I will show the design of a folded cascode amplifier in 65[nm] technology.

## Design specification
* VDD = 1.8[V]
* DC Gain > 60 dB
* PM > 45 [deg]
* GBW > 4[MHz]
* C load = 5[pF]
* DC offset < 0.5mV
* Ibias = 10[uA]

## Design calculations & consideration
We will design the following circuit (Taken from Razavi's book) - 

<img width="500" alt="image" src="https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/abefbd7e-05cd-44f3-85f7-3e89e3ae08e6">

Which consist of a "separated" GM stage (M1,M2) and Rout stage(M5-M10).
* M1,M2 - GM stage, should have low Vdsat ~ 50[mV] for high gm.
* M5,M6 - NMOS current source with Vdsat ~ 200[mV]
* M9,M10 - PMOS current source with Vdsat ~ 100[mV]
* M3-M8 - cascode transistors for better Rout with Vdsat ~ 100[mV]

$A_v = gm_1 * [(gm_3 * ro_3 * (ro_1||ro_5)] || (gm_7 * ro_7 * ro_9)$

**Note** - In order to reduce mismatch we will need the current in GM/Rout branch to be at ratio = 1-1.5 .

The folded cascode will drive an NMOS source follower, therefore input pair should be PMOS based.

For circuit stabilization, we will use a small capacitor (the circuit has only 1 pole).

**Bias circuits**

We will bias the top PMOS transistors with low voltage cascode current mirror, while keeping the bias transistor Mb1 Vdsat - $V_{dsat,Mb1} > V_{dsat,M7} + V_{dsat,M9}$

NMOS transistors will be biased using a basic current mirror from Ibias, same goes for Iss.
**********

## Design Test Bench and schematic
Test bench which consists the op-amp and a source follower - 

<img width="500" alt="image" src="https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/c4d2ce2f-0d85-4119-b40c-b5b082081df7">

Folded cascode - 

<img width="914" alt="image" src="https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/e44f48cb-d3f1-44f4-8ce5-df8d0220ca55">

## Simulation results 
DC sweep - output linear range is roughly from VSS to VCC - Vt - 2*Vdsat
![image](https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/11a5220c-0a4c-4e77-8043-d82f96d94b2b)

DC offset = Vout - Vin is low at linear range ~ 250[uV]
![image](https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/00451570-7255-487f-a92c-144ebaf5c0ca)

Gain & Stability (TT corner) - we can see Gain = 63dB, PM = 53[deg] and GBW ~ 4.5[MHz]

![image](https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/e1f1013d-14d2-4e3d-a5be-b82bd3595052)

Transient analysis - slight over-shoot
![image](https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/87224162-7b02-4bee-ae12-7f468db30c64)

Monte Carlo on V_offset @ Vin = 500[mV]. The input referred offset ranges from -2.5 to +2.5mV for 3-sigma
<img width="500" alt="image" src="https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/f50c2cc4-3b45-4f00-9771-61319d9f12da">

**Corners**

![image](https://github.com/dsapir4422/Folded_Cascode_Amplifier/assets/87266625/bc401323-3dbf-4204-8e3b-1cd66610163a)

