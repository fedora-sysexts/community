# 1password-gui

[1Password](https://1password.com/) password manager desktop application.

This sysext installs 1Password from the official tarball distribution, which supports both x86_64 and aarch64 architectures.

## How to use

1. Install the sysext
2. Create the `onepassword` group and set up browser integration:
   ```
   $ sudo systemd-sysusers /usr/lib/sysusers.d/1password.conf
   $ sudo systemd-tmpfiles --create /usr/lib/tmpfiles.d/1password.conf
   ```
3. Launch 1Password and install the browser extension from your browser's extension store
4. In 1Password, go to Settings → Browser and enable browser integration. This creates a native messaging config file that tells your browser how to communicate with 1Password.
5. Update the native messaging config to point to the correct binary location (see browser-specific instructions below)
6. Restart your browser

### Firefox

The native messaging config is located at `~/.mozilla/native-messaging-hosts/com.1password.1password.json`. Update it with:

```
$ sed -i 's|/usr/lib/1Password|/var/lib/1password|g' \
    ~/.mozilla/native-messaging-hosts/com.1password.1password.json
```

For other browsers, find the native messaging config (usually in `~/.config/<browser>/NativeMessagingHosts/`) and update the path similarly.

## Why the extra steps?

1Password's browser integration requires the `1Password-BrowserSupport` binary to run with the `onepassword` group (setgid). This is used to verify that the browser is communicating with the legitimate 1Password binary.

Since sysexts are read-only, we can't set file permissions directly on `/usr`. Instead:

- **sysusers.d** creates the `onepassword` group
- **tmpfiles.d** copies the binary to `/var/lib/1password/` with the correct setgid permissions on each boot

This means sysext updates are handled automatically - the binary is re-copied with correct permissions on every boot. The native messaging config only needs to be updated once.

## Compatibility

This sysext should be compatible with Fedora Atomic Desktops.
