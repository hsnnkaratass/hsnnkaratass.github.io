---
title: "EE430 Digital Signal Processing Course Project 2023-2024"
excerpt: "Dive into the world of signal processing with EE430 projects—exploring innovative solutions in digital signal processing. From analyzing short-time Fourier transforms to experimenting with dual-tone multi-frequency signaling, each project unveils the power of DSP. 🌐🔊<br/><img src='/images/dsp.png' width='600' height='450'>"
collection: portfolio
---


# EE430 Term Project Part 1

## Overview
This project, conducted in collaboration with my friend [Hasan Hüseyin Karatas](https://www.linkedin.com/in/hasan-huseyin-karatas/), is part of the EE430 Digital Signal Processing course at METU's Department of Electrical and Electronics Engineering. The objective of Part 1 is to implement a computer program that computes and displays the magnitude of the short-time Fourier transform (STFT) of a signal.

## Project Description

### Short-Time Fourier Transform (STFT)
The STFT, discussed in Chapter 10 of the course's textbook (Discrete-time Signal Processing 3rd ed. Oppenheim, Schafer Pearson, 2010.), is a sequence of Fourier transforms applied to short consecutive segments of a long signal. It is useful for analyzing the temporal frequency content of a signal, often referred to as "Time Dependent Fourier Transform."

### Tasks

#### Data Acquisition
The implemented program can work with various input signals:
- Sound data from a microphone: Captures user voice or audio playback with an adjustable sampling rate.
- Sound data from a file: Processes .wav or .mp3 files, retrieving time-domain signals and sampling frequencies.

#### Data Generation
The system generates time-domain signals using simple mathematical expressions. Examples include sinusoidal signals and windowed sinusoidal signals with adjustable parameters.

#### Spectrogram
A MATLAB code is written to display the spectrogram of a discrete-time signal. This spectrogram is a plot of the magnitude of the STFT on the time-frequency plane, providing insights into the signal's temporal frequency content.

### Implementation and Deliverables
A graphical user interface (GUI) is created using MATLAB's app designer to facilitate data acquisition, data generation, and spectrogram visualization. The GUI allows users to adjust parameters such as sampling rate, amplitude, frequency, phase, and signal duration.

# EE430 Term Project Part 2

## Exploring DTMF Signaling

In this phase of the project, I delved into the fascinating world of dual-tone multi-frequency (DTMF) signaling with my friend Hasan again. The aim was to implement signal processing methods using MATLAB to generate, transmit, receive, and decode audio DTMF signals.

## Unveiling the Background

Signaling, the art of exchanging information among network devices, forms the backbone of communication sessions. From dialing a phone number to controlling automated equipment, signaling plays a pivotal role. The evolution from the clunky rotary phones to the sleek push-button dialing system marked a significant shift in telecommunications.

### DTMF Signaling

Unlike the pulse dialing of rotary phones, push-button dialing introduced the efficiency of DTMF signaling. Each key press generates a unique combination of two constant frequencies, paving the way for faster and more effective communication. In the realm of DTMF, every key is encoded using eight tones, split into four high and four low-frequency groups.

## Decoding the Secrets

### Formulas in Action

The encoding of a DTMF-encoded key involves mathematical wizardry, expressed as:

$s(k)(t; T_d) = (\sin(f_L(k)t) + \sin(f_H(k)t)) \cdot (u(t) - u(t - T_d))$

This formula encapsulates the essence of encoding, where $s$ is the time-domain signal, $k$ is the key index, $f_L(k)$ and $f_H(k)$ are low and high frequencies, and $T_d$ is the signaling duration per key.

### Sequencing the DTMF

Given a sequence of numbers $x[n]$, the DTMF-encoded sequence $m(t; T_d, T_r)$ can be expressed as:

$ m(t; T_d, T_r) = \sum s(x[k])(t - k(T_d + T_r); T_d)$

Here, $T_r$ is the resting duration between two consecutively pressed keys.

## Deliverables

### Transmitter Panel Highlights

- A sleek push-button keypad,
- A dynamic display field showcasing pressed keys,
- A handy reset button for a clean slate,
- Adjustable parameters for signaling duration $T_d$, resting duration $T_r$, and amplitude,
- A visual representation of the DTMF-encoded sequence,
- An artistic display of the signal's spectrogram,
- Convenient buttons for saving and playing the generated audio signal.

### Receiver Panel Charm

- A user-friendly start/stop button for seamless listening,
- Visually stunning displays of the received time-domain signal and its spectrogram,
- A switch for selecting the decoding algorithm,
- A field to showcase the magic of the decoded signal.

# Github Repo

For an in-depth exploration, feel free to dive into the [GitHub repository](https://github.com/ahmetcankardes/EE430-Digital-Signal-Processing-METU-EEE-Project). You can see more details about the code and used algorithms. Thanks for visiting 😃
