Hardware Requirements
ESP8266 board (Wemos D1 Mini or similar)
MAX7219-based 8x8 LED matrix
Analog sound sensor / microphone module
Wiring:
DIN to D7
CLK to D5
CS to D6
Sound sensor OUT to A0
Library
LedControl.h: Used to control the MAX7219 LED matrix.
Install via Arduino Library Manager if not already done.
Concept
The matrix shows a mirrored waveform that scrolls left with each frame.
Sound levels are read via the analog pin and averaged for smoothing.
Based on thresholds, it decides whether to draw a '-' character or a blank ' ' space.
The waveform consists of 4 characters (waveform[4]) that are displayed mirrored on the matrix (4 left + 4 right = 8 columns).

Main Logic
Read Sound:
32 analog readings are taken and averaged to smooth out the signal.
This average is constrained between noiseFloor (300) and peakLevel (700).
Map to Level:
The average is mapped to a level from 0 to 4.
If level = 1, a '-' character is added to the waveform; otherwise, it's a space.
Scroll Waveform:
The waveform array is shifted left to create a scrolling effect.
Display:
The waveform is rendered symmetrically on the 8x8 matrix using setChar().
Delay:
delay(40) controls the scroll speed.
