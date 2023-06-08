# notify-send-all
Send a pop-up notification message to all users logged into a machine. 
Similar to the 'wall' command, but for graphical logins (X & Wayland).
 
Messages are sent asynchronously, not blocking, but --action can still be used to wait for a response from each user. Responses are prefixed with the username and a TAB.

## Installation

It's just a shell script. Download [notify-send-all](https://raw.githubusercontent.com/hackerb9/notify-send-all/main/notify-send-all), make it executable, and put it in your path. 

<details>
 
 ```
 wget raw.githubusercontent.com/hackerb9/notify-send-all/main/notify-send-all
 chmod +x notify-send-all
 sudo mv notify-send-all /usr/local/bin/
 ```
</details>

## Requirements

Users must be logged in graphically (X or Wayland) with dbus and a notification daemon running. This program does not yet work for users logged in on the console.

## Usage

**notify-send-all** _[options]_ \<message> 
    
### Simple usage

    notify-send-all "My hovercraft is full of eels"

### More complex example

    notify-send-all --urgency=critical \\
                    --action=run="Run away!" \\
                    --action=hide="Hide!" \\
                    "Warning: Nuclear launch imminent"

#### Example output
    andy		run
    circus		hide
    hackerb9	run

 ## Bugs
 
* `-?`, `--help` only works correctly if it is the first argument.
  
* If a user is logged in on a console instead of a graphical session
  (X or Wayland), then `notify-send` hangs for a long time before
  timing out on StartServiceByName for org.freedesktop.Notifications. 
  This seems to be a bug in libnotify-1.8.1.

  This bug is also triggered when the user is logged in on both
  console and graphical sessions and logged into the console first.
  In that case, not only does notify-send hang, but notifications
  will not show up at all in the graphical session.

 
 ## Bonus command: notify-send-to
 
If you make a symlink called "notify-send-to", you can use it to send a pop up notification to a single user. 
