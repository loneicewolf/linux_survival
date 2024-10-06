# linux_survival
A Survival Guide In Linux!


<details>
  <summary>Basic Part</summary>

</details>


<details>
  <summary>Desktop Part</summary>

## Install different Desktop Environments
- ⚠️ Note!  sometimes it can error on different OS's, like `gnome` not found, try `gnome-desktop`, or similar
```sh

# install and re install
# in case of issues (Ubuntu Specific but good to know for other D.envs)
sudo apt install ubuntu-desktop      # Installs Ubuntu desktop
sudo apt-get install ubuntu-gnome-desktop     # installs gnome in ubuntu
sudo apt-get install --reinstall ubuntu-gnome-desktop     # reinstalls gnome in ubuntu

# personal choie
sudo apt install lxde
sudo apt install lxde-desktop

# Gnome
sudo apt install gnome
sudo apt install gnome-desktop

# Mate
sudo apt install mate

# KDE/PLASMA
sudo apt install kde
sudo apt install plasma
sudo apt install plasma-kde
sudo apt install kde-plasma

```

## Further Readings
- https://stackexchange.com/search?q=separate+desktop+enviroments


</details>


<details>
  <summary>Scripting</summary>




# A script which uses Zenity for gui boxes
## it lets you choose the desktop environment to install then it outputs the command 

```sh

#F1() {
#    local A="$1"
#    echo "hello: $A..."
#    zenity --info --text="do something with $A"
#}




#!/bin/bash

# Function to output the install command for the selected desktop environment
output_install_command() {
    local desktop_env="$1"
    echo "Command to install $desktop_env: sudo apt install -y $desktop_env"
}

# Create a list of desktop environments
desktop_envs=("GNOME" "KDE" "XFCE" "LXQt" "MATE" "Cinnamon")

# Create a selection dialog
chosen_env=$(zenity --list \
    --title="Choose Desktop Environment" \
    --text="Select a desktop environment to install:" \
    --column="Desktop Environments" "${desktop_envs[@]}" \
    --height=300 --width=400)

# Check if the user made a selection
if [ -z "$chosen_env" ]; then
    zenity --error --text="No selection made. Exiting."
    exit 1
fi

# Map the selection to the corresponding package name
case "$chosen_env" in
    "GNOME")
        pkg="ubuntu-desktop"
        ;;
    "KDE")
        pkg="kubuntu-desktop"
        ;;
    "XFCE")
        pkg="xubuntu-desktop"
        ;;
    "LXQt")
        pkg="lxqt"
        ;;
    "MATE")
        pkg="ubuntu-mate-desktop"
        ;;
    "Cinnamon")
        pkg="cinnamon"
        ;;
    *)
        zenity --error --text="Invalid selection. Exiting."
        exit 1
        ;;
esac

# Output the command
output_install_command "$pkg" | zenity --info --text="$(output_install_command "$pkg")"


```






</details>

