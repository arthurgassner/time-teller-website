# How to build it

## Introduction

The idea of having a sentence-based clock had been floating around in my head for a while.[^1] I eventually stumbled upon [this dataset](https://github.com/JohannesNE/literature-clock/blob/master/litclock_annotated.csv), and figured I'd build one.

Cue to some building.

[^1]: I assume I'd stumbled upon [one](https://literature-clock.jenevoldsen.com/) [of](https://www.authorclock.com/) [these](https://www.reddit.com/r/somethingimade/comments/xcbwpx/i_made_a_literary_quote_clock_out_of_an_old/) at some point.

## Step 1: Gather the necessary parts

First, I listed all things I'd expect to need -- naturally amending that list as I kept on building. Exhaustively:


| Part                                      | Description                                        | Price [CHF] |
| ----------------------------------------- | -------------------------------------------------- | ----------- |
| **Waveshare's 7.5inch e-Paper screen**    | Our screen                                         |     60      |       
| **Raspberry Pi Zero 2W**                  | To drive our screen.                               |     20      |       
| **Micro SD card**                         | To house the RPi's OS.                             |     10      |       
| **Waveshare's 7.5inch e-Paper HAT**       | To act as a bridge between our RPi and screen.     |     20      |       
| **USB cable Type C**                      | To power our RPi.                                  |     10      |       
| **3D-printed case**                       | To house everything.                               |     ~30     |       


<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>All required hardware.</figcaption>
</figure>

## Step 2: Setup the RPi

First, I needed to setup the freshly-opened RPI Zero 2W.
I flashed it -- thereby installing Raspberry Pi OS (64bit), based on Debian -- by following the [official guide](https://www.raspberrypi.com/software/).

!!! warning
    
    Make sure to flash your WiFi credentials and [SSH public key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) onto the board, allowing you to easily SSH into it later.

<figure markdown="span">
  ![Rpi Imager software](assets/how_to_build_it/rpi-imager.png){ width="100%" }
  <figcaption>Flashing the RaspberryPi Zero 2W.</figcaption>
</figure>

Once flashed and booted, the newly-installed RPi will automatically connect to my WiFi.
I can then figure out its local IP address with `sudo arp-scan --localnet`.

<figure markdown="span">
  ![arp-scan showing the local IPs](assets/how_to_build_it/arp-scan.gif){ width="100%" }
  <figcaption>Attempting to SSH into each local addresses, till I find the RPi.</figcaption>
</figure>

Once I'm in, the first thing to do is to update its software with `sudo apt update && sudo apt upgrade`. 

??? tip "Making the shell more pleasant"
    
    Whenever I install some Debian-based OS, I start by installing [`oh-my-zsh`](https://ohmyz.sh/) -- along with [`fzf`](https://github.com/junegunn/fzf), [`zsh-syntax-highlighting`](https://github.com/zsh-users/zsh-syntax-highlighting) and [`zsh-autosuggestions`](https://github.com/marlonrichert/zsh-autocomplete) -- making the entire shell-based interaction much more pleasant.

Then, since the code we'll write will be running directly on our RPi, it's preferable to write -- and test it -- directly on our headless board. Luckily, VSCode -- and most IDEs -- [supports this by default](https://code.visualstudio.com/docs/remote/remote-overview), allowing me to edit on my computer the files on our RPi.

## Step 3: Display something on the screen

I can now turn off the RPi, and hook the RPi to the HAT, and the HAT to the screen.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Raspberry Pi Zero 2W, connected to our HAT, and HAT to the e-Paper screen.</figcaption>
</figure>

Now e-ink technology is quite peculiar, in that it has a very high refresh time (~4s for our screen), and some several types of refresh, namely

- **Full-refresh**: The entire screen is refreshed at once, quite noticabely.
- **Partial-refresh**: Only a part of the screen is refreshed at once, discretely. The downside is that a part of the previous image is usually visible, leading to a "dirty-looking" screen after a while.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Side-by-side .gif of the full-refresh and partial-refresh.</figcaption>
</figure>

After diving through [Waveshare's demo codes](https://github.com/waveshareteam/e-Paper), and struggling to figure out what code was actually needed, I managed to display something onto the screen. The fully-fledged Python code is available [here](TODO).

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>A .gif of the e-ink screen displaying "something". The code is available [here](TODO/test_screen.py)</figcaption>
</figure>

Wonderful! I can now work my software magic and end up with a small Python script which fetches the time-accurate quote, builds a nice-looking image of it, and display it onto the screen. Using [`cron`](https://en.wikipedia.org/wiki/Cron), I can setup my RPi to run that script every minute, and _tada_! A clock!

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>A .gif of the e-ink screen changing minute.</figcaption>
</figure>

## Step 4: House the hardware properly

We now have a working clock -- yet fully naked on my desk.
I turn to a 3D modelling software -- [solvespace](https://solvespace.com), as I am a Linux user -- to draw what I'd see as a nice-looking housing.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Our 3D model, as seen in solvespace.</figcaption>
</figure>

Not owning a 3D printer myself, I order the parts to be 3D-printed in ABS, and 10 days later -- here they are.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Our 3D printed ABS shape, received by mail.</figcaption>
</figure>

threaded inserts

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Inserting threaded inserts</figcaption>
</figure>

usb C 

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Mounting the USB-C female port onto the housing.</figcaption>
</figure>

assemble 

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Fully-assembled literature clock.</figcaption>
</figure>
