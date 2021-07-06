# Connect a Raspberry Pi to Eduroam at the University of Cambridge.

This guide based on that published by Robert Bricheno at https://github.com/rbricheno/eduroam-ucam-raspberry, albeit updated and modified.

1. Connect the RPi to a personal hotspot to directly copy and paste the commands and to download the wireless certificate.
2. Download the University of Cambridge certificate here: https://help.uis.cam.ac.uk/system/files/documents/wireless-ca.crt.
3. Use the following commands to move it from the RPi Downloads directly into the wpa_supplicant folder:

    '''
    cd /
    sudo mv ~/Downloads/wireless-ca.crt /etc/wpa_supplicant
    '''
