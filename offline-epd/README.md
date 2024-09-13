This directory contains scripts for end-point detection. One or more audio recording is taken in and segmented for recognition using energy based voice activity detection.
The scripts are meant to be used at the start of speech recognition with a Kaldi ASR. The output audio segmentation file is used by Kaldi when decoding.

The directories steps and utils are needed and should be linked to from the WSJ recipe
ln -s $KALDI_ROOT/egs/wsj/s5/steps steps
ln -s $KALDI_ROOT/egs/wsj/s5/utils utils

Please refer to the information inside the repository [samromur-asr](https://github.com/icelandic-lt/samromur-asr) how to setup a Kaldi environment, e.g. via Docker.