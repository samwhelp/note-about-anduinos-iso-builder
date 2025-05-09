---
title: build-interrupt-on-creating-efi-boot-image
nav_order: 1010
has_children: false
parent: 開發紀錄
grand_parent: 如何
---


# build-interrupt-on-creating-efi-boot-image




## 主題

* [相關討論](#相關討論)
* [狀況描述](#狀況描述)




## 相關討論

* [回覆： #51 - [分享] 我順手慣用的「按鍵綁定」設定](https://github.com/Anduin2017/AnduinOS/discussions/51#discussioncomment-13042053)




## 狀況描述

在製作「AnduinOS Live ISO」時，會中斷在某一處，

出現下面的訊息

```
Installing for i386-pc platform.
grub-install: error: install device isn't specified.
```

我找到在「[build.sh](https://github.com/Anduin2017/AnduinOS/blob/1.3/src/build.sh#L260)」，其中程式碼如下，應該是中斷在這

``` sh
sudo grub-install --efi-directory=efi --uefi-secure-boot --removable --no-nvram
```

後來我參考我之前[紀錄的文章](https://samwhelp.github.io/note-about-grub/read/howto/boot-iso/create-live-usb-disk-for-uefi.html#%E7%94%A2%E7%94%9Fefibootbootx64efi)，做了修改如下

``` sh
    pushd $SCRIPT_DIR/image
    print_ok "Creating EFI boot image on /isolinux/efiboot.img..."
    (
        cd isolinux && \
        #dd if=/dev/zero of=efiboot.img bs=1M count=10 && \
        #sudo mkfs.vfat efiboot.img && \
        #mkdir efi && \
        #sudo mount efiboot.img efi && \
        #sudo grub-install --efi-directory=efi --uefi-secure-boot --removable --no-nvram && \
        #sudo umount efi && \
        #rm -rf efi
        sudo grub-mkimage \
            --format="x86_64-efi" \
            --output="./efiboot.img" \
            --directory="/usr/lib/grub/x86_64-efi" \
            --prefix="/EFI" \
                fat \
                iso9660 \
                part_gpt \
                part_msdos \
                normal \
                boot \
                linux \
                linux16 \
                configfile \
                loopback \
                chain \
                efifwsetup \
                efi_gop \
                efi_uga \
                ls \
                search \
                search_label \
                search_fs_uuid \
                search_fs_file \
                gfxterm \
                gfxterm_background \
                gfxterm_menu \
                test \
                all_video \
                loadenv \
                exfat \
                ext2 \
                ntfs \
                btrfs \
                hfsplus \
                udf \
                cat

    )
    judge "Create EFI boot image"
```

就可以製作成功「AnduinOS Live ISO」，

不過我是使用「傳統的BIOS」順利開機，

所以我沒有測試「UEFI」開機，

所以我也不確定這樣修改是否符合原本預期的，

因為關於這部份，我並不懂，只是依樣畫葫蘆，還沒研究透徹，所以先暫時紀錄發現到的狀況。
