grubの起動画面で `c` を押してコマンドラインに入る
```
grub> set root=(hd0,msdos3)
grub> linux /vmlinuz
grub> initrd /initrd.gz
grub> boot
```
