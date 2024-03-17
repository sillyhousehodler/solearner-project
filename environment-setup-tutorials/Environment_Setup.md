# Environment setup on Microsoft Windows
## Setup VirtualBox
### Download and install
- Download xubuntu ISO image (version LTS 22.04) from [https://xubuntu.org/download/](https://xubuntu.org/download/)
- Download Oracle VirtualBox from [https://www.virtualbox.org/](https://www.virtualbox.org/) and install it.
- After VirtualBox installation finishes, open the VirtualBox Manager
- Click "New" to create VM
- In the name field, put in any name you want, e.g., xubuntu2204
- Change the destination folder location if you want
- Select the xubuntu ISO image you've just downloaded
- Check the *Skip Unattended Installation*. Next
- For Hardware, assign 2 - 4 Processors, assign 2GB to 4GB *Base Memory*. Leave *Enable EFI* unchecked. Next
- For Virtual Hard Disk, default 25GB harddisk space is fine. Next and Finish

### VirtualBox Settings
Now you will see your named VM on the left panel. Select it and click the yellow gear *Settings* button
- In General > Advanced. Change the Snapshot Folder if you want. It's where your snapshot image file is saved for your newly created VM
- In System, you can adjust your *Base Memory* in Motherboard tab and the number of *Proccessors* in Processor tab
- In Display, assign at least 32MB video memory

Click the OK button and then the green arrow Start button.
When GNU GRUB menu popup (in black screen), choose *Try or Install Xubuntu*

### xubuntu install & setup
- Choose *Install Xubuntu*
- Choose the right keyboard or leave it default. Continue
- Choose *Minimal installation*, uncheck all options. Continue
- In the installation type, choose *Erase disk and install Xubuntu*. Click Install Now, and then Continue
- Set your timezone. Continue
- Set *Your name" for display, *username* and *password* for login
- Choose *Require my password to log in* for safety practice. Continue

When installation finishes, click Restart. If the restarting process halts in black screen. Click *Machine* from the top menu of VirtualBox and choose *Reset*.

- After restarted, login to the system. Click *Devices* from the VirtualBox top menu and choose *Insert Guest Additions CD image...*. You will see an explorer window popup with the path ."/media/yourUsername/VBox_GAs_7.0.14"
- Open the command terminal, go to the path "/media/yourUsername/VBox_GAs_7.0.14".
- Run the following
```sh
sudo ./VBoxLinuxAdditions.run
```
- After installing the modules, restart the system.
---
## Installing programs
### nvm and node
- Install curl
```sh
sudo apt install curl
```
- Install nvm
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
>The command for the latest nvm installation can be found at [https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)

- Restart terminal session. To show all the avaiable node versions, run :
```sh
nvm ls-remote
```
- Choose to install the latest LTS version. e.g. v20.11.1
```sh
nvm install v20.11.1
```
>To verify the successful installation of node, run "node" to get into node shell. Use Control-D to quit the node shell.
### Install rust toolchain for running Solana program
- Find the following command at [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install). Run :
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
- Choose *1) Proceed with standard installation*
- Restart the terminal session, check the version of rustc and cargo :
```sh
rustc -V
```
```sh
cargo -V
```
### Install Git for version control
```sh
sudo apt install git
```
If the installation is successful, run *git* will show git help
### Install IDE : VS Code
- Download Debian / Ubuntu version from [https://code.visualstudio.com/download](https://code.visualstudio.com/download)
- Go to */Download* directory; there should be a file something like **code_1.87.2-1709912201_amd64.deb**
- Install vscode :
```sh
 sudo dpkg -i code_1.87.2-1709912201_amd64.deb
 ```
- After installation success, you should be able to run vscode in the system menu.
### System upgrade
- Update all available upgrades for the whole system
```sh
sudo apt update
```
- To see all available upgrades (optional, run if necessary)
```sh
apt list --upgradable
```
- To upgrade all
```sh
sudo apt upgrade
```
---
## Install CLI
Find the following command at [https://docs.solanalabs.com/cli/install](https://docs.solanalabs.com/cli/install) and run :
```sh
sh -c "$(curl -sSfL https://release.solana.com/v1.18.4/install)"
```
After installation, re-login to take effect
### Create / manage keypair and address
- Create new keypair / public address
```sh
solana-keygen new
```
- Check balance
```sh
solana balance
```
- Check address
```sh
solana address
```
- Check config
```sh
solana config get
```
- Set RPC to devnet
```sh
solana config set -u devnet
```
- Get airdrop on devnet
```sh
solana airdrop 1
```
- Create a new keypair with a destinated keypair file. Useful for creating the second keypair
```sh
solana-keygen new --outfile ~/.config/solana/any-name-you-want.json --no-passphrase
```
- Switching between keypair addresses
```sh
solana config set --keypair ~/.config/solana/any-existing-name.json
```
- Create vanity keypair. For example, create a keypair with a public address that starts with "peter":
```sh
solana-keygen grind --starts-with peter:1
```
