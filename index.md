Pi Desktopの設定メモ

#以下のファイルをダウンロード
https://github.com/pi-desktop/deb-make/releases/download/v1.1.0/pidesktop-base-1.1.0.zip

#解凍して以下のコマンドでインストール
sudo dpkg -i pidesktop-base-1.1.0.deb

以前に未選択のパッケージ pidesktop-base を選択しています。
(データベースを読み込んでいます ... 現在 81560 個のファイルとディレクトリがインストールされています。)
pidesktop-base-1.1.0.deb を展開する準備をしています ...
pidesktop-base (1.0.0) を展開しています...
pidesktop-base (1.0.0) を設定しています ...
Created symlink /etc/systemd/system/reboot.target.wants/embest-shutdown.service → /lib/systemd/system/embest-shutdown.service.
Created symlink /etc/systemd/system/poweroff.target.wants/embest-shutdown.service → /lib/systemd/system/embest-shutdown.service.
Created symlink /etc/systemd/system/multi-user.target.wants/embest.service → /lib/systemd/system/embest.service.
sudo systemctl disable fake-hwclock.service
Synchronizing state of fake-hwclock.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable fake-hwclock

#SD Card CopierでSDカードからSSDにシステムをコピーする

#以下のコマンドでマウントポイントを確認する
sudo lsblk

pi@raspberrypi:~ $ sudo lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda           8:0    0 223.6G  0 disk 
├─sda1        8:1    0   1.6G  0 part 
├─sda2        8:2    0     1K  0 part 
├─sda5        8:5    0    32M  0 part 
├─sda6        8:6    0    69M  0 part 
└─sda7        8:7    0 221.9G  0 part 
mmcblk0     179:0    0   7.6G  0 disk 
├─mmcblk0p1 179:1    0   1.6G  0 part 
├─mmcblk0p5 179:5    0    32M  0 part /media/pi/SETTINGS1
├─mmcblk0p6 179:6    0    69M  0 part /boot
└─mmcblk0p7 179:7    0   5.9G  0 part /

起動ドライブを変更する
vi /boot/cmdline.txt

変更前
dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=/dev/mmcblk0p7 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait splash plymouth.ignore-serial-consoles
変更後
dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=/dev/sda7 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait splash plymouth.ignore-serial-consoles
