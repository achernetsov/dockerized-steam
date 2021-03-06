# overview
docker + wine for running windows apps (or games) on linux and keeping host system clean.

only nvidia and alsa implemented, but you feel free to contribute and add amd, pulseaudio, etc., following design rules;

steam-os will not be supported, only windows steam; recommended way to install steamos is using flatpak;

# nvidia prerequisites
need to install nvidia-docker: https://github.com/NVIDIA/nvidia-docker/wiki/Installation
need to run for nvidia-docker-plugin for nvidia images to work:
```
sudo nvidia-docker-plugin
# now can run container
cd winetricks
./run.sh
```

# example of running windows steam
1. clone this repo to use run.sh script: ```git clone https://github.com/achernetsov/dockerized-steam && cd dockerized-steam```
2. create directory to persist /home/wine between container sessions: ```mkdir wine-home```
3. run nvidia-docker-plugin: ```sudo nvidia-docker-plugin```
4. run achernetsov/winetricks: ```cd winetricks && ./run.sh```; after this command you will be inside container shell: ```wine@myhost:~$```
5. init wine prefix, for example: ```WINEPREFIX="$HOME/win32" WINEARCH=win32 wine wineboot```
6. download steam installator: wget https://steamcdn-a.akamaihd.net/client/installer/SteamSetup.exe
7. install steam: ```WINEPREFIX="$HOME/win32" WINEARCH=win32 wine SteamSetup.exe```
8. run steam ```WINEPREFIX="$HOME/win32" WINEARCH=win32 wine [path to steam.exe inside win32]```

you could create wine prefix for specific setup and use shared Steam folder. read wine documentation: https://www.winehq.org/

# design rules for Dockerfiles:
1. fine-grained with single responsibility for simple debugging, updating and interchanging
2. testable: 
to avoid running steam, install game, to only find that sound doesn't work, 
every image should have simple test. for example, alsa have playsound.sh to check that sound works.

# improvements
1. search for todo's in code
2. maybe need to refactor images hierarchy, it should be decided when amd or pulsaudio will be added

# resources
nvidia driver: https://github.com/NVIDIA/nvidia-docker/wiki/NVIDIA-driver

glxgears "X11 no protocol found" error fix: https://unix.stackexchange.com/a/118826

ms fonts: https://askubuntu.com/questions/86335/installing-other-fonts-on-wine
