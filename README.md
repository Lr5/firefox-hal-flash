# Dockerfile for Firefox with HAL Flash player

Firefox with [HAL Flash](https://launchpad.net/~mjblenner/+archive/ubuntu/hal-flash), based on the same ideas as [docker-chrome-pulseaudio](https://github.com/jlund/docker-chrome-pulseaudio).

Firefox with HAL Flash allows viewing DRM-protected content on sites that use Flash Player's DRM functionality, such as HBO Nordic.

This has been tested on the following sites:

- https://fi.hbonordic.com/ (especially Game of Thrones)

## Technical details

The Docker container will start an internal DBUS service (required for HAL Flash) and an SSH server (required for easy host-independent video/audio access).

The host system needs to have a Pulseaudio server running, with network access enabled (see instructions later here, or in [docker-chrome-pulseaudio](https://github.com/jlund/docker-chrome-pulseaudio).

## Build instructions

1. Copy your ssh public key to src/id_rsa.pub

2. Run build.sh

## Host setup

To get sound working, you need to setup pulseaudio server like done in [docker-chrome-pulseaudio](https://github.com/jlund/docker-chrome-pulseaudio).

In short:

1. Install pulseaudio preferences:

        sudo apt-get install paprefs

2. Launch PulseAudio Preferences, go to the "Network Server" tab, and check the "Enable network access to local sound devices" checkbox

3. Restart PulseAudio

        sudo service pulseaudio restart

For more detailed instructions and solutions to possible problems, see [docker-chrome-pulseaudio](https://github.com/jlund/docker-chrome-pulseaudio).

## Usage

1. In one terminal, run ./start.sh to start the Docker container with the necessary services (to stop this later, use CTRL-c or equivalent).

2. In another terminal, start Firefox by running ./access.sh (you might want to edit the file to change the default web page)

3. When trying to view a video, you might need to allow flash player to run. Click the plugin button on the left of the address bar and ensure it is allowed to run. In some cases you might need to press "continue allowing" right after opening a video for the video to play.
