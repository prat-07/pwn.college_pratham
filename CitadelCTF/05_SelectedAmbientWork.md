# Selected Ambient Work

## Challenge Description
The symphonic adventure does not end here. On the next floor, a single song keeps echoing through the floor, repeating in a haunting loop. Amid the sound, you find a note left by a past candidate. It hints that the song holds a secret message, hidden in plain sight, much like how Aphex Twin concealed his face within his music with the help of spectrograms.

To move forward, you must find the message hidden in this sound.

Note: Separate the words in the flag with `_` and make it UPPERCASE. Example: `citadel{S3L3CT3D_AMB13NT_W0RK}`

## Solve
**Flag:** `citadel{1_L0V3_1DM}`
- Upon opening the file, music starts playing. Some time into the music, a **morse code** plays.
- I try decoding it but it is distorted, maybe due to background noise. So, I run it on a spectrogram.
- I observe the flag format `citadel{` appears at around **1 minute** mark.
- Running the audio file in the morse decoder again around the **1 minute** mark and adjusting the frequencies mentioned by the spectrogram, I see many words.
- Since most of them do not make sense, I only try the 3 words: `1 L0V3 1DM` with the flag format to get the flag.
