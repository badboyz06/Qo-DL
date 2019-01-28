# Qobuz-DL
Tool written in Python to download MP3s & FLACs from Qobuz for Windows.   
Latest version: 28th Jan 19 - Release 3a.


![](https://thoas.feralhosting.com/sorrow/Qobuz-DL/1.jpg)
![](https://thoas.feralhosting.com/sorrow/Qobuz-DL/2.jpg)
![](https://thoas.feralhosting.com/sorrow/Qobuz-DL/3.jpg)

# Setup
## Mandatory ##
The following need to be inputted into the config file:
- App id
- App secret - you can get your app id & app secret by contacting Qobuz (you can also use the ones already in the config file).
- Email address
- Format id - download quality (5 = 320 kbps MP3, 6 = 16-bit FLAC, 7 = 24-bit / =< 96kHz FLAC, 27 = best avail - 24-bit / >96 kHz =< 192 kHz FLAC).
- MD5 hashed password
- User auth token - you'll be given this automatically if it's not already inputted in. App id & app secret are required.
- Naming scheme - file naming scheme (1 = "01. ", 2 = "01 -").
- Cover size - cover size to request from API (1 = 230x230, 2 = 600x600).

**You can't download ANY tracks with a free account.**
## Optional ##
- Comment tag 

You can specify what you want to be put into the comment field in your tracks. Special characters will be escaped.

# Usage
It's simple; input Qobuz Player or Qobuz store URL. 
Ex. 
```
https://play.qobuz.com/album/hxyqb40xat3uc
https://www.qobuz.com/xxxx/album/mount-to-nothing-sangam/hxyqb40xat3uc
```
# Update Log
## 26th Jan 19 - Release 1 ##
## 27th Jan 19 - Release 2 ##
- Mp3 support.
- Max downloadable tracks per album 50 -> 100.
- More efficient code for checking if files exists & deleting them if they do. 
- Integrated Get UAT into main exe.
- implemented invalid URL input handling.
- Crash fixed when attempting to download albums with video goodies.
- Ability to choose naming scheme via config file.
- Ability to choose which size album cover to fetch via config file.
## 27th Jan 19 - Release 2a ##
- Check for empty user_auth_token field would prevent users from getting to the url input screen, thus not allowing them to get the uat.
## 28th Jan 19 - Release 3 ##
- Unlimited tracks downloadable per album.
- Code clean up - 1800 lines down to 400! Mainly thanks to the above.
- "<" & ">" handled in file names.
- uat input removed - you'll be given your uat automatically now if it's needed.
## 28th Jan 19 - Release 3a ##
- Handled the below. This happens when you try to download tracks using a free account. You can't.
```
TypeError: 'NoneType' object is not subsciptable Failed to execute script Qobuz-DL
```
# Misc Info
Tested on Python v3.6.7.  
Used libraries:
- codecs
- configparser
- datetime
- glob
- hashlib
- mutagen
- os
- pathlib
- re
- requests
- shutil
- sys
- time
- urllib.request

The following tag fields are wrote to:
- album
- albumartist
- artist
- comment (depends on users' choice)
- title
- track
- tracktotal
- year

The tracktotal field won't be written to mp3s. Instead, the track total will be written to the track field. Ex: (current_track)/(total_tracks) 

Misc:
- If a digital booklet is available, it will be downloaded and put in its respective album folder.
- Video goodies must be purchased. Qobuz-DL can't get them for you (API returns "None" when requesting).
- Downloaded tracks are put in the "Qobuz-DL Downloads" folder. Ex. (Qobuz-DL Dir)\\Qobuz-DL Downloads\\(albumartist) - (albumtitle)\\(tracks)
- Any specials characters that Windows doesn't support in filenames are replaced with "-" (except "<" & ">" for now).  
- If an album folder needs to be made, but already exists, it and its contents will be deleted.  
- If a track is unavailable for streaming because of right owner restrictions, it will be skipped (some record labels disallow streaming of their music).
- id3v2.3 tag format is used for mp3 tags.
- **If the following files exist in the current working dir, they'll be deleted: (1-100).flac/.mp3, cover.jpg, booklet.pdf. This is to avoid any filename clashes.**

If you need to get in touch: Sorrow#5631

# To do
- GUI version.
- Fix known issues.
- Progress bar?
- Download playlists.
- Implement Japanese translation.
- General code clean up.
- Commandline options.
- Download from list of urls.
- Reduce size of executable (exclude libs etc.).

# Known issues
- Albums with more than one disks will be treated as single-disk albums.

To make this clearer, track 1 of disk 2 wouldn't be tagged as track #1, but as the track after the last track of disk 1.

- Printing languages like Chinese, Japanese & Korean to the console prints garbage instead.

This doesn't effect anything else in the code; tracks containing any of the above languages will still download & tag correctly.
