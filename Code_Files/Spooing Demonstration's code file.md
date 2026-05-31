###### \###GNSS Spoofing Signal Simulation###





**0.**  Set Sample Rate Variable


Action:
Add **Variable block**


Settings:

|ID = samp\_rate|Value = 32000|
|-|-|



Purpose:
Defines global sample rate used across all blocks



**1.** Create Real GNSS Signal



Action:
Add **Signal Source block**



Settings:

|Frequency = 1000|Waveform = Sine|Sample Rate = 32k|Amplitude = 1|
|-|-|-|-|



Purpose:
Represents legitimate GNSS satellite signal





**2.**  Create Spoofed Signal



Action:
Add **second Signal Source block**



Settings:

|Frequency = 1200|Waveform = Sine|Sample Rate = 32k|Amplitude = 1|
|-|-|-|-|



Purpose:
Simulates fake signal sent by attacker





**3.**  Combine Both Signals



Action:
Add **Add block**



Purpose:
Merges real and spoofed signals together simulating a spoofing attack





**4.**  Visualize Spectrum



Action:
Add **QT GUI Sink**



Settings:

|FFT Size = 1024|Bandwidth = 32k|
|-|-|



Purpose:
Displays frequency spectrum showing strong peak at 73.81 dB indicating spoofing

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_



\###Output Analysis###



Strong peak at 0.77 kHz, 73.81 dB detected
Authentic GNSS signals are significantly weaker
Sharp peak confirms spoofing signal presence

