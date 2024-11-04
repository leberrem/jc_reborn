# Install on Raspberry Pi

## Install SDL

```
sudo apt update
sudo apt upgrade -y
sudo apt install -y libsdl2-dev libsdl2-2.0-0
sudo apt install -y libjpeg-dev libwebp-dev libtiff5-dev libsdl2-image-dev libsdl2-image-2.0-0
sudo apt install -y libmikmod-dev libfishsound1-dev libsmpeg-dev liboggz2-dev libflac-dev libfluidsynth-dev libsdl2-mixer-dev libsdl2-mixer-2.0-0
sudo apt install -y libfreetype6-dev libsdl2-ttf-dev libsdl2-ttf-2.0-0
```

## Install Johnny Castaway

```
cd /home/pi
wget https://github.com/jno6809/jc_reborn/archive/refs/heads/master.zip -O jc_reborn.zip
unzip jc_reborn.zip
rm -f jc_reborn.zip
cd jc_reborn-master/
sudo apt install make gcc
make -f Makefile.linux

wget https://archive.org/download/johnny-castaway-screensaver/scrantic-run.zip
unzip scrantic-run.zip
rm -f scrantic-run.zip
```

```
cd /home/pi
wget https://github.com/nivs1978/Johnny-Castaway-Open-Source/archive/refs/heads/master.zip -O Johnny-Castaway-Open-Source.zip
unzip Johnny-Castaway-Open-Source.zip
rm -f Johnny-Castaway-Open-Source.zip
cp Johnny-Castaway-Open-Source-master/JCOS/Resources/*.wav ./jc_reborn-master/
rm -rf Johnny-Castaway-Open-Source-master
```

## Display resolution to 640x480

```
sudo vi /boot/config.txt
or
sudo vi /boot/firmware/config.txt
# -----------------
hdmi_group=2
hdmi_mode=4
# -----------------
```

## Create service on boot

```
sudo vi /lib/systemd/system/jc_reborn.service

# --------------
[Unit]
Description=Johnny Castaway reborn

[Service]
Environment=DISPLAY=:0
WorkingDirectory=/home/pi/jc_reborn-master
ExecStart=/home/pi/jc_reborn-master/jc_reborn > jc_reborn.out 2>&1
Restart=always
RestartSec=10s
KillMode=process
TimeoutSec=infinity

[Install]
WantedBy=multi-user.target
# --------------

sudo systemctl enable jc_reborn.service
```
