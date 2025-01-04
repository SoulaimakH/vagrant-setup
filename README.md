# Vagrant Setup

This repository contains Vagrantfiles to provision virtual machines. The environment is designed to work on Windows 11 using VirtualBox, Vagrant, and WSL (Windows Subsystem for Linux).

## Environment Setup

**Operating System:** Windows 11  
**Virtualization:** VirtualBox  
**Automation Tool:** Vagrant  
**WSL (Windows Subsystem for Linux):** Used to run Linux-based commands in Windows

### Prerequisites

Before running Vagrant, ensure that the following are installed:
- VirtualBox
- Vagrant
- WSL (Windows Subsystem for Linux) with Ubuntu (or any preferred distribution)

## Best Practices

It is recommended to run `vagrant up` directly from Windows, rather than from WSL, to avoid potential conflicts.

**Example:**  
![Shared Folder Error Fix](https://github.com/user-attachments/assets/6b0dbee7-ac6c-4a3c-8cb8-a85127ba676d)

## Common Issues and Solutions

### 1. Network Configuration

To avoid network conflicts, use the same name for the existing DHCP server. 

Example:  
- Set up the network to match the DHCP range.
  
  ```config.vm.network "private_network", type: "dhcp", virtualbox__intnet: "Host-Only" # Host network ```
  

  File > Tools > Network Manager :
  
![Network Configuration](https://github.com/user-attachments/assets/89badb61-c11f-4169-bc5c-38f66d95e012)



### 2. Shared Folder Path Error

You may encounter the following error when configuring your machine:

```
The host path of the shared folder is not supported from WSL. Host path of the shared folder must be located on a file system with DrvFs type. Host path: .
```

**Solution:**  
To fix this, either:
- Disable the synced folder with the following command in your Vagrantfile:

    ```ruby
    config.vm.synced_folder '.', '/vagrant', disabled: true
    ```

- Alternatively, mount the VM into a Windows directory (e.g., `/mnt/c = c:/`):

    ```ruby
    config.vm.synced_folder '/mnt/c/pr', '/vagrant'
    ```



### 2. Enabling Windows Access in WSL

To ensure proper file access between Windows and WSL, add the following environment variable:

```bash
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
```



