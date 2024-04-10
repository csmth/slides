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


## Why cangjie3/ cangjie5 is preferred over default cangjie?
The choice of input method is only a matter of taste. However there is some inconvenience to use default cangjie input method under fcitx5 for Traditional Chinese users. Fcitx5 consider some words are identical, like 台 / 臺，and 体 / 體. Default cangjie input method always returns 臺 on cangjie code of 台 (IR 戈口), and returns 體 on cangjie code of 体 (ODM 人木一). Cangjie input method only relies on glyphs, this makes automatic conversion painful when using Cangjie. There is no such conversion in cangjie3/ cangjie5. 

選擇使用什麼輸入法只是口味問題。可是，在 Fcitx5 框架下的預設倉頡輸入法對正體中文使用者帶來不便。它視一些字視為相同，例如「台」「臺」和「体」「體」。預設倉頡輸入法在收到「台」的輸入碼（戈口）後輸出「臺」，收到「体」的輸入碼（戈口）後輸出「體」。因為倉頡輸入法的取碼只考慮字符，自動轉換令使用倉頡輸入法時痛苦。而 Fcitx5 框架下的三代倉頡和五代倉頡都沒有自動轉換的情況。



