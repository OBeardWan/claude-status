# Claude Status

A KDE/Linux system tray app that shows live Claude / Anthropic service health
as a scrolling two-row history bar drawn directly into the tray icon — no
dropdown needed to see recent uptime at a glance.

- **Top row**: overall `status.claude.com` indicator history
- **Bottom row**: the "Claude API (api.anthropic.com)" component specifically
- Polls the public Statuspage.io API every 60 seconds and persists history to
  disk so it survives restarts
- Dropdown menu still shows current status text, a manual refresh, and a link
  to the status page

This was built as a Linux/KDE equivalent to a macOS-only menu bar app of the
same idea, since no Linux port existed.

## Install (Arch / EndeavourOS / Manjaro)

Not yet on the AUR — build it from this repo's `PKGBUILD` directly:

```
git clone https://github.com/OBeardWan/claude-status.git
cd claude-status
makepkg -si
```

This installs the binary, a `.desktop` entry for your app launcher, and icons.

After installing, launch "Claude Status" from your application launcher once.
To have it start automatically on login, add it via your desktop's autostart
settings (on KDE Plasma: **System Settings → Autostart → Add → Application →
Claude Status**) — the package intentionally doesn't force autostart on you.

## Compatibility

- **KDE Plasma**: fully supported, X11 and Wayland.
- **XFCE**: supported out of the box (native tray icon support).
- **GNOME Shell**: GNOME removed the system tray by default. You'll need the
  [AppIndicator and KStatusNotifierItem Support](https://extensions.gnome.org/extension/615/appindicator-support/)
  extension installed first, or the icon simply won't appear.
- Depends on `libayatana-appindicator`, GTK3, and PyGObject — declared as
  package dependencies in `PKGBUILD` and pulled in automatically by `makepkg -si`.

## Manual install (other distros)

There's no distro-agnostic package yet. To run it manually:

1. Install system dependencies (package names vary by distro): Python 3,
   PyGObject (`python3-gi` / `python-gobject`), GTK3, `libayatana-appindicator3`
   (Debian/Ubuntu: `gir1.2-ayatanaappindicator3-0.1`), and `python3-cairo`.
2. Copy `bin/claude-status` somewhere on your `PATH` (e.g. `~/.local/bin/`)
   and `chmod +x` it.
3. Copy `data/claude-status.desktop` to `~/.local/share/applications/`.
4. Copy the icons from `data/icons/` to the matching
   `~/.local/share/icons/hicolor/<size>x<size>/apps/claude-status.png` paths.
5. Run `kbuildsycoca6` (KDE) or log out/in so your launcher picks up the new
   `.desktop` entry.

## Publishing checklist (maintainer notes)

Currently released via GitHub only (tagged releases + `PKGBUILD`), no AUR
submission planned for now. If that changes later:

1. Create an AUR account and register an SSH key with it.
2. Clone `ssh://aur@aur.archlinux.org/claude-status.git`, copy in `PKGBUILD`
   (AUR also wants a generated `.SRCINFO` via
   `makepkg --printsrcinfo > .SRCINFO`), commit, and push.

## License

MIT — see [LICENSE](LICENSE).
