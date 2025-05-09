---
title: 放置額外的「File」到「Live System (new_building_os)」
nav_order: 1030
has_children: false
parent: 開發紀錄
grand_parent: AnduinOS / ISO Builder / Remix
---


# 放置額外的「File」到「Live System (new_building_os)」




## 主題

* [相關討論](#相關討論)
* [說明](#說明)




## 相關討論

* [#51 - [分享] 我順手慣用的「按鍵綁定」設定](https://github.com/Anduin2017/AnduinOS/discussions/51)




## 說明

開發一個新的模組「[src/mods/14-my-extra-1020-overlay-mod](https://github.com/samwhelp/anduinos-iso-builder-remix/tree/main/asset/template/src/mods/14-my-extra-1020-overlay-mod)」，用來安裝額外我想要安裝的「Package」。


想要放置的「File」可以放在「[src/mods/14-my-extra-1020-overlay-mod/asset/overlay](https://github.com/samwhelp/anduinos-iso-builder-remix/tree/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay)」這個資料夾。

模組是在「`chroot`」下執行的。

這個資料夾會對應到「Live System」的「/」，

也就是對應到建製過程中的「src/new_building_os」這個資料夾。
