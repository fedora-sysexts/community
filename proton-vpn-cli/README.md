# proton-vpn-cli

Proton VPN CLI from the official Proton VPN repositories, without the GUI.

See: <https://protonvpn.com/support/official-linux-vpn-fedora>

## How to use

- Install either this sysext or `proton-vpn`, not both: the GUI sysext already
  includes the CLI.
- NetworkManager's OpenVPN plugin (`NetworkManager-openvpn` and
  `NetworkManager-openvpn-gnome`) and a Secret Service provider (gnome-keyring
  is the one supported by Proton) are not included and must be part of the
  image. They are included in Fedora Silverblue.

## Split tunneling is not supported

Proton implements split tunneling in `proton-vpn-daemon` with eBPF programs
compiled at runtime by bcc. Shipping it would add the LLVM and Clang libraries
(most of the size of the sysext) and a root daemon, and it needs headers for the
running kernel and does not work on kernels locked down in `confidentiality`
mode. The daemon and its dependencies are thus removed from this sysext.

## Compatibility

This sysext is only built for x86_64.
