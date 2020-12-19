# Tutorial for SuperSX prototype 3

Note: 

SuperSX must be placed on the C drive. 

You are going to need a tool that can make changes to .big files, like finalbig. Finalbig is included with SuperSX.

You can contact me on email: kris.supersx@gmail.com, youtube: https://www.youtube.com/channel/UCqo34dlxornriXOMfCI0JiQ, reddit: https://www.reddit.com/user/Kris2ffer/

I would appreciate if you send me the music files you create, or make a donation if you have found this tool useful.

Paypal: paypal.me/mppro

Special thanks to Tsukiyo and Zenloup for feedback during development of this tool.

## About SuperSX and the music in SSX
The tool is currently using existing music files as a template. This means you must make and mix segments that are structured in the exact same way as the template used. They must also be of the same length and should use the same beats per minute. You can find bpm of songs here: https://songbpm.com/. When you're done making your mix, you export it as wav files and use SuperSX to convert it. There are two ways of converting your music, either as one wav file, or one file for each segments. The latter option is preferred. There are however only a few songs that can currently be used as templates. The songs are listed below, but only the last 3 have support for segmented exports.

* Swollen Members - Deep End (92 bpm)
* Basement Jaxx - Do Your Thing (124.87 bpm)
* X-ecutioners - Like This (139 bpm)
* Queens of the Stone Age - No One Knows (165 bpm)
* Yellowcard - Way Away (180 bpm)
* Dilated Peoples - Who's Who (97.1 bpm)
* Black Eyed Peas - Labor Day (104 bpm)
* The Faint - Glass Danse (130 bpm)

There are 3 files associated with each song. 2 .mus files and 1 .mpf file. The biggest mus file contains the song itself with remixes and looping segments for different places and situations on the track. The small one, ending with loops0.mus, contains looping audio that plays when you get big air (I'm going to call this the airloop), and the sound effects for when you start and restart a big challenge. The mpf file tells the game how and when to play the content of the other 2 files. The tool can make the 2 mus files, but not the mpf file for now. That will probably be added in the future.

## Making the music
The interactive music of SSX is beat based. When the game transitions the music from "normal" to cave remix, the audio should have been edited in such a way that there is a seamless transition in terms of the beat. The beats must be placed in the same way at the start and end of all segments. A metronome beat should loop perfectly when a segment is played consecutively. 

![](/tut-met-bars.png)

The game will play the audio at a lower volume than it normally would on your computer depending on how much the audio is “compressed”. This means that the audio must often be boosted/amplified first. To identify if your music must be boosted, simply look at the wave form and see if it fills almost the entire audio space. 

Boosting the audio in Audacity:
First select all audio, then go to Effect -> Compressor. Adjust Threshold and Ratio to your needs. All music is different and require different adjustments. This is just something that you have to experiment with. Make sure the “Make-up gain for 0 db …” and “Compress based on peaks” options are selected.

Here is an axample of audio that will be loud enough in game. It can also be a little less extreme, but it is better to make it too loud than too quiet, as the volume for individual songs can be adjusted down in a config file.

![](/wave-example.png)

The documents in the segments folder tells you the layout of the music. You should use the info in these documents to cut and mix your music. Many segments have a normal part, and a secondary part that plays after you crash. These segments are shown as a and b. 

For example in bep-laborday-segments.txt. The beginning starts on segment #8 and points to segment #7. Segment 8 is 18,456 seconds long and #7 is 23,07 seconds long. In your audio editor, make a cut after that amount of time and export each part. This should be after making sure your music adapted to the correct bpm if it already wasn't. 

The segments also have alternative versions that play when you crash. Often they are instrumental only versions of the main version. You can use the same audio clip for both so the muscic won't change when you crash.

Now these files can be either placed in the segments folder if you want to convert each segment seperately, or in a single project that will contain all of the music and mixes for caves etc that will be exported as a single file. The segments must be in the same order as they are in the template song.

The airloop must be at a certain length, should be the same bpm as the song and should obviously loop well. This file must be saved as airloop.wav and placed in the same folder as the tool. You can choose to not make an airloop if you don’t want to.

Note: 

* Some segments, for big challanges or cave remix, will change tempo.
* **The airloop must be exported as mono.**
* I have gotten feedback that the tool wouldn't properly convert the files at 41.1 Hz but got it working at 48 Hz


### Big challenge sound effects
The sound effects that plays when you start and restart a Big Challange can be modified for each song. The audio files for these sound effects are in the bc folder. You can replace them with any sounds you want. Just remember to use the same names.

## Conversion
If you want to convert using one file, place the file in the same folder as the SuperSX tool, and name it music.wav. For segments, place your files in the segments folder and name them according to the contents of the txt files in the segments folder like 01.wav, 02.wav 03a.wav, 03b.wav etc. Exporting your music as segments will give more accurate results. Run the batch files with "segments" in their name to convert segments. If you get the error message "sx.exe has stopped working", then try adding extra silence to the segment that happened on. It's fine if the duration of a segment is longer.

SuperSX will make a file called newMus.mus, and airloop.mus if you made an airloop file.

## After conversion
It is possible the conversion will fail sometimes. If there are leftover files in the temp folder that are 0 kb, then it failed the conversion for some reason. To fix this you can simply make the duration of your files a bit longer. Just adding extra silence will be enough. This extra bit of the audio will not be included in the final result, it will just help with the conversion for some odd reason.

After successfully converting your music, rename your new mus files to whatever you like and add them to one of the MUSIC.big files. Finally, it’s time to edit the music.inf playlist.inf file, in the config folder.

Add your song to the music.inf file by copying the information og the song you used as a template. Paste it a the bottom. You can paste it whereever you want, but the list of songs in game is based on the ordering of the songs in the music.inf and playlist.inf documents. What index has been selected in your custom playlist remains unchanged. This means that if you add a new song at the top of music.inf, the songs selected to be part of your playlist in-game will change. 
Change the id in the square brackets to a new id for your song. This will be used in playist.inf and is supposed to be unique. 

**Pathlevel** is the volume of your song. You should initially set this to 100, then test how it sounds like in game. If the volume still sounds like it is too low, then it must be boosted with an audio editor. Look at Making the music section.

**Asynclevel** is the volume of teh airloop. Do the same as with Pathlevel.

**Musdata** and loopdata must be changed to the names of your new mus files. 

**Pathdata** can be left as it is. You can reference the mpf file of your template song. No need to make a copy of it.

**Ducktoloops** tells the game if it should lower the volume of your song and play the airloop during big air time. If you don't have an airloop, then add "DUCKTOLOOPS = 0" to the configuration. 

**Sedvalue** is the introduction DJ Atomika gives your song. -1 gives no introduction. 999 will give you a generic introduction. Can also use 15.

You can also change how much the song cuts off with **Lowpass**.

After editing music.inf, add your song id to playlist.inf at the bottom. It should be in teh same order as music.inf. If the order is wrong, the game is very likely to crash between heats in a race. 

If you just want to replace a song then you don't have to copy paste the data. Just edit the data like explained above.
