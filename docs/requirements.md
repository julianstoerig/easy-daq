# Requirements

## Goal

Build a minimal, documented data acquisition system (DAQ).

## Scope

### In Scope

- single analog input channel
- external ADC connected via bus
- input voltage range of at least 0V-3.3V
- continuous sampling and streaming to a Linux host over USB (CDC serial)
- Host-side capture to CSV and a simple plot
- basic documentation: wiring, build steps, sample measurements

### Out of Scope

- multiple channels
- differential inputs
- Wi-Fi / BLE streaming
- GUI application
- high-precision metrology or ENOB guarantees
- calibration beyond 0V and VCC offsets

## Functional Requirements

### Sampling

- samples shall be uniformly spaced in time, derived from a hardware timer or equivalent
- the device samples one analog input channel via an external ADC
- it supports a configurable sampling rate
- it has a minimum sustained output data rate of 10kS/s

### Streaming

- the device streams samples to a host over USB CDC serial
- packets include a monotonically increasing sequence number (wrapping allowed)

### Host capture


- a host tool shall capture the stream and write to a CSV file with columns `sequence_number,timestamp,value`
- the duration of the host's capture is either indefinite or a specified time

### Documentation

- the project documents
    - hardware wiring and pinout
    - firmware build and flash process from linux
    - host capture usage
    - sample recordings and plots
    
## Non-functional Requirements

### Reliability

- the system should run continuously for one hour of continuous streaming at 10kS/s with sample-loss rate of <0.1%
- if data cannot be transmitted quickly enough, the system should indicate this to the host
