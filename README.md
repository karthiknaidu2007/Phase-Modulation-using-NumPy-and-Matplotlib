# Phase-Modulation-using-NumPy-and-Matplotlib

### Aim
To implement and analyze phase modulation (PM) using Python's NumPy and Matplotlib libraries.   
### Apparatus Required
1.	Software: Python with NumPy and Matplotlib libraries  
2.	Hardware: Personal Computer Theory  
Phase Modulation (PM) is a technique where the phase of the carrier wave is varied in proportion to the instantaneous amplitude of the input signal (message signal). Unlike frequency modulation, where the frequency is varied, in phase modulation, the phase angle of the carrier wave changes with the amplitude of the message signal.  

The general form of a PM signal can be represented as:


<img width="306" height="241" alt="image" src="https://github.com/user-attachments/assets/b8d2db63-afe0-4bd8-8826-efc89a111423" />

### Algorithm

1.	Initialize Parameters:  
o	Set values for carrier amplitude (AcA_cAc), carrier frequency (fcf_cfc), message frequency (fmf_mfm), sampling frequency, and phase deviation sensitivity (kpk_pkp).  
2.	Generate Time Axis:  
o	Create a time vector for the signal duration based on the sampling frequency.  
3.	Generate Message Signal:  
o	Define the message signal as a cosine wave.  
4.	Generate PM Signal:  
o	Apply the PM modulation formula to obtain the modulated signal.  
5.	Plot the Signals:   
o	Use Matplotlib to plot the message signal, carrier signal, and phase-modulated signal.  


### Program

import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import hilbert

Ac = 14.6       
Am = 7.3        
fc = 7130    
fm = 713       
fs = 713000   
kp = np.pi / 4 


t = np.arange(0, 2/fm, 1/fs)
m = Am * np.cos(2 * np.pi * fm * t)
c = Ac * np.cos(2 * np.pi * fc * t)
s = Ac * np.cos(2 * np.pi * fc * t + kp * m)

analytic_signal = hilbert(s)
inst_phase = np.unwrap(np.angle(analytic_signal))
m_demod = (inst_phase - 2 * np.pi * fc * t) / kp
m_demod = m_demod - np.mean(m_demod)  
plt.figure(figsize=(10, 8))

plt.subplot(4, 1, 1)
plt.plot(t, m, color='blue')
plt.title('Message Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude (V)')

plt.subplot(4, 1, 2)
plt.plot(t, c, color='orange')
plt.title('Carrier Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude (V)')

plt.subplot(4, 1, 3)
plt.plot(t, s, color='green')
plt.title('Phase Modulated (PM) Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude (V)')

plt.subplot(4, 1, 4)
plt.plot(t, m_demod, color='red')
plt.title('Demodulated (Recovered) Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude (V)')

plt.tight_layout()
plt.show()
### Tabulation
![WhatsApp Image 2025-12-05 at 23 52 08_da671807](https://github.com/user-attachments/assets/7e84b8bb-c6e6-4450-bfbb-758b07059275)


### Output
<img width="562" height="449" alt="image" src="https://github.com/user-attachments/assets/382bdc19-370d-4962-9cf7-5de20f5f43de" />


### Result
The message signal, carrier signal, and phase-modulated (PM) signal will be displayed in separate plots. The modulated signal will show phase variations corresponding to the amplitude of the message signal.

