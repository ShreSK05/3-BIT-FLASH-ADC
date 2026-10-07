  # 3-Bit Flash ADC

## Overview

This project presents the design and transistor-level simulation of a **3-Bit Flash Analog-to-Digital Converter (ADC)**.

A Flash ADC is one of the fastest ADC architectures. It uses a resistor/reference ladder to generate reference voltages and multiple comparators to compare the analog input simultaneously. The comparator outputs form a thermometer code, which is converted into a 3-bit binary output using a thermometer-to-binary encoder.

The complete design consists of:

- Reference voltage ladder
- 7 comparators
- Thermometer-code generation
- Thermometer-to-binary encoder
- 3-bit digital output

---

## ADC Architecture

For an N-bit Flash ADC, the number of comparators required is:

**Number of Comparators = 2^N - 1**

For a 3-bit Flash ADC:

**2^3 - 1 = 7 Comparators**

Therefore, this design uses **7 comparators**.

### Block Diagram

                       ANALOG INPUT
                            |
                            v
                  +-------------------+
                  | Reference Voltage |
                  |      Ladder       |
                  +---------+---------+
                            |
             +--------------+--------------+
             |              |              |
             v              v              v
          +------+       +------+       +------+
          | CMP1 |       | CMP2 |  ...  | CMP7 |
          +--+---+       +--+---+       +--+---+
             |              |              |
             +--------------+--------------+
                            |
                            v
                    THERMOMETER CODE
                            |
                            v
                +-----------------------+
                | Thermometer-to-Binary|
                |       Encoder        |
                +-----------+-----------+
                            |
                            v
                         D2 D1 D0
                       3-Bit Output


## Simulation Parameters

| Parameter | Value |
|---|---|
| Supply Voltage (VDD) | 1.8 V |
| Reference Voltage (VREF) | 1.8 V |
| Input Signal (VINP) | Sine Wave |
| Input Frequency | 20 kHz |
| Input Amplitude | 800 mV |
| Input DC Level | 800 mV |
| Clock Voltage | 0 V to 1.8 V |
| Clock Period | 195.61 ns |
| Clock Rise Time | 100 ps |
| Clock Fall Time | 100 ps |
| Clock Pulse Width | 95.31 ns |
| NMOS Width | 2 µm |
| NMOS Length | 180 nm |
| PMOS Width | 4 µm |
| PMOS Length | 180 nm |
| NMOS Model | nmos2v |
| PMOS Model | pmos2v |

---

# Block 1: Comparator

The comparator compares the analog input voltage with a reference voltage and produces a digital logic output.

The comparator is one of the main building blocks of the Flash ADC. Seven comparators operate at different reference voltage levels to generate the thermometer code.

## Comparator Performance

| Parameter | Value |
|---|---|
| Supply Voltage | 1.8 V |
| Regeneration Time | 123 ps |
| Input Offset Voltage | 2.452 mV |
| Clock-to-Q Delay | 515 ps |
| Average Supply Current | 118.39 nA |
| Average Power Consumption | 213.1 nW |

---

## Comparator Calculations

### 1. Regeneration Time

The regeneration time is calculated as:

**Treg = Tstart - T(90%)DP**

### Simulation Result

**Treg = 123 ps**

---

### 2. Input Offset Voltage

The input offset voltage is the small differential input voltage required between the two comparator inputs to make the output switch or produce an equal output condition.

### Simulation Result

**VOS = 2.452 mV**

---

### 3. Clock-to-Q Delay

The measured clock-to-Q delay is:

**Clock-to-Q Delay = 515 ps**

---

# Block 2: Thermometer-to-Binary Encoder

The thermometer encoder converts the comparator outputs into a 3-bit binary code.

The encoder receives the 7-bit thermometer code from the comparator block and generates the digital output:

**D2 D1 D0**

---

## Encoder Power

| Parameter | Value |
|---|---|
| Supply Voltage | 1.8 V |
| Average Supply Current | 18.59 pA |
| Average Power Consumption | 33.46 pW |

---

## Truth Table

The relationship between the comparator outputs and the 3-bit digital output is:

| C7 | C6 | C5 | C4 | C3 | C2 | C1 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 |
| 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 1 | 1 |
| 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |
| 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 1 |
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

---

# Overall ADC Results

The complete Flash ADC was simulated using a **1.8 V supply**.

| Parameter | Value |
|---|---|
| Supply Voltage | 1.8 V |
| Average Supply Current | 464.7 µA |
| Average Power Consumption | 836.46 µW |

---

# Key Performance Parameters

| Parameter | Result |
|---|---|
| ADC Resolution | 3-bit |
| Number of Comparators | 7 |
| Supply Voltage | 1.8 V |
| Reference Voltage | 1.8 V |
| Input Frequency | 20 kHz |
| Input Amplitude | 800 mV |
| Regeneration Time | 123 ps |
| Input Offset Voltage | 2.452 mV |
| Clock-to-Q Delay | 515 ps |
| Average ADC Current | 464.7 µA |
| Average ADC Power | 836.46 µW |

---

# Transistor Parameters

## NMOS

| Parameter | Value |
|---|---|
| Width | 2 µm |
| Length | 180 nm |
| Model | nmos2v |

## PMOS

| Parameter | Value |
|---|---|
| Width | 4 µm |
| Length | 180 nm |
| Model | pmos2v |

---

# Features

- 3-bit Flash ADC architecture
- 7 parallel comparators
- Reference voltage ladder
- Thermometer-code generation
- Thermometer-to-binary conversion
- Transistor-level implementation
- 1.8 V supply operation
- Comparator performance analysis
- Power consumption analysis
- Input offset voltage analysis
- Regeneration time analysis
- Clock-to-Q delay analysis

---

# Results Summary

| Parameter | Result |
|---|---|
| ADC Resolution | 3-bit |
| Number of Comparators | 7 |
| Supply Voltage | 1.8 V |
| Reference Voltage | 1.8 V |
| Input Frequency | 20 kHz |
| Input Amplitude | 800 mV |
| Regeneration Time | 123 ps |
| Input Offset Voltage | 2.452 mV |
| Clock-to-Q Delay | 515 ps |
| Average ADC Current | 464.7 µA |
| Average ADC Power | 836.46 µW |
| Comparator Current | 118.39 nA |
| Comparator Power | 213.1 nW |
| Encoder Current | 18.59 pA |
| Encoder Power | 33.46 pW |

---

# Conclusion

A **3-Bit Flash ADC** was designed and simulated using a transistor-level implementation.

The architecture uses seven comparators to compare the analog input with different reference voltages. The comparator outputs form a thermometer code, which is converted into a 3-bit binary output using a thermometer-to-binary encoder.

The design operates with a **1.8 V supply** and uses a **20 kHz, 800 mV amplitude sine-wave input**.

The comparator achieves a measured **123 ps regeneration time**, **2.452 mV input offset voltage**, and **515 ps clock-to-Q delay**.

The complete Flash ADC has an average supply current of **464.7 µA** and an average power consumption of **836.46 µW**.
