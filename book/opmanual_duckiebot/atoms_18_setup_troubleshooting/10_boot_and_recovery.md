# Boot and recovery troubleshooting {#setup-troubleshooting-boot status=ready}

What to do if your Raspberry Pi does not boot, network is unreachable etc.

## The Raspberry Pi does not have power

Symptom: The red LED on the Raspberry Pi is OFF.

Resolution: Press the button on the side of the battery ([](#troubleshooting-battery-button)).

<figure id="troubleshooting-battery-button">
    <figcaption>The power button on the RAVPower Battery.</figcaption>
     <img src="battery_button.jpg" style='width: 14em'/>
</figure>


## The Raspberry Pi has power but it does not boot

Symptom: The Raspberry Pi has power but it does not boot.

Resolution: [Initialize the SD card](#setup-duckiebot) if not done already. Try again if done instead.

## Hanging {#troubleshooting-hanging}

Symptom: The Pi hangs when you do `docker pull` commands or otherwise and sometimes shuts off.

Resolution: An older version of the SD card image had the docker container `cjimti/iotwifi` running but this was found to be causing difficulties. `ssh` into your robot by some method and then execute:

    duckiebot $ docker rm $(docker stop $(docker ps -a -q --filter ancestor=cjimti/iotwifi --format="{{.ID}}"))
    duckiebot $ sudo systemctl unmask wpa_supplicant
    duckiebot $ sudo systemctl restart networking.service
