* `sudo tzselect`

Please identify a location so that time zone rules can be set correctly.
Please select a continent or ocean.
#? 9) Pacific Ocean
Please select a country.
#? 26) United States
Please select one of the following time zone regions.
#? 21) Pacific

The following information has been given:
        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
Local time is now:      Wed Jun 15 13:11:13 PDT 2016.
Universal Time is now:  Wed Jun 15 20:11:13 UTC 2016.
Is the above information OK?
#? 1) Yes

Make the time zone permanent through the bashrc
* `vim .bashrc`
 * Append this line to the file
  * TZ='America/Los_Angeles'; export TZ
 * Save and quit the file
 * Exit the terminal and open a new terminal

* `sudo systemctl restart rsyslog`
* `sudo timedatectl status`
* `sudo rpm -qa | grep tzdata`
