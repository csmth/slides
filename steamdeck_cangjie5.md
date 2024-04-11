# Install cangjie3/ cangjie5 under fcitx5 in steamdeck

Normally Steamdeck only support software installation by flatpak. Steamdeck user can install software of ArchLinux OS but those software will be erased at system upgrade. Moreover default cangjie input method of steamdeck fcitx5 is unfriendly for Traditional Chinese users. It is much better to use cangjie3/ cangjie5 instead. But these two input methods are not readily available in steamdeck. This guide is to address how to install cangjie3/ cangjie5 under fcitx5 flatpak. 一般情況 Steamdeck 只支援以 Flatpak 安裝軟件。使用者有方法安裝 ArchLinux 的軟件，但這些軟件都在每次系統更新後被移除。而它的預設倉頡輸入法不便利正體中文使用者，使用三代倉頡或五代倉頡有更好效果。可是這兩個輪入法並不是立即能用，本篇目的旨在安裝三代倉頡或五代倉頡輸入法。

## Using unstable flatpak of offical fcitx5 repository
- ```TableExtra``` addon package is hosted under ```fcitx5-unstable``` flatpak repository. Add this repository to your steamdeck. You need TableExtra addon to configure Fcitx5 with cangjie3/ cangjie5. 你需要在增加軟件庫 ```fcitx5-unstable``` 於你的 Steamdeck 下，它的附加軟件 ```TableExtra``` 是三代倉頡或五代倉頡所需。
```
flatpak remote-add --user --if-not-exists fcitx5-unstable https://flatpak.fcitx-im.org/unstable-repo/fcitx5-unstable.flatpakrepo
```

- Verify the repositories being recognized. Note that your steamdeck has at least ```flatpak``` by default. 確定你的系統認可的軟件庫。你的 Steamdeck 在出廠時最少已認可 ```flatpak``` 軟件庫。
```
flatpak remotes
```

- List the software package being installed and verify their repository (origin). *Widen your terminal to 120 characters width* to display more information about your packages. 列出你的軟件和他們的來源軟件庫 (origin)。把終端顯示擴闊至 120 字元以方便看到更多軟件資料。
```
flatpak list
flatpak info org.fcitx.Fcitx5
flatpak info org.fcitx.Fcitx5.Addon.ChineseAddons
```

- Uninstall offical fcitx5 if their origin are not ```fcitx5-unstable```. Skip this step if fcitx5 is not installed. 如果你已經安裝了 Fcitx5 而來源並不是```fcitx5-unstable```，移除它們。
```
flatpak uninstall org.fcitx.Fcitx5
flatpak uninstall org.fcitx.Fcitx5.Addon.ChineseAddons
```

- Install these three packages from the same flatpak origin: ```fcitx5-unstable```. 這三個軟件應來自同一軟件庫： ```fcitx5-unstable``` 以確保沒有阻力。
```
flatpak install fcitx5-unstable org.fcitx.Fcitx5
flatpak install fcitx5-unstable org.fcitx.Fcitx5.Addon.ChineseAddons
flatpak install fcitx5-unstable org.fcitx.Fcitx5.Addon.TableExtra
```

- You need to logout and re-logon and configure your Fcitx5 software again. After re-login, cangjie3/ cangjie5 are available for configuration. The new input methods are put under zh-HK (香港) or zh-TW (台灣) locales, which are different from other Chinese Addons with zh-CN (中国) locales. 你需要登出戶口再登入，之後就可以在 Fcitx5 軟件下找到三代倉頡和五代倉頡。新輸人法在香港和台灣的 locale 下，與其他中文輸入法的中国 locale 並不同類。
![Alt](fcitx5_table_extra.jpg)

## Steamdeck update failure message
You may be asked to update the Fcitx5, but the update fails. 你會被要求更新 Fcitx5 軟件，然後更新失敗。
![Alt](steamdeck_fcitx5_update_fail.jpg)

- This failure message is irritating. You can fix this by: 這項更新失敗訊息可能令人困擾，你可以這麼解決：
```
flatpak update
```
- This command may ask you to update other flatpak components (in my case that is ```org.kde.Platform/x86_64``` that matches the error message above). Accept this so that fcitx5 can be updated. After this Steamdeck update process will resume normally. 這項指令可能要求你更新其它 Flatpak 元件 (我的情況是更新 ```org.kde.Platform/x86_64``` 合乎上圖訊息)，接受它，這樣 fcitx5 就可以更新了。之後 Steamdeck 軟件更新程序會回復正常。

