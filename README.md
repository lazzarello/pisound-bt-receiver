# RPi + Pisound as bluetooth audio receiver

This repository contains an Ansible playbook to configure a Raspberry Pi with a Pisound audio board into a Audiophile grade Bluetooth receiver.

What is Ansible? Ansible is a system used primarily by software engineers managing numerous amounts of network devices. It is used here as a sort of "installer" to bring a default Rasperry Pi into the state where you can pair a phone (or any other Bluetooth device) to it and playback sound to an amplifier and speakers. This was intended to replace the numerous forum posts and threads documenting various attempts to make this work.

## Getting Ansible...

boop!

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

## Installing Raspbian
 Use the graphical thing [screenshot of graphical thing] and select the 32 bit "Lite" OS. Customize with the GUI to enable SSH at boot.

## Connecting to the RPi

mDNS should pick up the default hostname, `raspberrypi.local`. If you cannot ping this name, refer to the remote connection documentation.

SSH to the pi and...

* Copy SSH public key for password-less auth.
  * `ssh-copy-id -i ~/.ssh/big_id_rsa.pub pi@raspberrypi.local`
* Confirm Ansible connectivity
  * `ansible -i hosts -m ping raspberrypi`

## Running the playbook

## Pairing a Bluetooth device

TODO:
  * Publish ansible playbook to make changes to default Raspbian
    * Run playbook on fresh Raspbian Light
  * disable password ssh
  * give host a new name
  * 3D print enclosure at noisebridge
