# SIMULATION OF FREQUENCY DIVISION MULTIPLEXING (FDM) AND DEMULTIPLEXING USING SCILAB

# AIM:
  To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

# EQUIPMENTS Needed
  Computer with Scilab installed
  
# ALGORITHM:

  Define six different frequencies to generate six sine wave signals.

  Generate the time vector to represent time samples.

  Compute six sine signals for each frequency over the time vector.

  Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.

  Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.

  Plot original signals, multiplexed signal, and demultiplexed signals for verification.

  # PROGRAM:
  ```
t = linspace(0, 1, 1000);
fs = 1000; 


freqs = [8, 10, 12, 14, 16, 18]; 

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = cos(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 100; 
cutoff_freq = 15 / (fs/2);  
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* cos(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1); clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2); clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3); clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

```
# GRAPH:
<img width="1917" height="1038" alt="image" src="https://github.com/user-attachments/assets/802a3ab7-419b-48d6-8fed-c2d493872409" />

<img width="1916" height="1047" alt="image" src="https://github.com/user-attachments/assets/f87e040b-0c74-4768-a68a-ab1dd9cde5dc" />

<img width="1919" height="1000" alt="image" src="https://github.com/user-attachments/assets/91f11f1b-7d87-4c9a-b47c-da9508f8dbbe" />

# TABULATION:
  ![WhatsApp Image 2025-11-28 at 12 15 02_8c3cbbcb](https://github.com/user-attachments/assets/65daa223-3cd9-46ff-b8e4-34ff4a790999)
  
  ![WhatsApp Image 2025-11-28 at 12 15 01_ff3ac8ff](https://github.com/user-attachments/assets/26ddb88e-5ba3-4f0f-b917-caa3e0473b6e)

# RESULTS:
  The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.




