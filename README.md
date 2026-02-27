# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
google collab
# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# -----------------------------
# Original Analog Signal
# -----------------------------
fs = 1000              # Sampling frequency
t = np.arange(0, 1, 1/fs)
fm = 5                 # Message frequency
x = np.sin(2*np.pi*fm*t)

# -----------------------------
# Ideal Sampling
# -----------------------------
Ts = 0.1               # Sampling period
ideal_sample = np.zeros(len(t))

for i in range(len(t)):
    if (t[i] % Ts) < (1/fs):
        ideal_sample[i] = x[i]

# -----------------------------
# Natural Sampling
# -----------------------------
pulse_width = 0.02
natural_sample = np.zeros(len(t))

for i in range(len(t)):
    if (t[i] % Ts) < pulse_width:
        natural_sample[i] = x[i]

# -----------------------------
# Flat-top Sampling
# -----------------------------
flat_sample = np.zeros(len(t))

for i in range(0, len(t), int(Ts*fs)):
    flat_sample[i:i+int(pulse_width*fs)] = x[i]

# -----------------------------
# Reconstruction (Low Pass Filter)
# -----------------------------
b, a = butter(4, 2*fm/fs)
reconstructed = lfilter(b, a, flat_sample)

# -----------------------------
# Plotting
# -----------------------------
plt.figure(figsize=(10,8))

plt.subplot(5,1,1)
plt.plot(t, x)
plt.title("Original Signal")

plt.subplot(5,1,2)
plt.plot(t, ideal_sample)
plt.title("Ideal Sampling")

plt.subplot(5,1,3)
plt.plot(t, natural_sample)
plt.title("Natural Sampling")

plt.subplot(5,1,4)
plt.plot(t, flat_sample)
plt.title("Flat-top Sampling")

plt.subplot(5,1,5)
plt.plot(t, reconstructed)
plt.title("Reconstructed Signal")

plt.tight_layout()
plt.show()
```
# Output Waveform

<img width="1212" height="600" alt="image" src="https://github.com/user-attachments/assets/1a1e6aa5-3e25-49bb-b8cf-31c5f6e64ef2" />
<img width="1157" height="398" alt="image" src="https://github.com/user-attachments/assets/a784872c-2a2c-4636-86f4-99070e23f0ae" />


# Results
Ideal,natural and flat top sampling are verified

# Hardware experiment output waveform.
