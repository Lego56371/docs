# Casaos Installation Guide

### Installation

1. We need a fresh linux vm.

2. We need to ssh into the vm

3. We need to update our packages
```bash
sudo apt update
```

And the upgrade to install
```bash
sudo apt upgrade -y
```

4. Now all we need to do is run the istall script
```bash
curl -fsSL https://get.casaos.io | sudo bash
```