# Charge Sampler - Integrate and Hold Amplifier using Cadence Virtuso

# Introduction (Analog to Digital Converter)

<div style="text-align: justify;">
  
Broadband data converters play a crucial role in broadband digital communication systems and high-end measuring equipment. The performance of communication or measuring systems is often limited by the sample rate, effective resolution, and bandwidth of these data converters.

Analog-to-Digital Converters (ADCs) are essential for converting continuous analog signals into discrete digital signals. By sampling the analog signal at regular time intervals, ADCs produce digital outputs in binary form. They are widely used in applications such as audio devices, sensors, and communication systems, enabling the digital processing of analog data.

IEEE Reference: https://ieeexplore.ieee.org/document/9482511

Textbooks: 1. **RF Microelectronics**, Razavi, Behzad, 2. Design of **Analog CMOS Integrated Circuits**, Razavi, Behzad, 3. **Analysis and Design of Analog Integrated Circuits**, Paul R. Gray, Paul J. Hurst, Stephen H. Lewis, and Robert G. Meyer.
   
</div>

# Objective and Tasks

<div style="text-align: justify;">
  
The primary goal of this task is to analyze and design a Charge Sampling Integrate-and-Hold Circuit (IHC) using IHP 130-nm G3 Aluminum SiGe BiCMOS Technology in Cadence Virtuoso. The circuit design is based on the Short Time Integration (STI) concept. The design process involved implementing five separate circuit blocks. Each block was individually biased and subsequently adjusted to align with the neighboring stages. Current mirrors were used for biasing, ensuring that all transistors operated in forward bias, except for certain circuits functioning as switches, where forward bias could not always be maintained.

Once each circuit block was fully operational, they were interconnected to form the complete circuit. The combined circuit's characteristics were then analyzed. Layouts for each circuit block were subsequently designed, and Electromagnetic (EM) simulations were conducted using RF Pro. These simulations assessed the impact of parasitic elements, specifically resistance (R), capacitance (C), and inductance (L). The S-parameter sub-circuits were extracted to evaluate signal propagation and component interactions. Based on the results, modifications were made, and the layouts were redesigned until the desired performance was achieved.

The thesis aims to develop an IHC based on the STI approach, achieving a 3 dB bandwidth exceeding 70 GHz. The charge sampling technique was analyzed mathematically, and the performance of the charge sampling architecture was evaluated to achieve a higher Effective Number of Bits (ENOB) within the 0–90 GHz range at a sampling rate of 10 GS/s. Finally, the results from reference papers and EM simulations were compared with current state-of-the-art designs to assess the circuit’s effectiveness.

</div>


# Block Diagram using Cadence Virtuso Environment

