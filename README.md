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

`ansible-playbook -i hosts --check --diff playbook.yaml`

## Pairing a Bluetooth device

The pairing process seems to happen in reverse, in that the RPi needs to pair to the phone, which presents a PIN on both endpoints. Tap on the phone PIN dialog and type "yes" into the shell to pair. My phone (Google Pixel 4a) disconnected after a few seconds. Clicking the `raspberrypi` device on my phone paired persistently. Not sure how to fix this bug...

```
bluetoothctl
discoverable on
scan on
```
Find the MAC address of the device you want to pair mine is below
```
pair 88:54:1F:4D:4E:81
trust 88:54:1F:4D:4E:81
```

There is another bluetooth bug where sometimes the phone disconnects and pairing does not work from the phone. connecting from the RPi succeeds. Annnnd, it seems that the device disconnects without an interactive session. Booo. This is a downgrade from the desktop distribution. Perhaps because DBus isn't installed? IDK.

TODO:
  * tune [resample method in pulse](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Audiophile/) (trivial method has audio dropouts)
  * put bluetooth into discoverable mode by default
  * improve the bluetooth pairing procedure
  * give host a new name
  * 3D print enclosure at noisebridge
