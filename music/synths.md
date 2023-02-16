# Synthesis & Synthesizers notes
### What is synthesis?

The process of creating sounds using synthesizers is called **synthesis**. 

It is done so through the process of creating sound waves through electronic signals that are converter into sound waves using instruments and loudspeakers. 

We have many different types of synthesis and synthesizers

## Types of synthesis

### Additive Synthesis

Additive synthesis generates sound by adding the output of multiple sine wave generators. It works on the believe that any sound can be deconstructed into a bunch of sine waves fit together.

Alternative implementations may use pre-computed wavetables or the inverse fast Fourier transform.

### Substractive Synthesis
Subtractive synthesis works in the opposite way to additive synthesis. 

Subtractive works by subtracting harmonics from the original waveform. 

Then we proceed to remove particular frequencies with the use of a filter, until we get our desired sound.

It usually uses a rich harmonic waveforms like a saw or square wave.

### FM Synthesis
FM (Frequency Modulation) synthesis is the process of using one simple waveform to modulate the frequency of another, with the result then being used to modulate another simple waveform, which in turn can modulate another, and so on.


### Granular synthesis
Granular synthesis is a sound synthesis method that operates on the microsound time scale.

It is based on the same principle as sampling. However, the samples are split into small pieces of around 1 to 100 ms in duration. These small pieces are called grains. Multiple grains may be layered on top of each other, and may play at different speeds, phases, volume, and frequency, among other parameters.


### Wavetable synthesis
Used mostly to create realistic, natural sounds. Wavetable synthesis consists of isolating one loop of a wave and the synth then stores a digital representation of that sound in a table. 

Imagine it as a table of pre-saved waveforms, which can be recalled at anytime
