# xremap-tools

A Bash script for managing custom key bindings on Linux systems. Unlike **xremap**, which requires the terminal to stay open, this script allows your key remappings to run in the background, ensuring they remain active even after closing the terminal.

Easily specify your keyboard device in the script for quick setup. To find your keyboard's name, refer to [How to Locate Your Keyboard](#how-to-locate-your-keyboard) for guidance.

> **Note:** This script was made for personal use but is shared for anyone who may find it helpful.


## Install xremap

Download a binary from [Releases](https://github.com/k0kubun/xremap/releases).

If it doesn't work, please [install Rust](https://doc.rust-lang.org/cargo/getting-started/installation.html)
and run one of the following commands:

```bash
cargo install xremap --features x11     # X11
cargo install xremap --features gnome   # GNOME Wayland
cargo install xremap --features kde     # KDE-Plasma Wayland
cargo install xremap --features wlroots # Sway, Hyprland, etc.
cargo install xremap                    # Others
```

You may also need to install `libx11-dev` to run the `xremap` binary for X11.

### Arch Linux

If you are on Arch Linux and X11, you can install [xremap-x11-bin](https://aur.archlinux.org/packages/xremap-x11-bin/) from AUR.

### NixOS

If you are using NixOS, xremap can be installed and configured through a [flake](https://github.com/xremap/nix-flake/).

## Configure xremap

To configure **xremap**, first create the configuration directory if it doesn't already exist:

```bash
mkdir -p ~/.config/xremap
```
- If the directory exists, simply add your configuration file:
```bash
touch ~/.config/xremap/config.yml
```

For more information on configuring xremap, visit the official [xremap GitHub repository](https://github.com/xremap/xremap). You can also find my configuration file in the config folder of this repository.


## How to Locate Your Keyboard

To find the event number for your keyboard, run the following command in your terminal:

```bash
cat /proc/bus/input/devices
```

Look for the section that contains your keyboard's name. Here’s an example output:

```
I: Bus=0003 Vendor=260d Product=0009 Version=0110
N: Name="HOLTEK A87 Gaming Keyboard"
P: Phys=usb-0000:09:00.3-2/input0
S: Sysfs=/devices/pci0000:00/0000:00:08.1/0000:09:00.3/usb3/3-2/3-2:1.0/0003:260D:0009.0005/input/input13
U: Uniq=
H: Handlers=sysrq kbd leds event13 
B: PROP=0
B: EV=120013
B: KEY=1000000000007 ff9f207ac14057ff febeffdfffefffff fffffffffffffffe
B: MSC=10
```

In this example, the event number for the keyboard is event13. All you need to do is copy the name of your keyboard (e.g., HOLTEK A87 Gaming Keyboard) and put it in the script. For the next steps, refer to [Installation for xremap-tool](#installation-for-xremap-tool)


## Installation for xremap-tool

To use this script, follow these steps:

1. **Clone the Repository**: Download the repository to your local machine.
   ```bash
   git clone https://github.com/fr0st-iwnl/xremap-tools.git
   cd xremap-tools
   ```

2. **Edit the script**: Open the script file and enter the name of your keyboard.
   ```bash
   vim ~/path/to/toggle_xremap.sh 
   ```
    - Replace **DEVICE_NAME=**`"HOLTEK A87 Gaming Keyboard"` with the actual name of your keyboard.

3. **Make the Script Executable**: Change the permissions of the script to make it executable.
   ```bash
   chmod +x toggle_xremap.sh
   ```

## Usage

1. **Run the Script**: Execute the script with the required parameters.
   ```bash
   ./toggle_xremap.sh
   ```

## Custom Command Setup (Optional)

If you'd like to run the script from anywhere, follow these steps to create a custom command:

1. **Create the `bin` Directory**  
   Create a folder called `bin` in `~/.local/share/`. If it already exists, simply add the script there and rename it to a simple command name (e.g., `xremap`).

   ```bash
   mkdir -p ~/.local/share/bin
   cp /path/to/toggle_xremap.sh ~/.local/share/bin/xremap
   ```

2. **Update Your Shell Configuration**:  
   Add the following line to your `~/.bashrc` or `~/.zshrc`:

   ```bash
   export PATH="$HOME/.local/share/bin:$PATH"
   ```

3. **Reload Your Terminal**:  
   Apply the changes by running:

   ```bash
   source ~/.bashrc
   ```

   or

   ```bash
   source ~/.zshrc
   ```

## TO DO

- [ ] **User Input for Device Name**: Prompt users to enter their input device name when they start the script. Log this information to a file for easy reference. Users can find their device name by running `cat /proc/bus/input/devices`.

- [ ] **Known Issue**: If users frequently unplug and replug their keyboard or use different USB ports, the script may not function correctly. This is a known issue that needs to be addressed.

