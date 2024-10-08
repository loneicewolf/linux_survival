# linux_survival
A Survival Guide In Linux!


```
<details>
  <summary>Script _________ (Dark mode) - _________</summary>

</details>
```



<details>
  <summary>Problems And Solutions</summary>

Problem: 
Solution: 

- Problem: Slow system, etc.
  - Solution: `Add additional desktop environment(in this case LXDE) logout, and choose that, and login`

- Problem: tar.bz2 files, how to open?
  - Solution: `engrampa or xarchiver (engrampa worked)`

</details>

<details>
  <summary>Desktop Part</summary>

## Install different Desktop Environments
- ⚠️ Note!  sometimes it can error on different OS's, like `lxde` not found, try `lxde-desktop`, or similar
```sh

# install and re install
# in case of issues (Ubuntu Specific but good to know for other D.envs)
sudo apt install ubuntu-desktop
sudo apt-get install ubuntu-gnome-desktop 
sudo apt-get install --reinstall ubuntu-gnome-desktop 

# personal choie
sudo apt install lxde
sudo apt install lxde-desktop

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


<details>
  <summary>Screenshots</summary>

![image](https://github.com/user-attachments/assets/fcdc7d83-0864-43c0-8032-31acae35ce91)
![image](https://github.com/user-attachments/assets/697b9f9c-2bb1-462f-9826-8cb76b1f58b5)

</details>

<details>
  <summary>Script A (Light Mode)  - Desktop-Env Handling</summary>

```sh

#!/bin/bash

# Function to output the install command for the selected desktop environment
output_install_command() {
    local desktop_env="$1"
    echo "Command to install $desktop_env: sudo apt install -y $desktop_env"
}

# Create a list of desktop environments
desktop_envs=("KDE" "XFCE" "LXQt" "MATE" "Cinnamon")

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


<details>
  <summary>Script B (Dark mode) - Desktop-Env Handling</summary>



```sh
#!/bin/bash

# Function to output the install command for the selected desktop environment
output_install_command() {
    local desktop_env="$1"
    echo "Command to install $desktop_env: sudo apt install -y $desktop_env"
}

# Create a list of desktop environments
desktop_envs=("KDE" "XFCE" "LXQt" "MATE" "Cinnamon")

# Set the GTK theme to dark mode
export GTK_THEME="Adwaita:dark"

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













<details>
  <summary>Script C (Dark mode) - SSH Handling</summary>

```sh

#!/bin/bash

# Function to output the install command for the selected SSH option
output_command() {
    local action="$1"
    local service="$2"
    case "$action" in
        "install")
            echo "Command to install $service: sudo apt install -y $service"
            ;;
        "remove")
            echo "Command to remove $service: sudo apt remove -y $service"
            ;;
        "enable")
            echo "Command to enable $service: sudo systemctl enable $service"
            ;;
        "disable")
            echo "Command to disable $service: sudo systemctl disable $service"
            ;;
        *)
            echo "Invalid action."
            ;;
    esac
}

# Create a list of SSH options
ssh_services=("OpenSSH Client" "OpenSSH Server")

# Set the GTK theme to dark mode
export GTK_THEME="Adwaita:dark"

# Create a selection dialog for action
chosen_action=$(zenity --list \
    --title="Choose SSH Action" \
    --text="Select an action for SSH:" \
    --column="Actions" "install" "remove" "enable" "disable" \
    --height=300 --width=400)

# Check if the user made a selection
if [ -z "$chosen_action" ]; then
    zenity --error --text="No action selected. Exiting."
    exit 1
fi

# Create a selection dialog for SSH service
chosen_service=$(zenity --list \
    --title="Choose SSH Service" \
    --text="Select an SSH service:" \
    --column="SSH Services" "${ssh_services[@]}" \
    --height=300 --width=400)

# Check if the user made a selection
if [ -z "$chosen_service" ]; then
    zenity --error --text="No service selected. Exiting."
    exit 1
fi

# Map the selection to the corresponding package name
case "$chosen_service" in
    "OpenSSH Client")
        service="openssh-client"
        ;;
    "OpenSSH Server")
        service="openssh-server"
        ;;
    *)
        zenity --error --text="Invalid selection. Exiting."
        exit 1
        ;;
esac

# Output the command
output_command "$chosen_action" "$service" | zenity --info --text="$(output_command "$chosen_action" "$service")"


```

</details>













</details>

