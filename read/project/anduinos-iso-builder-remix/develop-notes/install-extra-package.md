---
title: 安裝額外的「Package」
nav_order: 1030
has_children: false
parent: 開發紀錄
grand_parent: AnduinOS / ISO Builder / Remix
---


# 安裝額外的「Package」




## 主題

* [相關討論](#相關討論)
* [說明](#說明)




## 相關討論

* [#51 - [分享] 我順手慣用的「按鍵綁定」設定](https://github.com/Anduin2017/AnduinOS/discussions/51)




## 說明

開發一個新的模組「[src/mods/14-my-extra-1010-package-mod](https://github.com/samwhelp/anduinos-iso-builder-remix/tree/main/asset/template/src/mods/14-my-extra-1010-package-mod)」，

用來安裝額外我想要安裝的「Package」。


想要安裝的「Package List」，

可以放在「[src/mods/14-my-extra-1010-package-mod/asset/package/install](https://github.com/samwhelp/anduinos-iso-builder-remix/tree/main/asset/template/src/mods/14-my-extra-1010-package-mod/asset/package/install)」這個資料夾。

可以多個檔案，副檔名是「`.txt`」。

檔案的每一行，就是想要安裝的「`Package Name`」。

接受『`行開頭註解「#」`』。
