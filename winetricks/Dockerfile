FROM achernetsov/wine

RUN sudo wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks \
&& sudo chmod +x winetricks \
&& sudo mv ./winetricks /usr/local/bin/winetricks

RUN sudo apt-get install -y cabextract

#init win32 prefix using
#WINEPREFIX="$HOME/prefix32" WINEARCH=win32 wine wineboot

#run winetricks for prefix:
#WINEPREFIX="$HOME/prefix32" WINEARCH=win32 winetricks --help

#run some app:
#WINEPREFIX="$HOME/prefix32" WINEARCH=win32 wine app.exe