## But I wish to pick other input methods
- Repository ```fcitx5-unstable``` provides other addons that support different input methods, and you do not need to pick cangjie3/ cangjie5. This is the command to list the addons: 軟件庫```fcitx5-unstable```提供其他附加附件支援不同的輸入法，提供有別於倉頡三代和五代的選擇：
```
flatpak remote-ls fcitx5-unstable 
```
- Below are the list of choices as of early April-2024 以下是 2024 年四月所見的選項： (My comment is vague because I don't use them 我的註解含糊因為我完全沒使用它們)

| Package Name                            | My Comment                                                                                                            |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| org.fcitx.Fcitx5                        | Primary software, not addon 主體軟件，不是附加元件                                                                       |
| org.fcitx.Fcitx5.Addon.Anthy            | Japanese IME 日語輸入法引擎 https://en.wikipedia.org/wiki/Anthy                                                         |
| org.fcitx.Fcitx5.Addon.Bamboo           | Vietnamese IME 越南語輸入法引擎                                                                                         |
| org.fcitx.Fcitx5.Addon.Chewing          | Chewing=酷音/新酷音                                                                                                    |
| org.fcitx.Fcitx5.Addon.ChineseAddons    | Addons for Simplified Chinese, not for Traditional Chinese 給中囯人使用，並非以正體中文為目標                              |
| org.fcitx.Fcitx5.Addon.Cskk             | Japanese IME 日語輸入法引擎                                                                                             |
| org.fcitx.Fcitx5.Addon.Hangul           | Korean IME 韓語輸入法引擎                                                                                               |
| org.fcitx.Fcitx5.Addon.Jyutping         | Jyutping=粵拼                                                                                                         |
| org.fcitx.Fcitx5.Addon.Kkc              | Japanese IME 日語輸入法引擎                                                                                             |
| org.fcitx.Fcitx5.Addon.LibThai          | Thai language related 泰語相關 https://github.com/tlwg/libthai                                                         |
| org.fcitx.Fcitx5.Addon.Lua              | Lua UI addon, not extra input method. For example OpenWRT uses Lua. Lua 不是輸入法是外掛元件，例如 OpenWRT 使用 Lua UI     |                                                                                    |
| org.fcitx.Fcitx5.Addon.Mozc             | Japanese IME 日語輸入法引擎                                                                                             |
| org.fcitx.Fcitx5.Addon.Rime             | Rime=中州韻輸入法引擎，如支援嘸蝦米                                                                                       |
| org.fcitx.Fcitx5.Addon.Sayura           | Sinhala IME 僧咖羅語輸入法引擎                                                                                          |
| org.fcitx.Fcitx5.Addon.Skk              | Japanese IME 日語輸入法引擎                                                                                             |
| org.fcitx.Fcitx5.Addon.TableExtra       | You need this for cangjie3/ cangjie5 用倉三倉五快三快五就需要此元件                                                       |
| org.fcitx.Fcitx5.Addon.TableOther       | IME to support different lanaguages not supported otherelse 支援其他語言                                               |
| org.fcitx.Fcitx5.Addon.Unikey           | Vietnamese IME 越南語輸入法引擎                                                                                        |
| org.fcitx.Fcitx5.Addon.Zhuyin           | Zhuyin/Bopomofo=注音引擎                                                                                             |


## Why cangjie3/ cangjie5 is preferred over default cangjie?
The choice of input method is only a matter of taste. However there is some inconvenience to use default cangjie input method under fcitx5 for Traditional Chinese users. Fcitx5 consider some words are identical, like 台 / 臺，and 体 / 體. Default cangjie input method always returns 臺 on cangjie code of 台 (IR 戈口), and returns 體 on cangjie code of 体 (ODM 人木一). Cangjie input method only relies on glyphs, this makes automatic conversion painful when using Cangjie. There is no such conversion in cangjie3/ cangjie5. 

選擇使用什麼輸入法只是口味問題。可是，在 Fcitx5 框架下的預設倉頡輸入法對正體中文使用者帶來不便。它視一些字為相同，例如「台」「臺」和「体」「體」。預設倉頡輸入法在收到「台」的輸入碼（戈口）後輸出「臺」，收到「体」的輸入碼（戈口）後輸出「體」。因為倉頡輸入法的取碼只考慮字形，自動轉換在用倉頡輸入法時痛苦。而三代倉頡和五代倉頡都沒有字形自動轉換的情況。

## Reference
- Official Fcitx5 installation Guide 官網安裝指引 https://fcitx-im.org/wiki/Install_Fcitx_5
- Another method by installing fcitx5 under ArchLinux software 安裝 ArchLinux 的 fcitx5 軟件的另一方法 https://forum.gamer.com.tw/C.php?bsn=60599&snA=40156


