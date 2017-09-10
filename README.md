# Precord
Precord mp3,wav,ogg,aac,flac recorder/player with rec, play,pause, and duration, and interface to Pscheduler


NOTE WELL: Please remember to delete your old ~/.precord config directory before installing this latest version.

Important note: Make sure you are using the latest Precord. Some earlier versions suffered from arecord having a flaw in its VU meter code as decribed in the link below (the arecord VU code used to overwrite system file /dev/null which could cause many system-related problems; e.g. the old bug caused wireless connectivity not to work according to one report). Versions of Precord and pAVrecord published since Jan 2014 do not suffer from that arecord bug.

http://murga-linux.com/puppy/viewtopic.php?p=784184#784184

Changes 9.0.3:

# (YMD)2014/08/03: changed hijack ext to .hijack; Removed old 'slave' addon code. Hijack addon modules allow developer to add to or change code functionality/codec commands etc without needing to edit the main program script. Details in second post of pavrecord thread, which also provides the same addon ability.

Fixed record Duration not working. Modified such that most functionality no longer requires ffmpeg (which was previously used in playback code). Can now also control playback (but not record) of video files too if mplayer on system.

One version now only. Tested on Slacko 6 beta, Precise 5.7.1 and DebianDog.

Major config GUI modification.
Can use avconv if available.
Selects appropriate AAC encoder.
As per pAVrecord, Precord now includes hijack expansion capability to allow modular plugin addition of new main code, new functions, new gui panels and new gui general config buttons:

http://www.murga-linux.com/puppy/viewtopic.php?p=656913#656913

Notes for Precord mp3, wav, ogg, acc(faac), and flac recorder and player with pause controls and auto config saving:

If precord ever fails to start, its config file is probably corrupted so simply delete your old /root/.precord config directory and precord will automatically rebuild it the next time it is re-started. Its config file is not known to become corrupted in normal use though.

Uses ffmpeg for ogg recording if oggenc is not available.

Precord has the advantage over, for example, mhWaveEdit, in that it records straight to mp3, wav or ogg, so doesn't need to use the hard disc for temporary storage of huge intermediate files.

It depends on arecord and lame for recording, and ffmpeg and aplay for playback; these are all standard core apps in Puppy

For vorbis ogg Precord uses oggenc for recording if it is available, otherwise it uses ffmpeg.

Precord has an inbuilt interface to Pschedule, so you can also use it for very versatile timed-recording (over, days, months, and years...). It can also record any sound coming through your soundcard (e.g. radio streams). Indeed, 01micko's pupradio/tv program automaticaly includes a button to call up Precord once Precord is installed. You just need to select appropriate Mixer input channel instead of Mic input using retrovol or alsamixer.

The provided dotpet installs an entry/icon for the program in JWM Start menu -> Multimedia -> Precord mp3,wav,ogg recorder/player

As well as having a GUI interface, Precord can also be used from the commandline. It reads commandline args of the form:

[action][filename][duration] via stdin (e.g. pipe).

For example
Code:	

precord [with no args starts GUI version]

precord  rec  /mnt/home  anything.mp3 10 [records without GUI; assumes mp3 previously selected in precord config GUI]

or via pipe:

echo  rec  /mnt/somewhere  testrec.ogg  25 | precord -
[assumes ogg previously selected in precord config GUI]

precord  play  /root  out.mp3 [plays without GUI]

echo  play  /mnt/sdb1  out.mp3 5 | precord -
[also plays without GUI; here using duration of 5 seconds]

If no outfile or duration parameter is supplied, precord uses previous configuration as defaults.

precord quit
does what you'd expect...

precord --help
for commandline usage 
