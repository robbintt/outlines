## Convert audio to 1 channel wav for DeepSpeech

It is remarkable that recording sound is the hard part of DeepSpeech.

With deepspeech installed in a `virtualenv`, do the following.


### Use ffmpeg

1. Get ffmpeg: `brew install ffmpeg` or `apt install ffmpeg`
1. Convert to single channel 192kbps: `$ ffmpeg -i ~/Desktop/test_audio.m4a -ac 1 -ab 192k ~/Desktop/test.wav`
1. Run the demo: `deepspeech models/output_graph.pb ~/Desktop/test.wav models/alphabet.txt`