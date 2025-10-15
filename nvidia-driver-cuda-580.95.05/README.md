# nvidia-driver-cuda

This provides the NVIDIA CUDA driver and userspace tools.

## Prerequisites

To successfully use this sysext, you **must** have the **NVIDIA kernel modules** installed on your host *before* proceeding with the installation.
These modules provide the core functionality required for the NVIDIA CUDA driver to operate.

## How to use

- Install the sysext
- Create the `nvidia-persistenced` user:
  ```
  $ sudo systemd-sysusers /usr/lib/sysusers.d/nvidia-persistenced.conf
  ```

## Compatibility

This sysext is compatible with all Fedora variants (CoreOS, Atomic Desktops,
etc.) but has only been tested on CoreOS.
