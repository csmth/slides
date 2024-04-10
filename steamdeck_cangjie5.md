# Install cangjie3/ cangjie5 under fcitx5 in steamdeck

[中文版在此](#中文版)
Normally steamdeck only support software installation by flatpak. Steamdeck user can install software of ArchLinux OS but those software will be erased at system upgrade. But its default cangjie input method is unfriendly for Traditional Chinese users. It is much better to use cangjie3/ cangjie5 instead. But these two input methods are not readily available in steamdeck. This guide is to address how to install cangjie3/ cangjie5 under fcitx5 flatpak.

## Using unstable flatpak of offical fcitx5
- 
```
flatpak remote-add --user --if-not-exists fcitx5-unstable https://flatpak.fcitx-im.org/unstable-repo/fcitx5-unstable.flatpakrepo
```

- Verify the source of fcitx5 installed
```
flatpak list
flatpak info org.fcitx.Fcitx5
```

- Uninstall offical fcitx5, if the source is not ```fcitx5-unstable```
```
flatpak uninstall org.fcitx.Fcitx5
```


## Managing default flatpak and fcitx5 unstable flatpak

```
flatpak remotes
```


## Ignore Steamdeck upgrade message


# 中文版
# 如何在 Steamdeck 的 fcitx5 框架下安裝三代或五代倉頡輸入法 

