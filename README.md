MixAudio Plugin v1.2
What is this?
MixAudio lets you play internet audio streams on your Enigma2 receiver while watching TV. The main use case? Watching a football match on a foreign channel while listening to Arabic commentary from an online radio stream. Pretty handy, right?

Before You Start
Make sure you have:

* An Enigma2 receiver (works with OpenATV, OpenPLi, OpenBH, Egami, and most other images)
* Either GStreamer or FFmpeg installed (most images have at least one)
* A decent internet connection


Getting Around
When you open the plugin, you'll see a list of audio channels. Here's what the buttons do:
Navigation:

* Up/Down arrows - scroll through channels
* Left/Right arrows - switch between playlists
* OK - play the selected audio
* Long press OK - play the last audio you used
* Exit - close the plugin

Colored buttons:

* Green - stop audio and restore TV sound
* Red - delete saved settings for current TV channel
* Yellow - decrease audio delay
* Blue - increase audio delay

Other stuff:

* Menu - open settings
* Info - open playlist editor
* 0 - force EPG refresh


The Status Bar
At the bottom of the screen, you'll see something like:
● Vid: 10s | Aud: 500ms AL | AUT | GStreamer | EPG: 5m ago
What does it mean?

* The dot shows connection status (filled = connected, empty = disconnected, X = error)
* Vid: 10s = video is delayed by 10 seconds (timeshift)
* Aud: 500ms = audio delay in milliseconds
* AL = Anti-Latency mode is on
* AUT = Auto mute method
* GStreamer = current audio player
* EPG: 5m ago = when EPG was last updated


Settings Explained
Playlist Token
If you have a subscription, enter your token here. Press OK to type it in. The plugin will automatically download your channel list.
Audio Output
Two choices:

* GStreamer - the default, works well on most boxes
* FFmpeg - try this if GStreamer gives you problems

Honestly, just try both and see which one works better on your box.
Volume Boost
Goes from 1 to 10. Start with 1 or 2. If the audio is too quiet, bump it up. Going too high might cause distortion though.
Mix Audio

* Off = mutes the TV sound (most people want this)
* On = plays both TV sound and stream audio together

Mute Method
This is how the plugin silences your TV audio. Options:

* Auto Detect - let the plugin figure it out (recommended)
* setTarget - fastest method, works on OpenATV, Egami, foxBob, pure2
* ALSA - uses the sound system directly
* Device Rename - old school method, works everywhere but causes a brief channel restart

If Auto doesn't work, try the others one by one.
Timeshift Delay
This delays your video (in seconds) to sync with the audio stream. The audio stream is usually 5-15 seconds behind live TV, so you need to delay your video to match.
Start with something like 10 seconds and adjust from there.
Audio Delay Step
When you press Yellow/Blue to adjust audio delay, how much should it change? Options are 0.1, 0.2, 0.5, or 1 second. I usually keep it at 0.5.
Anti-Latency Mode

* On = faster response, less buffering, but might stutter on slow connections
* Off = more stable, but higher delay

Good internet? Turn it on. Slow or unstable internet? Turn it off.
Network Buffer
How much audio to buffer before playing. Range is 500ms to 10000ms.
Quick guide:

* Fast fiber connection: 1000-1500ms
* Normal broadband: 1500-2500ms
* Slow or unstable: 3000-5000ms
* Really bad connection: 5000-10000ms

Remember Timeshift
When enabled, the plugin remembers your delay settings for each TV channel. Next time you tune to that channel, it applies the same settings automatically.
Auto Start Audio
When enabled, if you've previously linked a TV channel to an audio stream, it will start playing automatically when you tune to that channel.

How to Use It (Step by Step)
First Time Setup

1. Open the plugin from your extensions menu
2. Go to Settings (Menu button) and enter your token if you have one
3. Go back to the main screen

Playing Audio

1. Find the audio channel you want in the list
2. Press OK to start playing
3. The TV audio should mute and you'll hear the stream

Syncing Audio with Video
This is the tricky part. The audio stream is usually delayed compared to live TV, so your video and audio won't match at first.
Here's what to do:

1. Watch the screen and listen to the audio
2. If the audio is BEHIND the video (you hear the goal after seeing it):

Increase Timeshift Delay in settings, OR
Press the Blue button to add audio delay


3. If the audio is AHEAD of the video (you hear the goal before seeing it):

Decrease Timeshift Delay, OR
Press Yellow to reduce audio delay



The Timeshift method is better for big adjustments (5+ seconds). The Yellow/Blue buttons are for fine-tuning.
Stopping Audio
Press the Green button. This stops the audio stream and brings back your normal TV sound.

Auto-Start Feature
Once you've set up audio for a TV channel, the plugin remembers it. Here's how it works:

1. You're watching BeIN Sports 1 (TV)
2. You start playing "Orange BN1" audio stream
3. You adjust the delays until everything syncs
4. You leave and watch something else

Next time:

1. You tune to BeIN Sports 1
2. Plugin automatically starts "Orange BN1"
3. Same delay settings are applied
4. No manual setup needed!

To remove this link, press the Red button while on that TV channel.

EPG Info
The plugin shows EPG (program guide) info for beIN Sports and SSC channels. You'll see:

* L before a program = it's live
* R before a program = it's a replay
* Start time
* Match or program name
* Next program coming up

EPG updates automatically every 30 minutes. Press 0 to force an update.

Troubleshooting
Audio won't play

* Check your internet connection
* Try switching between GStreamer and FFmpeg
* Look at /tmp/MixAudio.log for error messages

TV audio won't mute

* Try different Mute Methods in settings
* Make sure Mix Audio is set to Off
* Some images have issues with certain methods, experiment

Audio keeps cutting out

* Increase Network Buffer
* Turn off Anti-Latency
* Your internet might be too slow for streaming

Audio and video out of sync

* Adjust Timeshift Delay (for big differences)
* Use Yellow/Blue buttons (for small adjustments)
* It takes some trial and error to get it perfect

EPG not showing

* Press 0 to refresh
* Check internet connection
* EPG only works for beIN/SSC channels


Tips for Different Boxes
Older MIPS boxes (DM800, VU+ Solo, etc.)
These have limited processing power. Recommended settings:

* Anti-Latency: Off
* Network Buffer: 3000-5000ms
* Audio Output: Try FFmpeg first
* Volume Boost: Keep it low (1-3)

Newer ARM boxes (VU+ Duo 4K, Zgemma H9, etc.)
These can handle more. You can use:

* Anti-Latency: On
* Network Buffer: 1500-2000ms
* Audio Output: GStreamer usually works great
* Volume Boost: Whatever you need


Files Location
The plugin stores stuff in these places:

* /etc/enigma2/mixaudio.json - your custom playlist
* /etc/enigma2/mixaudio/simple_epg.json - cached EPG data
* /tmp/MixAudio.log - debug log (useful for troubleshooting)


Common Questions
Can I add my own audio streams?
Yes, edit the mixaudio.json file or use a token that provides your channels.
Does it work with IPTV?
Yes, any valid audio stream URL should work.
Why does audio stop when I change channels?
That's normal. Each TV channel can have its own linked audio stream. If the new channel has a saved link, audio will start automatically.
How much internet bandwidth does it use?
Audio streams are tiny - usually 64-128 kbps. Nothing compared to video streaming.
Can I use this for radio?
Absolutely. Any audio stream works, not just sports commentary.

Need Help?
If you're having problems, grab the log file at /tmp/MixAudio.log - it usually shows what went wrong. Include your box model and image name when asking for help.

That's it! Enjoy your matches with proper commentary. ⚽🎧
