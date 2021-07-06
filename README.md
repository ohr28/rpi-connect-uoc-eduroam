# Connect a Raspberry Pi to Eduroam at the University of Cambridge.

This guide based on that published by Robert Bricheno at https://github.com/rbricheno/eduroam-ucam-raspberry, albeit updated and modified.

1. Connect the RPi to a personal hotspot to directly copy and paste the commands and to download the wireless certificate.
2. Download the University of Cambridge wireless certificate here: https://help.uis.cam.ac.uk/system/files/documents/wireless-ca.crt.
3. Go to https://tokens.uis.cam.ac.uk/person/ohr22 and create a new eduroam token, noting down the ```CRSid+name``` and your ```tokenspassword`
5. Use the following commands to move it from the RPi Downloads directly into the wpa_supplicant folder:
    
    ```
    cd /
    sudo mv ~/Downloads/wireless-ca.crt /etc/wpa_supplicant
    ```
5. Now enter the wpa_supplicant.conf file:
 
    ```
    cd etc/wpa_supplicant
    sudo nano wpa_supplicant.conf
    ```
    
6. Add scroll down to the bottom of the file and, replacing ```CRSid+name``` and ```tokenspassword``` with your information, add:

    ```
    network={
        ssid="eduroam"
        proto=RSN
        key_mgmt=WPA-EAP
        eap=PEAP
        pairwise=CCMP
        group=CCMP
        identity="CRSid+name@cam.ac.uk"
        anonymous_identity="_token@cam.ac.uk"
        password="tokenspassword"
        ca_cert="/etc/wpa_supplicant/wireless-ca.crt"
        subject_match="/C=GB/ST=England/L=Cambridge/O=University of Cambridge/OU=University Information Services/CN=token.wireless.cam.ac.uk"
    }
    ```
    
7. Press Ctrl+O and then Enter to save changes, then Ctrl-X to exit the nano editor.
8. Close the terminal window, open a new one and then enter the 10-wpa_supplicant file with the following commands:
 
    ```
    cd /
    sudo nano lib/dhcpcd/dhcpcd-hooks/10-wpa_supplicant
    ```
    
9. Scroll down to around line 58, and edit the line ```wpa_supplicant_driver="${wpa_supplicant_driver:-nl80211,wext}"``` to  ```wpa_supplicant_driver="${wpa_supplicant_driver:-wext,nl80211}"``` , ensuring that the minus sign stays with the colon!
10. Save and exit the file with Cntrl-O, Enter and then Cntl-X, as before.
11. Reboot the RPi, and check the files above if necessary to ensure the correct changes have been saved. If they have been correctly changed, then the RPi should automatically connect to eduroam, although it remains greyout in the menu.
  
   
    
