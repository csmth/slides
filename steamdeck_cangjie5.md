# Install cangjie3/ cangjie5 under fcitx5 in steamdeck

Normally steamdeck only support software installation by flatpak. Steamdeck user can install software of ArchLinux OS but those software will be erased at system upgrade. But its default cangjie input method is unfriendly for Traditional Chinese users. It is much better to use cangjie3/ cangjie5 instead. But these two input methods are not readily available in steamdeck. This guide is to address how to install cangjie3/ cangjie5 under fcitx5 flatpak.

## Using unstable flatpak of offical fcitx5
- ```TableExtra``` software package is hosted under ```fcitx5-unstable``` repository. Register this repository to your steamdeck.
```
flatpak remote-add --user --if-not-exists fcitx5-unstable https://flatpak.fcitx-im.org/unstable-repo/fcitx5-unstable.flatpakrepo
```

- Verify the repositories being recognized. Note that your steamdeck has at least ```flatpak``` recognised.
```
flatpak remotes
```

- List the software package being installed and verify their repository (origin). *Widen your terminal to 120 characters width* to display more information about your packages.
```
flatpak list
flatpak info org.fcitx.Fcitx5
flatpak info org.fcitx.Fcitx5.Addon.ChineseAddons
```

- Uninstall offical fcitx5, if the source is not ```fcitx5-unstable```. Skip this step if fcitx5 is not installed
```
flatpak uninstall org.fcitx.Fcitx5
flatpak uninstall org.fcitx.Fcitx5.Addon.ChineseAddons
```

- These three packages MUST comes from the same flatpak source. When you install TableExtra from fcitx5-unstable, other fcitx5 packages must comes from fcitx5-unstable as well.
```
flatpak install fcitx5-unstable org.fcitx.Fcitx5
flatpak install fcitx5-unstable org.fcitx.Fcitx5.Addon.ChineseAddons
flatpak install fcitx5-unstable org.fcitx.Fcitx5.Addon.TableExtra
```

## Ignore Steamdeck upgrade message



