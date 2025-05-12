---
title: 安裝「variety」
nav_order: 1050
has_children: false
parent: 開發紀錄
grand_parent: AnduinOS / ISO Builder / Remix
---


# 安裝「variety」




## 主題

* [相關討論](#相關討論)
* [狀況說明](#狀況說明)
* [解法](#解法)
* [相關設定檔](#相關設定檔)




## 相關討論

* [#51 - [分享] 我順手慣用的「按鍵綁定」設定](https://github.com/Anduin2017/AnduinOS/discussions/51)




## 狀況說明

透過新的模組「[src/mods/14-my-extra-1010-package-mod](https://github.com/samwhelp/anduinos-iso-builder-remix/tree/main/asset/template/src/mods/14-my-extra-1010-package-mod)」的[機制](https://samwhelp.github.io/note-about-anduinos-iso-builder/read/project/anduinos-iso-builder-remix/develop-notes/install-extra-package.html)去安裝的，

一開始測試的結果，發現「variety」沒有安裝在「Live ISO」裡，

但是其它我額外想安裝的「Package」確有安裝。

後來我實做了「Build and Log」的機制，

看到有其中類似如下的訊息。


```

Reading package lists...
Building dependency tree...
Reading state information...
Package 'imagemagick-7-doc' is not installed, so not removed
REMOVING:
  gir1.2-gexiv2-0.10*    liblqr-1-0*              python3-pil*
  gir1.2-notify-0.7*     libmagickcore-7.q16-10*  python3-soupsieve*
  imagemagick*           libmagickwand-7.q16-10*  variety*
  imagemagick-7-common*  python3-bs4*
  imagemagick-7.q16*     python3-lxml*

Summary:
  Upgrading: 0, Installing: 0, Removing: 13, Not Upgrading: 0
  Freed space: 22.1 MB

```

執行

``` sh
apt-cache show variety | grep '^Depends:'
```

顯示

```
Depends: gir1.2-gdkpixbuf-2.0, gir1.2-gexiv2-0.10, gir1.2-glib-2.0, gir1.2-gtk-3.0, gir1.2-notify-0.7, gir1.2-pango-1.0, imagemagick, python3-bs4, python3-lxml, python3-cairo, python3-configobj, python3-dbus, python3-gi, python3-gi-cairo, python3-packaging, python3-pil, python3-requests, python3:any
```

後來使用「`imagemagick`」當「關鍵字」找尋，

在「[src/mods/79-useless-package-remover/install.sh](https://github.com/Anduin2017/AnduinOS/blob/1.3/src/mods/79-useless-package-remover/install.sh#L31)」發現到其中有一行如下

```
    imagemagick*
```

綜合以上找到的線索，

因為「`variety`」這個「Package」依賴「`imagemagick`」這個「`imagemagick`」，

但是「`79-useless-package-remover`」這個模組會將「imagemagick」相關的「Package」移除，

一開始雖然透過「`14-my-extra-1010-package-mod`」這個模組安裝了「`variety`」，


但後來隨著移除「imagemagick」相關的「Package」，於是「`variety`」也跟著被移除了。




## 解法

複製一份「[src/mods/79-useless-package-remover/install.sh](https://github.com/Anduin2017/AnduinOS/blob/1.3/src/mods/79-useless-package-remover/install.sh#L31)」來修改，

將原本那行註解

```
    imagemagick*
```


[修改成](https://github.com/samwhelp/anduinos-iso-builder-remix/blob/main/asset/template/src/mods/79-useless-package-remover/install.sh#L31)如下

```
    #imagemagick*
```




## 相關設定檔

| 設定檔 |
| ----- |
| [~/.config/autostart](https://github.com/samwhelp/anduinos-iso-builder-remix/blob/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay/etc/skel/.config/autostart) |
| [~/.config/autostart/variety.desktop](https://github.com/samwhelp/anduinos-iso-builder-remix/blob/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay/etc/skel/.config/autostart/variety.desktop#L5) |


| 設定檔 |
| ----- |
| [~/.config/variety](https://github.com/samwhelp/anduinos-iso-builder-remix/tree/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay/etc/skel/.config/variety) |
| [~/.config/variety/.firstrun](https://github.com/samwhelp/anduinos-iso-builder-remix/blob/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay/etc/skel/.config/variety/.firstrun) |
| [~/.config/variety/history.txt](https://github.com/samwhelp/anduinos-iso-builder-remix/blob/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay/etc/skel/.config/variety/history.txt) |
| [~/.config/variety/variety.conf](https://github.com/samwhelp/anduinos-iso-builder-remix/blob/main/asset/template/src/mods/14-my-extra-1020-overlay-mod/asset/overlay/etc/skel/.config/variety/variety.conf) |
