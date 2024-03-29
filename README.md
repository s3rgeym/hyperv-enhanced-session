# README

AUR package that provides Enhanced Session Mode support for the Hyper-V virtual machine. Based on [linux-vm-tools](https://github.com/microsoft/linux-vm-tools/).

![image](https://github.com/s3rgeym/hyperv-enhanced-session/assets/12753171/afba61f6-be08-4bf9-bc1e-bf08ca81bab8)

## Installation

```bash
# install
yay -S hyperv-enhanced-session

# enable session
sudo systemctl enable --now hyperv-enhanced-session

# xrdp reads .xinitrc
echo "/usr/lib/plasma-dbus-run-session-if-needed startplasma-x11" > ~/.xinitrc
chmod +x ~/.xinitrc

# restart xrdp if service already started
sudo systemctl daemon-reload
sudo systemctl restart xrdp
```

## Hyper-V Settings

```ps
Set-VMhost -EnableEnhancedSessionMode $True
Set-VM -VMName <NameVM> -EnhancedSessionTransportType HvSocket
```

## Links

* [Arch Wiki: Xrdp]( https://wiki.archlinux.org/title/xrdp)
* [Setup Hyper-V enhanced session for Ubuntu 20](https://gist.github.com/milnak/54e662f88fa47a5d3a317edb712f957e)
