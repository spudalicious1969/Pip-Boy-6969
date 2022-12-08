# Pip-Boy 6969

![screenshot](https://user-images.githubusercontent.com/5025384/206265810-fdfbf51f-83c6-498c-adf8-223f271cda92.png)


## Description

---

This is my working version of a [Pip-Boy](https://fallout.fandom.com/wiki/Pip-Boy) .  I'm not smart enough to make anything new so, this is a mishmash of different little programs.    Below are the things I used to make it work however, I am on a mac.  If using linux or WSL on windows, there are better options for a couple things.  I'll try to list what I consider "better" as we go along.

## Terminal Emulator.

--- 

The terminal emulator used is [Cool Retro Term](https://github.com/Swordfish90/cool-retro-term) .   I use a modified version of the Monochrome Green profile which is included in this repository (`pipboy.json`)  

**Setup - Linux and MacOS:**

Easy as pie.  Just follow the instructions on the github page.

**Setup - Windows:** 

The setup process for Windows is a bit more involved.  There are a couple things I will link below for Windows installation.   This may take some experimentation on your part but, worse case worst.   You ain't gonna break anything critical if it all goes bork.

- **Install WSL2 (Windows Subsystem for Linux):** 
  
  - [Run Linux GUI apps with WSL | Microsoft Learn](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps)

- **Install Cool-Retro-Term (Methods to try in preferred order):**
  
  - *Install using Snap Store:*   WSL2 is now (supposedly) supporting linux GUI apps. If it is a perfect world you will install and instantly be able to run.
    
    - ```bash
      sudo snap install cool-retro-term
      ```
  
  - *Install using Ubuntu repository:*  See above, as related to perfect worlds
    
    - ```bash
      sudo apt install cool-retro-term
      ```
  
  - *Compile the mother fucker:*  Yet again...  In a Perfect world, it will run with GUI without extra hassle
    
    - First get the dependencies
    
    - ```bash
      sudo apt install qtquickcontrols2-5-dev qml-module-qt-labs-platform qml-module-qtquick-controls qml-module-qtquick-layouts qml-module-qtquick-localstorage
      ```
    
    - Then compile
    
    - ```bash
      # Get it from GitHub
      git clone --recursive https://github.com/Swordfish90/cool-retro-term.git
      
      # Build it
      cd cool-retro-term
      
      # Compile
      qmake && make
      
      # Have fun!
      ./cool-retro-term
      ```
  
  - **The less than perfect world** 😩
    
    - Soooo, this is probably where we land.  Because luck is never on our side.
    
    - After you have installed Cool-Retro-Term in WSL, if the perfect world failed to materialize for us, we must rely on Xming-server to provide us with a GUI server.   It works fine.  I've done it before.  Uses a bit more resources but, not disasterously so.
    
    - Follow this guide from STEP 3 onward
    
    - [Cool-Retro-Term-Windows10.md · GitHub](https://gist.github.com/h3r/2d5dcb2f64cf34b6f7fdad85c57c1a45#step-3---connecting-seamlessly-to-windows-10)

## The Meat and Gravy

--- 

Everything from here out will run in any terminal emulator.  If for some reason Cool-Retro-Term flops entirely for you, you can still run all of this in any terminal emulator like Windows Terminal or PuTTY.   I beleive Windows Terminal even has some retro effects you can apply.

### Music

I use Musikcube.  Mostly because it is a pretty nice little command line music app that does support a mouse if we choose. 

- Head on over to the Musikcube [releases page](https://github.com/clangen/musikcube/releases) .   If you are on a mac, just grab the mac version.   If on Windows, since we are building in WSL, I'm going out on a limb and say to download the .deb.

- Mac install is very self evident.   
- WSL install
  
  - ```bash
    sudo dpkg -i musikcube_x.y.z_ubuntu_xxx_amd64.deb
    sudo apt-get install -f
    /usr/bin/musikcube
    ```

- Once Musikcube is open.   
  
  - Press "s" to enter settings menus
  
  - Add a folder for the music library 
    
    - I use this music to remain true to the project: - Fallout 4 OST (Diamond City radio station) 
    
    - I found it on SoulSeek cuz i'm shady. But you do you.
    - Here is a youtube playlist with the same songs [FO4DCR](https://youtu.be/N7Fpp2VT5lk)    
    - For color theme: Select "8 colors (compatability mode)" Other themes that utilize 256 colors will not display correctly in a monochrome session

**Other Music Player Options:**  

You can use any CLI music player here.  I just choose Musikcube because I only want to use local files.   [CMUS](https://github.com/cmus/cmus) or [MPD](https://github.com/MusicPlayerDaemon/MPD) are also great choices

Sometimes, I also stream audio directly from YouTube.  My forced choice due to MacOS is [yewtube](https://github.com/iamtalhaasghar/yewtube) .   If on linux, for streaming audio from YouTube, I much prefer [pipe-viewer](https://github.com/trizen/pipe-viewer).    

In addition there are CLI options out there for Spotify (I think)

### ASCII ART

Use whichever ascii art file you like.  I have included `pipboy.txt` in this repository

We will view our ascii art in vim.  It may already be installed but, just in case.

```bash
sudo apt install vim
```

or for mac

```bash
brew install vim
```

### Time and Date

The time and date are a little clock program called `tty-clock`

```bash
sudo apt install tty-clock
```

or for mac

```bash
brew install tty-clock
```

### Matrix looking shit

The matrix looking stuff can be done with a few different programs.   The one I use is [unimatrix](https://github.com/will8211/unimatrix) .  This is a pretty dang light python application.    Python should already be installed for Mac and WSL users.   Install `unimatrix` with pip3

```bash
pip3 install git+https://github.com/will8211/unimatrix.git
```

**Other Options:**   I haven't had success with anything like this on Mac but, in Linux (assuming also WSL).   Another *Coooler* option is to run a command line music visualizer in this pane instead.  [cava](https://github.com/karlstav/cava) would be a great choice.   I may get it working on mac sooner or later.  

## Putting it all together

--- 

To put all these little CLI programs on one screen, each in their own tidy little pane, we will use a terminal multiplexer.   My choice is [tmux](https://github.com/tmux/tmux/wiki) .  Another option is [screen](https://www.gnu.org/software/screen/) if you are old sk00L like that.

TMUX is frigging rad on so many levels.  BUT, I will not go into all of that here.  If you are unfamiliar, here is a nice little introduction.  [A Gentle Introduction to tmux. What is tmux? | by Alek Shnayder | HackerNoon.com | Medium](https://medium.com/hackernoon/a-gentle-introduction-to-tmux-8d784c404340)

Let's get it installed!

- For MacOS
  
  - ```bash
    brew install tmux
    ```

- For Linux (WSL)
  
  - ```bash
    sudo apt-get install tmux
    ```

-  Once installed.  Verify it installed correctly
  
  - ```bash
    tmux -V
    ```

I have included a very bare bones `tmux.conf` file for us to use, included in this repository.   As a side note, these conf files can be used to make tmux super useful and look extremely cool.  If you chose to play with that a bit.

- Place the `tmux.conf` file in your home folder and rename to `~/.tmux.conf`   note the period at the start of the filename.
  
  - ```bash
    mv ~/tmux.conf ~/.tmux.conf
    ```

## Let's Get teh Party Started

--- 

Ok!  We're near the end now! 

- Place the file `pipboy` found in this repository in your `/usr/local/bin` folder.  This is the same for both macos and wsl.   

- Edit the file `pipboy` to reflect the correct path to your ascii art.

- Make sure `pipboy` is owned by you.  
  
  - ```bash
    sudo chown YOURUSER:YOURGROUP /usr/local/bin/pipboy
    ```

- Make sure `pipboy` is executable.
  
  - ```bash
    chmod +x /usr/local/bin/pipboy
    ```

- Now! fire up Cool-Retro-Term (should now be in start menu or applications)

- We can now run our new executable script `pipboy`  press ENTER and let it rip.
  
  
  ![screenshot-pipboy-start](https://user-images.githubusercontent.com/5025384/206265945-bdbae230-c3b3-4e9d-8955-362323ca20f6.png)


- At this point, you will want to adjust the font size by holding the CTRL button and pressing the +/- key.

- Also, you should be able to use your mouse to resize the tmux panes as neede to get everything to look right.
  

- One last note:   tmux is similar to a virtual environment.  If you close Cool-Retro-Term, your session will still continue running in the background.    Before you close Cool-Retro-Term, I have added the tmux shortcut of CTRL-B X.    This will kill the session.   For clarity.  press CTRL-B, then let off and press capital X.   You will see a dialog in the bottom status bar confirming you want to kill the session.  say yes, then close Cool-Retro-Terminal

- If you prefer you can close Cool-Retro-Terminal then run this  in any terminal emulator
  
  - ```bash
    tmux kill-server
    ```

You know I've made mistakes in all of this.   Give me a shout with any questions.






