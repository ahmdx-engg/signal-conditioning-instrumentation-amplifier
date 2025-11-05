# Signal Conditioning Amplifier

This repository presents the design, evaluation, and optimization of a Signal Conditioning Amplifier Module developed for amplifying low-level analog signals from sensors, strain gauges, transducers, and other measurement devices.
The project focuses on analyzing the operational characteristics of the amplifier, identifying limitations, and implementing design modifications to enhance performance, stability, and linearity.

The amplifier employs the AD620A Instrumentation Amplifier, a 7660 charge pump voltage converter, and an LM358 operational amplifier configured as a unity-gain buffer. The module was evaluated through simulation and measurement to verify its amplification accuracy, noise performance, and response under various conditions.

## Introduction

Signal conditioning is a critical process in analog front-end design where weak or noisy signals from sensors are amplified, filtered, or offset-adjusted before being processed by data acquisition systems.
This project aims to design and evaluate a precision amplifier module capable of accurately amplifying small AC and DC input signals with minimal distortion and high stability.

The work emphasizes the evaluation of an existing amplifier circuit, identification of performance bottlenecks, and implementation of practical modifications to optimize gain control, power supply stability, and overall output quality.

## Module Overview

The amplifier module operates within a voltage range of 3.5 V to 10 V and provides an adjustable gain between 1.5× and 1000×, controlled by a potentiometer connected to the AD620A’s gain adjustment pins.
A 7660 voltage converter IC is used to generate the required negative voltage rail from a single positive supply, enabling the AD620A to operate symmetrically. The LM358 op amp acts as a unity-gain buffer at the output stage to provide current drive capability and isolate the amplifier from load variations.

The overall system achieves a nominal bandwidth of approximately 120 kHz at a gain setting of 100×, ensuring stable operation for low-frequency sensor and instrumentation applications.

## Theory of Operation

The input voltage (VIN) supplies the circuit with power ranging between 3.5 V and 15 V. The IC 7660 generates the negative voltage rail (V−) required for dual-supply operation, while the AD620A functions as the main amplification stage.
The amplifier’s gain is determined by the resistance connected between the AD620A’s gain control pins, which is adjustable through a 100 kΩ potentiometer.

After amplification, the signal passes to an LM358 op amp configured as a voltage follower, ensuring that the output maintains low impedance and faithfully reproduces the amplified signal without distortion or loading effects.
This configuration provides both high input impedance and stable output performance suitable for sensor signal conditioning applications.

## Evaluation and Limitations

During the evaluation phase, it was observed that the 7660 voltage converter introduced noticeable switching noise and output ripple on the negative voltage rail.
This electrical noise slightly degraded the amplifier’s performance, especially during high-gain operation. Additionally, the 7660 IC exhibited latch-up behavior at higher supply voltages, limiting the usable voltage range of the module.

The 100 kΩ potentiometer used for gain adjustment was found to provide uneven sensitivity across its range. At higher gain settings, small movements of the potentiometer resulted in large gain variations, reducing adjustment precision.

Despite these limitations, the amplifier performed effectively when properly filtered and adjusted, providing clean amplification of millivolt-level input signals.

## Design Improvements and Modifications

To address the identified limitations, several design enhancements were implemented and tested.

First, a bulk capacitor (ranging from 10 µF to 100 µF) was connected between the negative voltage output and ground. This addition significantly reduced ripple in the V− supply line, stabilizing the amplifier’s performance under dynamic load conditions.

Second, the 7660 charge pump was optionally removed to allow the use of an external negative voltage supply. This modification eliminated charge-pump-induced noise and enabled the circuit to operate from cleaner dual supply rails, expanding its usable input voltage range.

Third, the 100 kΩ gain potentiometer was replaced with a smaller value, such as 10 kΩ or 1 kΩ, improving linearity and control sensitivity during gain adjustments. In applications requiring fixed amplification, the potentiometer could be replaced entirely with a fixed resistor to ensure repeatable gain accuracy.

## Simulation and Analysis

The circuit was simulated to observe its behavior with both low-frequency and high-frequency input signals.
In the test setup, a 5 mV, 1 kHz sinusoidal input was applied to the amplifier. The output waveform captured on the oscilloscope showed a clean amplified signal with minimal noise, confirming proper operation of the differential stage and the unity buffer.

When powered through the internal 7660 converter, minor ripple artifacts appeared at the output, consistent with the charge-pump switching frequency. After adding bulk capacitance and filtering, these ripples were substantially reduced, leading to a cleaner output signal.

When the 7660 was replaced by an external dual supply (for example, ±5 V or ±9 V), the amplifier demonstrated further improvement in noise suppression, higher stability, and cleaner waveform reproduction. The amplified output reached approximately 500 mV peak-to-peak for a 5 mV input, indicating a gain of around 100×, consistent with theoretical predictions for the AD620A at the given resistance configuration.

The measured output bandwidth was consistent with the specified 120 kHz limit for a gain of 100×, with minimal phase distortion within the operating frequency range. The waveform retained its sinusoidal shape without clipping or overshoot, validating that the amplifier remained within its linear region of operation.

## Scope Capture Observations

Oscilloscope measurements confirmed that after implementing the proposed modifications, the amplifier produced a stable and noise-free output.
At an input of 5 mV (1 kHz), the output amplitude reached approximately 500 mV, corresponding to an amplification factor of 100×.

The signal displayed negligible phase shift between input and output, indicating effective buffering by the LM358 stage.
The removal of the 7660 charge pump and the addition of a filtering capacitor provided a noticeable improvement in waveform smoothness and noise performance. The ripple that was initially visible in the negative voltage rail was significantly minimized, confirming that the improvements directly enhanced circuit stability and accuracy.

## Recommendations

Based on the evaluation, several recommendations can ensure reliable long-term operation and precision performance.
It is preferable to power the amplifier using a clean external dual voltage supply rather than relying on the internal 7660 charge pump. This ensures noise-free operation and prevents voltage drop issues at higher gains.
For consistent gain control, it is advisable to replace the high-value 100 kΩ potentiometer with a 10 kΩ potentiometer or a fixed precision resistor, depending on the intended gain requirement.
Future designs may integrate improved voltage reference and filtering circuits to further minimize residual ripple and temperature drift.
