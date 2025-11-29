# MAWESS – Multi-component Autoencoder for Waveform Enhancement and Signal Separation

> Open-source AI denoiser and source separator for ocean-bottom seismometers (OBS) and hydrophones –  
> from earthquakes to whales, ice, and ships.

---

## 🌊 What is MAWESS?

MAWESS is an open-source AI tool to **clean and separate complex marine seismic and acoustic records**.

It adapts modern *self-supervised* and *physics-informed* autoencoder methods from audio processing to:
- **Ocean-bottom seismometers (OBS)** – including under-ice deployments  
- **Hydrophones** – for future extensions

MAWESS can:
- Suppress hard ocean noise (waves, currents, instrument noise)
- Preserve real **seismic signals** (earthquakes, microseisms)
- Separate **environmental and anthropogenic sources**:
  - sea-ice deformation
  - iceberg noise
  - swell-driven microseisms
  - whale vocalizations
  - ship traffic
  - instrument-induced tremor

MAWESS is built to be:
- **Free and open** (MIT license)
- **Accessible** to *students, small labs, NGOs, and independent scientists*
- **Usable** through:
  - a Python API,
  - a command-line interface,
  - and a **GUI with intuitive visualizations**

---

## 💡 Why MAWESS?

Ocean and polar data are expensive and logistically hard to acquire, but **many amazing open datasets already exist** and are underused because they are extremely noisy and difficult to interpret.

MAWESS aims to:

- **Unlock underused marine archives** (AWI/DEPAS, IRIS, GFZ/GEOFON, RESIF, etc.)
- Make advanced denoising and source separation **available to everyone**, not just a few well-funded groups
- Support:
  - **Earthquake and microseism studies**
  - **Whale and marine mammal monitoring**
  - **Sea-ice and iceberg dynamics**
  - **Ship traffic and noise impact studies**
  - **Citizen science & NGOs** working on ocean and whale protection

If you:
- care about **whales and noise pollution**,
- work with **Arctic / Antarctic / ocean recordings**,
- or just want cleaner waveforms for your seismology workflows,

**MAWESS is for you.**

---

## ✨ Key Features (planned)

### Core denoising & separation

- Self-supervised **multi-component autoencoder**  
- Trained on real OBS data, including under-ice deployments
- Separation of:
  - Long-period & short-period **microseisms** (LPDF, SPDF)
  - **Sea-ice HF noise** and storm-induced ice collisions
  - **Iceberg tremor & bursts** (future models)
  - **Hydrodynamic / instrument tremor** (strumming, cable noise)
  - **Ship noise** (narrowband harmonic lines)
  - **Whale calls & other bioacoustic signals** (future hydrophone model)
- Outputs:
  - Cleaned waveforms
  - Per-source components (earthquake / microseism / ice / ship / etc.)
  - Uncertainty maps
  - Time–frequency masks

### Tooling & integration

- **Python library** (PyTorch, NumPy, ObsPy)
- **Command-line tools** for batch processing
- **SeisBench-compatible** model interface (planned)
- Smooth integration in:
  - ObsPy workflows
  - Jupyter notebooks
  - Docker / container environments

### User-friendly GUI

We are designing a **graphical user interface** with:

- Drag-and-drop support for miniSEED / SAC / WAV / HDF5/Zarr
- Interactive **spectrograms & waveform views**
- “Before vs after” denoising comparisons
- Per-source component sliders (e.g. *mute ships*, *enhance whales*, *show ice noise only*)
- Export of:
  - cleaned traces,
  - masks,
  - summary reports (PNG/PDF/CSV)

The goal: **non-experts should be able to use MAWESS within minutes.**

---

## 🐳 Phase 2 Vision: Open Ocean Noise & Whale Portal

In the **second stage** of the project, we plan to build a **web portal** that:

- Continuously ingests **open OBS and hydrophone data**
- Runs MAWESS models in the background
- Provides **live and historical maps** of:
  - Noise levels
  - Sea-ice deformation activity (from seismic noise)
  - **Whale presence probability** in specific areas (where bioacoustic data are available)
- Exposes:
  - Simple dashboards for NGOs and citizen scientists
  - Downloadable preprocessed datasets for research and teaching
  - Transparent **model cards & documentation** on limitations and training data

This is especially aimed at:
- **Whale protection organizations**
- **Environmental NGOs**
- **Students & educators** interested in marine soundscapes

---

## 🚀 Project Status

> **This repository is under active development.**

---

## 🧱 Architecture (high-level)

MAWESS uses a **multi-branch masked autoencoder** with physics-informed constraints:

- **Low-frequency branch** (0.01–1 Hz):  
  LPDF, SPDF, IG waves  
- **Mid-frequency branch** (1–15 Hz):  
  SPDF2, certain whale calls, ship components
- **High-frequency branch** (> 5 Hz):  
  Sea-ice deformation, storm collisions, ship & instrument harmonics

All branches feed into a **shared latent space**, where components are separated and reconstructed through dedicated heads (earthquakes, microseisms, ice, ship, etc.), plus an uncertainty head.

You don’t need to understand the ML details to use it,  
but if you do: check the `docs/` for architecture notes and examples.

---

## 🧰 Installation (planned interface)

Once the first release is out:

```bash
# Using pip
pip install mawess

# Or from source
git clone https://github.com/anuota/mawess.git
cd mawess
pip install -e .
