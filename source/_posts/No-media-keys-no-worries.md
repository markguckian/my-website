---
title: No media keys - no worries
date: 2017-04-01 23:13:51
tags:
---

I got a new laptop at work today. A high speced HP ZBook G3.

All was going well until I installed Spotify and found I couldn't automatically play/skip/pause songs from the keyboard. 
Despite providing a full sized keyboard HP have not included media keys.
I had got used to using media keys to control my music in my old laptop so had to find some way of replicating that ability.

Turns out there is an easy solution: [AutoHotKey](https://autohotkey.com/)

#### Steps:
1. Download AutoHotKey
2. Create a AutoHotKey script: 
   * Right-click in any folder
   * Click **New** -> **AutoHotKey Script**
   * Add the following:
      ```
      ;next song
      +F12::	;the + means shift
      Send {Media_Next}
      return

      ;previous song
      +F11::
      Send {Media_Prev}
      return

      ;play/pause
      +F7::
      Send {Media_Play_Pause}
      return
      ```
      (I picked those function keys as they don't have a function assigned to them on the ZBook)
3. Save the file, name it something like 'media-hotkeys.ahk'
4. Run the script:
   * Right-click on the file
   * Click **Run Script**
   * SHIFT + f11 should move to the previous song
   * SHIFT + f12 should move to the next song
   * SHIFT + f7 should toggle play/pause
5. If these work, compile the script to an exe:
   * Right-click on the file
   * Click **Compile Script**
6. Include the compiled in the Windows startup folder to ensure it is always running:
   * Create a shortcut to the compiled exe
   * Open ```%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup```
   * Copy the shortcut file to this folder

Done!
