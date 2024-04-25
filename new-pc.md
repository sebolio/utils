$\color{green}\textsf{\large \&#129438; Configuración fácil de nuevo PC}$ 

### Configurar Terminal
* Abrir [Windows Terminal ➡️](http://r.seb.cl/powershell) y seguir instrucciones para dejarlo como predeterminado
* Elegir Ubuntu 🐧 como default, guardar y abrir una nueva pestaña del terminal

### Habilitar sudo sin password
```
sudo sed -i 's/) ALL/) NOPASSWD:ALL/' /etc/sudoers
```

### Instalar Zsh, Node y configuraciones
```
sudo apt install zsh -y
```
```
curl https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/3d2d9802708bb276a5360dd8356bc1bebea2074a/z-p10k.zsh -o .p10k.zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
$\color{blue}\textsf{Presionar "enter" antes de seguir}$ 

Luego pegar esto para implementar `nvm`, fuente, `p10k` y `alias`.
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
. $HOME/.nvm/nvm.sh
nvm install --lts
WINDIR=`cmd.exe /c echo %systemdrive%%homepath% 2> /dev/null | tr -d '\r' | xargs -0 wslpath`           
sed -i 's/robbyrussell/powerlevel10k\/powerlevel10k/' .zshrc
sed -i '1s/^/source "${XDG_CACHE_HOME:-$HOME\/.cache}\/p10k-instant-prompt-${(%):-%n}.zsh"\n/' .zshrc
sed -i 's/"name": "Ubuntu",/"name": "Ubuntu", "font": { "face": "CaskaydiaCove Nerd Font", "size": 10 },/' $WINDIR/AppData/Local/Packages/Microsoft.WindowsTerminal_8wekyb3d8bbwe/LocalState/settings.json
echo "
#alias y comandos
unalias gp
unalias gg
function gp { git add -A; git commit -m \"\$*\"; git push }
function gg { git clone git@github.com:sebolio/\$1 }
alias dev=\"([ -f bun.lockb ] && echo bun && bun run dev) || ([ -f pnpm-lock.yaml ] && echo pnpm && pnpm run dev) || npm run dev\"
alias doc=\"npm run storybook\"
alias json=\"npm run stub\"
alias stub=\"npm run stub\"
alias pu=\"git pull\"
alias p=\"ping nic.cl\"
\n[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh">>~/.zshrc
pnpm setup
sudo apt update;sudo apt install -y openjdk-11-jre
```
Ignorar mensajes de error

### 
Instalaciones por click

* **[Adobe CC](https://creativecloud.adobe.com/en/apps/download/creative-cloud) [▶️](https://creativecloud.adobe.com/en/apps/download/creative-cloud)** 🖱️
* **[Morgen](https://www.morgen.so/download) [▶️](https://www.morgen.so/download)** 🖱️

* **[WhatsApp](http://r.seb.cl/whatsapp) [▶️](http://r.seb.cl/whatsapp)**
* **[Overwatch](http://r.seb.cl/ow) [▶️](http://r.seb.cl/ow)**
* **[Actualizar Terminal](http://r.seb.cl/terminal) [▶️](http://r.seb.cl/terminal)**
* **[TransulcentTB](http://r.seb.cl/translucenttb) [▶️](http://r.seb.cl/translucenttb)**
* **[QuickLook](http://r.seb.cl/quicklook) [▶️](http://r.seb.cl/quicklook)**
* **[Wallpaper Engine](http://r.seb.cl/wallpaperengine) [▶️](http://r.seb.cl/wallpaperengine)**

![](https://raw.githubusercontent.com/javascript-obfuscator/javascript-obfuscator/master/images/logo.png)

<details>
<summary></summary>
Añadir llaves

```
mkdir ~/.ssh 2>/dev/null
WINDIR=`cmd.exe /c echo %systemdrive%%homepath% 2> /dev/null | tr -d '\r' | xargs -0 wslpath`
while [ ! -f ~/.ssh/config ]; do
  cmd.exe /c explorer.exe /select,%userprofile%\\onedrive\\.ssh 2>/dev/null
  PowerShell.exe -Command "Add-Type -AssemblyName PresentationFramework;[System.Windows.MessageBox]::Show(\"Para configurar reposotorios:\`n‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾\`n\`n-> Haz clic derecho en [.ssh]\`n-> Elige [Mantener siempre en este dispositivo]\`n\`nAcepta cuando termine de descargar.\",'', 'OK', 'Info', 'OK', [System.Windows.MessageBoxOptions]::DefaultDesktopOnly)"
  cp $WINDIR/OneDrive/.ssh/* ~/.ssh
  chmod 600 ~/.ssh/*
done
```

Clonar
```
git clone git@github.com:sebolio/enti.git
git clone git@github.com:sebolio/seb.cl.git
git clone -b main git@github.com:sebolio/fichero.git fichero
git clone -b master git@github.com:sebolio/fichero.git vetmaster
```
</details>
