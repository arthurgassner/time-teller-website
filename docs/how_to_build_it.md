# How to build it

## Introduction

The idea of having a sentence-based clock had been floating around in my head for a while.[^1]

[^1]: I assume I'd stumbled upon [one](https://literature-clock.jenevoldsen.com/) [of](https://www.authorclock.com/) [these](https://www.reddit.com/r/somethingimade/comments/xcbwpx/i_made_a_literary_quote_clock_out_of_an_old/) at some point.

Eventually, I stumbled upon [this dataset](https://github.com/JohannesNE/literature-clock/blob/master/litclock_annotated.csv), and figured I'd build one.

Cue to some building.

## Step 1: Gather the necessary parts

First, I listed all things I'd expect to need -- naturally amending that list as I kept on building. Exhaustively:
- **Waveshare's 7.5inch e-Paper screen**: Our screen.
- **Raspberry Pi Zero 2W**: To drive our screen.
- **Micro SD card**: To house the RPi's OS.
- **Waveshare's 7.5inch e-Paper HAT**: To act as a bridge between our RPi and screen.
- **USB cable Type C**: To power our RPi.
- **A 3D-printed case**: To house everything.

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
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Flashing the RaspberryPi Zero 2W.</figcaption>
</figure>

??? tip "Making the shell more pleasant"
    
    Whenever I install some Debian-based OS, I start by installing [`oh-my-zsh`](https://ohmyz.sh/) -- along with [`fzf`](https://github.com/junegunn/fzf), [`zsh-syntax-highlighting`](https://github.com/zsh-users/zsh-syntax-highlighting) and [`zsh-autocomplete`](https://github.com/marlonrichert/zsh-autocomplete) -- making the entire shell-based interaction much more pleasant.

Once flashed and booted, the newly-installed RPi will automatically connect to my WiFi.
I can then figure out its local IP address with `sudo arp-scan --localnet`.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Attempting to SSH into each local addresses, till I find the RPi.</figcaption>
</figure>

## Step 3: Display something on the screen

I can now turn off the screen, and the RPi to the HAT, and HAT to the screen.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Raspberry Pi Zero 2W, connected to our HAT, and HAT to the e-Paper screen.</figcaption>
</figure>

paper screens have partial refresh and full-refresh, explain it
Python script printing the quote on the screen, using cron.

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>The quote actualizing.</figcaption>
</figure>

## Step 4: House the hardware properly

solvespace to build some housing

<figure markdown="span">
  ![Image title](https://placehold.co/600x400){ width="100%" }
  <figcaption>Our 3D model, as seen in solvespace.</figcaption>
</figure>

print-as-a-service, ABS

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
