Using zram on steamdeck does not increase gaming performance. But if you use steamdeck as a workstation, 16GB ram is not good enough. Using ZRAM greatly improve workstation performance.
```
sudo swapoff -a
sudo modprobe zram
sudo zramctl -fs 8192M
sudo mkswap /dev/zram0
sudo swapon /dev/zram0
swapon
```
