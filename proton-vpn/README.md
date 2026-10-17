# proton-vpn

Proton VPN GTK app and CLI from the official Proton VPN repositories.

See: <https://protonvpn.com/support/official-linux-vpn-fedora>

## How to use

- Install either this sysext or `proton-vpn-cli`, not both: they ship the same
  Python libraries and the CLI is already included here.
- NetworkManager's OpenVPN plugin (`NetworkManager-openvpn` and
  `NetworkManager-openvpn-gnome`) and a Secret Service provider (gnome-keyring
  is the one supported by Proton) are not included and must be part of the
  image. They are included in Fedora Silverblue.
- On GNOME, the tray icon needs `gnome-shell-extension-appindicator`.

## Split tunneling is not supported

Proton implements split tunneling in `proton-vpn-daemon` with eBPF programs
compiled at runtime by bcc. Shipping it would add the LLVM and Clang libraries
(most of the size of the sysext) and a root daemon, and it needs headers for the
running kernel and does not work on kernels locked down in `confidentiality`
mode. The daemon and its dependencies are thus removed from this sysext. The
rest of the app (connections, kill switch, etc.) does not depend on it.

## Compatibility

This sysext is only built for x86_64. It has been tested on Fedora Silverblue.
