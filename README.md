# Testbook-packager
Node script for packaging ebooks with audio for testing purposes

This is a convenience script to shave time off of a workflow for packaging up ebooks with audio narration. It does not actually do anything but tie together existing services.

The script should be written with clear documentation and using all 'Q' promises, including for the webservice calls.

Script should output status periodically including number of books being processed currently etc.

### Here is the workflow:

1. Watch a folder for changes to subfolders, each containing 
   * one HTML file with an "assets" folder
   * one "audio" folder with a sequence of audio files (MP3, Flac or Wav)

1. Using LAME, Encode MP3 files into a final target encoding and also a compact encoding 
```
    Target: –preset voice
   Compact: -V 9 –vbr-new -mm -h -q 0
```

1. Extract text from HTML and place it in a ZIP file with the compact MP3 files

1. Send ZIP file to sync.readbeyond.it for syncing (http://www.readbeyond.it/sync/quickstart/index.html)

1. Check every 10 minutes with readbeyond for completion then download resulting SMIL data when complete

1. Create EPub3 with SMIL data, place in output folder (use something like epub-zip for packaging)

1. Create EPub2 with simulated SMIL (using https://github.com/pettarin/rb_smil_emulator), place in output folder