![image](https://github.com/user-attachments/assets/48e5a719-69ce-40eb-920c-19149b0ef2ca)

<div style="text-align: justify;">
  
The circuit comprises an inverter, two tunable delays, two switches, a subtractor, and an integrator. The control signals include Integrate, Track 1, and Track 2. The track signals are derived as the inverse of the integrate signal, delayed by Tunable Delay 1 and Tunable Delay 2. The integration time is determined by the delay between the two tunable delay components, which in turn defines the sampler's bandwidth.

The tunable delay technique minimizes the difference in delay between the two components, enabling the achievement of very high bandwidth. The switches manage the integration time based on these tunable delay elements. After the integration time \( T_i \), the integrator’s input signal is reset to 0 by subtracting the outputs of the two switches. Consequently, the subtractor must generate extremely short pulses and be optimized carefully to maximize the bandwidth of the sampler.

</div>

# Final Test Bench

![image](https://github.com/user-attachments/assets/e6c9dff8-0ba4-44ec-bddc-cda1029f158f)


<!-- # Full Layout Design -->
<!-- ![Without_Bondpads](https://github.com/user-attachments/assets/d1fdc34e-309b-4847-9d0d-a975bfd4e9df) -->

<!-- # Full IC Chip Design (Bondpads, Slots, Fillers and Transmission Lines) -->
<!-- ![Bondpadswithfillers](https://github.com/user-attachments/assets/ff517c14-4fa9-4f55-a8cd-622736aae213) -->

<div style="text-align: justify;">

After completing the layout design, several critical steps must be taken to ensure the design functions correctly. These include adding bond pads, incorporating fillers, creating slots, and ensuring proper impedance.

**Bond pads** are crucial for connecting the internal circuitry of the chip to external components. They should be placed near the edges of the layout to facilitate bonding. Proper placement and sizing are essential to prevent issues during the bonding process.

**Slots** in the metal layers is another vital step. These slots help reduce stress and prevent cracks from forming during fabrication. They also manage the thermal expansion and contraction of the metal layers, ensuring the structural integrity of the chip.

**Fillers** are used to maintain consistent metal layer density across the chip, which is crucial for uniform manufacturing. This helps prevent issues such as metal peeling, cracking, or mechanical stress. The process design kit (PDK)-specific density rules can be verified using a Design Rule Check (DRC), and fillers can be added automatically using dedicated tools in Cadence.

</div>

<div style="text-align: justify;">

# Steps in Chip Design and Analysis

**1. Full Layout Design**: Developed the complete layout of the chip, ensuring accurate placement and routing of components to meet the desired specifications.
Electromagnetic Simulations (RF Pro, Keysight)

**2. Electromagnetic Simulations (RF Pro, Keysight):** Performed EM simulations using RF Pro software to analyze and optimize high-frequency behavior, focusing on parasitics and electromagnetic effects.
RC Extraction

**3. RC Extraction:** Extracted resistance (R) and capacitance (C) values from the layout to evaluate and minimize their impact on circuit performance.
Impedance Calculation (ADS, Keysight)

**4. Impedance Calculation (ADS, Keysight):** Used Advanced Design System (ADS) to calculate impedance values for matching network designs, ensuring proper signal transmission.
Transmission Line Design for Input Signals

**5. Transmission Line Design for Input Signals:** Designed transmission lines optimized for the input signal's frequency range, maintaining signal integrity by minimizing reflections and losses.
FFT Analysis with Coherent Sampling

**6. FFT Analysis with Coherent Sampling:** Conducted Fast Fourier Transform (FFT) analysis using coherent sampling to verify signal integrity and ensure accurate frequency-domain representation.
Post-Layout Simulations

**7. Post-Layout Simulations:** Simulated the design after layout completion to validate functionality and performance, accounting for layout parasitics and real-world effects.
Voltage and Current Drop Analysis

**8. Voltage and Current Drop Analysis:** Analyzed voltage and current drops from the schematic level through the S-parameter file to ensure power delivery and performance consistency.
S-Parameter Analysis

**9. S-Parameter Analysis** Performed S-parameter analysis to evaluate the layout's high-frequency performance, including reflection and transmission characteristics.

**10. Metal Selection Based on Current Densities:** Evaluated and selected metals for routing layers based on their current-carrying capacities and resistance to electromigration.

**11. Via Analysis:** Properly analyzed via placements to ensure reliable connections between metal layers and to minimize resistance and inductance.

**12. Metal Layer Usage:** Utilized multiple metal layers effectively:
                           Metal 1 to Metal 5: Used for routing signals and maintaining connectivity.
                           Top Metal 1 and Top Metal 2: Leveraged for power signals due to their higher current-carrying capabilities.

**13. Bond Pads, Fillers, and Slots Installation:** Integrated bond pads, fillers, and slots into the layout to prevent cracking and ensure structural integrity during the fabrication process.

</div>


# Combination of all the blocks for different frequencies

<div style="text-align: justify;">
  
The schematic simulation below illustrates the operation of all the blocks working together. It begins with the integrate input pulse signal, which is inverted by an inverter and sent to Tunable Delays 1 and 2. These delays shift the Track 2 signal by 4 ps. The resulting signals are then fed into the CML switch, which tracks the input signal when the switch is ON and resets it when it is OFF.

The outputs from the CML switches are directed to the subtractor, where the difference between the two signals generates spikes resembling Gaussian pulses. The pulse width corresponds to the integration time. During the rising edge of the integrate signal, the integrator performs integration and holds the output steady until the signal turns off.

**Total Power Consumption** is ca. 550mW

</div>

**Schematic simulation for 1 GHz input frequency and sampling frequency of 10 GS/s.**

![image](https://github.com/user-attachments/assets/c84d1aaa-f73e-44fc-a1bb-a3547ace0b1c)

# Conclusion

<div style="text-align: justify;">

The operating principle of STI sampling using the IHC was thoroughly examined both theoretically and practically, accompanied by a comprehensive mathematical analysis. 

This sampler demonstrated a 1 dB large-signal bandwidth of 61.5 GHz and a 3 dB bandwidth of 70.1 GHz. At a sampling rate of 10 GS/s, the output signal achieved an ENOB exceeding 5 bits across the frequency range of 25 GHz to 85 GHz. A notable advantage of this charge sampler is that its bandwidth is determined by the integration time rather than the integration capacitor. As a result, the capacitance in the STI sampler can be increased to minimize noise without affecting bandwidth. However, a higher capacitance reduces the sampling frequency, introducing a trade-off between noise and sampling frequency for the STI sampler.

</div>

