
# Enable/Disable Touchpad in Arch Linux (Hyprland)

This guide explains how to create a simple toggle script and bind it to a keyboard shortcut or custom function key in the Hyprland Wayland environment on Arch Linux.

Prerequisites

- Arch Linux
- Hyprland Wayland Compositor
- `libnotify` (Optional, for desktop notifications):


```
sudo pacman -S libnotify

```

Use code with caution.

- `wev` (Optional, to identify keyboard key names):


```
sudo pacman -S wev

```

*Use code with caution.*

## Step 1: Identify Your Touchpad Device Name

You need to know the exact name of your touchpad to tell Hyprland which device to disable.

Open a terminal and run:

hyprctl devices

Use this code with caution.

Look for the `mice:` or `touchpad:` section and note the full name of your device. For example: `elan1300:00-04f3:3087-touchpad`.

## Step 2: Create a Toggle Script

Create a directory for your Hyprland scripts if one doesn't already exist, then create a new script:

    mkdir -p ~/.config/hypr/scripts
    nano ~/.config/hypr/scripts/toggle_touchpad.sh

*Use code with caution.*

Copy and paste the following code into the file, **making sure `DEVICE_NAME` matches the name you identified in Step 1**:

    #!/bin/bash
    
    # Replace with your actual device name from 'hyprctl devices'
    DEVICE_NAME="elan1300:00-04f3:3087-touchpad"
    STATE_FILE="/tmp/touchpad_state"
    
    if [ -f "$STATE_FILE" ]; then
    # If the state file exists, the touchpad is disabled. Enable it.
    hyprctl keyword "device[$DEVICE_NAME]:enabled" true
    rm "$STATE_FILE"
    notify-send "Touchpad Enabled"
    else
    # If the state file doesn't exist, the touchpad is enabled. Disable it.
    hyprctl keyword "device[$DEVICE_NAME]:enabled" false
    touch "$STATE_FILE"
    notify-send "Touchpad Disabled"
    fi

*Use code with caution.*

Save and exit the editor (`Ctrl+O`, `Enter`, `Ctrl+X` in nano).

## Step 3: Make the Script Executable

You must grant execute permissions to the script before it can run:

    chmod +x ~/.config/hypr/scripts/toggle_touchpad.sh

*Use the code with caution.*

You can test the script now by running it from the terminal:

    ~/.config/hypr/scripts/toggle_touchpad.sh

*Use the code with caution.*

## Step 4: Identify the Correct Keyboard Key Name (Optional/Important for Function Keys)

For laptop keyboards (especially ASUS), special function keys may require specific key names that differ from `F6`.

Use `wev` to find the correct key name:

    sudo pacman -S wev
    wev

*Use the code with caution.*

Press your physical touchpad function key (e.g., `Fn + F6`). Note the `sym:` that appears in the output (`F6` or `XF86TouchpadToggle` are the most common).

## Step 5: Link the Script to a Keyboard Shortcut

Edit your main Hyprland configuration file (usually `~/.config/hypr/hyprland.conf` or `~/.config/hypr/conf/custom.conf`):

    nano ~/.config/hypr/conf/custom.conf

*Use code with caution*.

Add a `bind` line using the key name you found in Step 4.

**Option A: Using `SUPER` + `F6`:**

conf

    # Bind Super + F6 to toggle the touchpad
    bind = SUPER + F6, exec, ~/.config/hypr/scripts/toggle_touchpad.sh

*Use code with caution.*

**Option B: Using a Single Function Key (recommended if `wev` returns a custom name):**

conf

    # Bind the specific function key (e.g., F6 or XF86TouchpadToggle) to the script
    bind =, F6, exec, ~/.config/hypr/scripts/toggle_touchpad.sh

*Use code with caution.*

Note: The first parameter after `bind =` is a modifier key (such as SUPER, ALT, CTRL, SHIFT). If you want the keys to work alone, leave them blank, like `bind=, F6, ...`.

## Step 6: Reload Hyprland

Save your configuration file and reload Hyprland to apply the changes:

    hyprctl reload

*Use code with caution.*

Now you can use your keyboard shortcuts to enable and disable the touchpad!
