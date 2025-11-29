# MAWESS
Multi-component Autoencoder for Waveform Enhancement and seismic Signal Separation

We are currently developing 

→ **MAE-style masked self-supervised autoencoder
	•	physics-informed losses
	•	time–frequency U-Net
	•	optional small variational latent layer**


##🎯 Signal classes MAWESS aims to separate*

###1) Iceberg burst noise

Broadband (1–40+ Hz), chaotic, fracturing, “white” spectrum.

Model strategy:
	•	treat bursts as a separate “noise layer” in a multi-head separator
	•	do time-domain separation (waveform U-Net) because bursts are impulsive

###2) Iceberg tremor**

Monochromatic, drifting fundamental, sometimes with overtones.

Strategy:
	•	frequency-domain MAE
	•	harmonic-coherence loss
	•	multi-resolution STFT

###3) Iceberg harmonic tremor**

Multiple stable harmonics (up to 30), chevron patterns.

Strategy:
	•	frequency-domain U-Net
	•	harmonic structure regularization
	•	temporal attention to capture minutes–hours long patterns

###4) Hydrodynamic OBS noise (currents)**

Turtle-back shapes, rising/plateau/dropping fundamental frequencies.

Strategy:
	•	latent clustering + classification
	•	separating into “ocean-coupling noise” components

###5) Whale and ship signals**

To avoid them being mistaken for iceberg tremor:
	•	use separate latent heads
	•	pretrained WhaleNet-style filters (transfer learning)
	•	add contrastive separation
