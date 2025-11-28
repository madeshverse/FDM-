# FDM-
# SIMULATION OF FREQUENCY DIVISION MULTIPLEXING (FDM) AND DEMULTIPLEXING USING SCILAB
### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

### EQUIPMENTS Needed

Computer with Scilab installed

### ALGORITHM

Define six different frequencies to generate six sine wave signals.

Generate the time vector to represent time samples.

Compute six sine signals for each frequency over the time vector.

Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.

Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.

Plot original signals, multiplexed signal, and demultiplexed signals for verification.

### PROGRAM

```
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

```

### GRAPH:
<img width="761" height="714" alt="image" src="https://github.com/user-attachments/assets/e6963b3d-495b-48e0-b0a5-4a5baf55f54d" />

<img width="758" height="719" alt="image" src="https://github.com/user-attachments/assets/c1c7cfe8-f284-4763-9bb9-fb2c996bf75b" />

<img width="759" height="718" alt="image" src="https://github.com/user-attachments/assets/ae7f731e-e51d-44e0-a904-ad3c75f34d20" />




### TABULATION:
<img width="758" height="1280" alt="image" src="https://github.com/user-attachments/assets/88465348-e206-4870-9ff5-f44dae4a618e" />



### RESULTS:

The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
