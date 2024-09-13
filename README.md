# Endpoint Detection in Automatic Speech Recognition (ASR)

![Version](https://img.shields.io/badge/master-darkgreen)
![Python](https://img.shields.io/badge/python-3.8+-blue?logo=python&logoColor=white)
![CI Status](https://img.shields.io/badge/CI-[unavailable]-red)
![Docker](https://img.shields.io/badge/Docker-[unavailable]-red)

This repository focuses on the concept of Endpoint Detection in Automatic Speech Recognition systems. Endpoint detection, also known as Voice Activity Detection (**VAD**) or Speech Activity Detection (**SAD**), is a fundamental component in ASR pipelines.

Endpoint detection aims to accurately identify the beginning and end of speech segments within an audio stream.

## Overview

This repository has been created by the [Language and Voice Lab](https://lvl.ru.is/) at Reykjavík University and is
part of the [Icelandic Language Technology Programme](https://github.com/icelandic-lt/icelandic-lt).

- **Category:** [ASR](https://github.com/icelandic-lt/icelandic-lt/blob/main/doc/asr.md)
- **Domain:** Server
- **Languages:** Python, Shell
- **Language Version/Dialect:**
  - Python: 3.8+
  - C++: C++14 (Kaldi)
- **Audience**: Developers, Researchers
- **Origin:** [endpoint detection](https://github.com/cadia-lvl/end-point-detection)

## Status
![Experimental](https://img.shields.io/badge/Experimental-darkviolet)

This repository is experimental as it doesn't provide a complete solution for VAD. The offline script is not using a state-of-the-art VAD model. Nowadays, deep learning models are used for VAD.<br>

Please refer to these alternatives:
- [NeMo MarbleNet](https://github.com/NVIDIA/NeMo/blob/265bd739c77c86ac423942d650eed6fc232e4fc6/tutorials/asr/Voice_Activity_Detection.ipynb)
- [Silero VAD](https://github.com/snakers4/silero-vad) 
- [PyAnnote Audio](https://github.com/pyannote/pyannote-audio)
- [SpeechBrain](https://github.com/speechbrain/speechbrain)

# Description
This repository demonstrates offline endpoint detection using **energy based voice activity detection** with the Kaldi ASR framework. Offline endpoint detection refers to using the local machine to process audio files and segment them into speech and non-speech regions. Refer to the description in [offline-epd/README.md](offline-epd/README.md).

It's also possible to perform online endpoint detection using the [Uberi's Speech Recognition](https://github.com/Uberi/speech_recognition). This toolkit uses various speech recognition APIs to transcribe speech in real-time. Refer to the description in [online-epd/README.md]([online-epd/README.md).

## Table of Contents
  * Installation
  * Running
  * Licence
  * Authors/Credit
  * Acknowledgements

## Installation

* The onine EPD script works with [Uberi's Speech recognition library](https://github.com/Uberi/speech_recognition).
  * The Speech recognition package need PyAudio. I had to install it like this:
      `sudo apt-get install portaudio19-dev python-all-dev python3-all-dev` and then `pip install pyaudio`
* The offline EPD scripts are intended to work within [Kaldi](https://github.com/kaldi-asr/kaldi).
* Follow the installation instructions from there and nothing else is needed.
* Alternatively, follow the instructions in the [samromur-asr](https://github.com/icelandic-lt/samromur-asr) repository to setup a Kaldi environment, e.g. via Docker.

## Running
Both online and offline scripts are not supposed to be whole recipies. This in only one part of what it needed when transcribing audio with an ASR, so running these parts doesn't give any final output. The code is supposed to help someone along with using an ASR. The online EPD script needs to be changed according to which ASR you plug in. The offline EPD can be put as a first step in a run script which applies a Kaldi ASR.

For the offline script to work one need to have a Kaldi directory properly set up with symlinks to steps and utils in the Wall street journal recipe:
`ln -s $KALDI_ROOT/egs/wsj/s5/steps steps`
`ln -s $KALDI_ROOT/egs/wsj/s5/utils utils`

The offline EPD script can be run like this:
`bash segment_single_raw_audio.sh audio/audiofile1.mp3 output/audiofile1`

The outputdir audiofile1 will be a typical Kaldi directory, but not it containd the new file: segments

The online script can be run like this:
`python run.py`

It will continue recording and recognizing till you kill it with ctrl-C. Since I don't know the future use case for this I let this part wait. One can decide whether to save the audio to a file or not.

## License
MIT License

Copyright (c) 2020 Language and Voice Lab

## Acknowledgements
This project was funded by the Language Technology Programme for Icelandic 2019-2023. The programme, which is managed and coordinated by [Almannarómur](https://almannaromur.is/), is funded by the Icelandic Ministry of Education, Science and Culture.
