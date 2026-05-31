##### \###GNSS ATTACK SIMULATION FLOWGRAPH###





###### **1.** Create Real GNSS Signal



Action:

Add **Signal Source block**



Settings:

Frequency = 1000

Amplitude= 0.5



Purpose:

Represents legitimate GNSS satellite signal







###### **2.**  Add Noise Source (Jamming Attack)



Action:

Add **Noise Source block**



Settings:

Noise type= Gaussian

Amplitude= 3



Purpose:

Simulates jamming attack

Creates interference in signal





###### **3.** Create Fake GNSS Signal (Spoofing)



Action:

Add **Another Signal Source Block**



Settings:

Frequency = 1005

Amplitude = 2



Purpose:

Simulates Spoofed Signal

Represents attackers sending fake navigation data







###### **4**. Combine Real Signal and Noise



Action:

Add **Add block (add1)**



purpose:

Combines:

&#x20;     Real Signal

&#x20;     Noise (Jammer)

Creates jamming condition





###### **5**. Combine Jammed Signal with Fake Signal



Action:

Add **Add block (add2)**



Purpose:

Combines :

&#x20;   Jammed Signal

&#x20;   Fake Signal

Simulates combined attack (Jamming + Spoofing)





###### **6.**  Apply Low Pass Filter



Action:

Add **Low Pass Filter**



Settings:

Cutoff Frequency = 1500

Transition Width = 500

Window = Hamming



Purpose:

Reduces high-frequency noise

Acts as a basic anti-jamming technique





###### **7**. Add Throttle Block



Action:

Add **Throttle**



Settings:

Sample Rate = samp\_rate



Purpose:

Controls data flow

Prevents system overload





###### **8.** Visualize  Frequency Domain



Action:

Add **QT GUI Frequency Sink**



Purpose:

Displays signal spectrum

Shows:

&#x20;       Signal peaks

&#x20;       Interference

&#x20;       Spoofed Signals







###### **9.**  Visualize Signal Over Time



Action:

Add **QT GUI Waterfall Sink**



Purpose:

Shows signal behavior over time

Helps detect continuous interference





###### **10.**  Visualize Waveform



Action:

Add **QT GUI Time Sink**



Purpose:

Displays waveform distortion

Helps analyze impact of attacks

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

\###OUTPUT ANALYSIS###

**1. Waterfall Sink**



Observation:

Bright band in center shows strong signal

Surrounding area shows noise



Purpose:

Displays signal power over time



Key Point:

Strong signal = GNSS signal

Noise = jamming interference





**2. Time Sink**



Observation:

Two signals visible (real + spoofed)



Purpose:

Shows waveform of signals



Key Point:

Overlapping signals indicate spoofing attack



**3. Frequency Sink**



Observation:

Peak at center frequency

Noise spread across spectrum



Purpose:

Displays signal in frequency domain



Key Point:

Peak = real signal

Noise = jamming effect


\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_



This demonstrates GNSS signal behavior under jamming and spoofing attacks with basic mitigation using filtering.

