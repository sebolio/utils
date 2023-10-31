$\color{green}\textsf{\large \&#129438; Configuración fácil de nuevo PC}$ 

![sho600](https://user-images.githubusercontent.com/197329/234124658-535eade7-84a6-43d4-a333-7ca90109d092.png)

### 1. Abrir `PowerShell` como administrador
* Tecla <kbd>⊞</kbd>, escribir `PW` y presionar <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Enter</kbd>

### 2. Instalar **WSL2**
```
wsl --install
```

Mientras se instala, abrir otro PowerShell de admin y continuar:

### 3. Utilidades Windows
<details>
<summary>¿Qué es esto?</summary>

**Son 4 archivos que se copiarán en tu $HOME (C:\Users\\...)**

| Archivo | Descripción |
|-|-|
| [choko.bat](https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/bd3eea8019b3803c59ce5415d92e88d0f56fb474/choko.bat) | Permite ejecutar `choko <programa>` para instalar programa desde Chocolatey, el cual pedirá permisos de administración
| [shoko.bat](https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/bd3eea8019b3803c59ce5415d92e88d0f56fb474/shoko.bat)| Permite hacer búsquedas de programas con `shoko <texto>`
| [.wslconfig](https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/bd3eea8019b3803c59ce5415d92e88d0f56fb474/wslconfig) | Configura WSL para usar máximo 8gb de RAM
| [utils.reg](https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/68db49965ad854f9992c79bba7460deebbbef86e/utils.reg) | Modifica el registro de windows para: <br>👉 Mostrar opción "Administrador de tareas" en click secundario de barra inferior <br>👉 Activar los menús clasicos al hacer clic derecho<br>👉 Hace que la tecla `Impr. Pant` seleccione un área de la pantalla<br>👉 Desactiva la barra de acoplamiento que aparece al arrastrar ventanas<br>👉 Cambia región a Chile<br>👉 Cambia teclado a "Español (España)"<br>👉 Configura gestos de 3 dedos en el Touchpad, para cambiar y cerrar pestañas
</details>

```bat
Invoke-WebRequest -Uri "https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/bd3eea8019b3803c59ce5415d92e88d0f56fb474/choko.bat" -OutFile "$HOME\choko.bat"
Invoke-WebRequest -Uri "https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/bd3eea8019b3803c59ce5415d92e88d0f56fb474/shoko.bat" -OutFile "$HOME\shoko.bat"
Invoke-WebRequest -Uri "https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/bd3eea8019b3803c59ce5415d92e88d0f56fb474/wslconfig" -OutFile "$HOME\.wslconfig"
Invoke-WebRequest -Uri "https://gist.githubusercontent.com/sebolio/b38f7ef6db673fd32b5f5366f0d97e86/raw/68db49965ad854f9992c79bba7460deebbbef86e/utils.reg" -OutFile "$HOME\seb-utils.reg"
reg import $HOME\seb-utils.reg
```

### 4. Instalar Chocolatey
```bat
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

### 5. Instalar mis programas favoritos:
```bat
choco install -y --force --allow -empty-checksums --ignore-checksum googlechrome evernote notion authy-desktop winrar vscode slack auto-dark-mode telegram tableplus docker-desktop treesizefree steam spotify
```

### 6. Instalar fuentes (🖱️)
1. [Descargar aquí](https://1drv.ms/u/s!An9eKsg-lFZRsJIzweujNblNSrMUQg?e=3K7l8C) (no descomprimir)
2. Ejecutar esto para instalar:
```
Expand-Archive -Path "$HOME\Downloads\Fuentes Terminal.zip" -DestinationPath $ENV:TEMP\Fuentes
$SourceFolder = "$HOME\AppData\Local\Temp\Fuentes"
Add-Type -AssemblyName System.Drawing
$WindowsFonts = [System.Drawing.Text.PrivateFontCollection]::new()
Get-ChildItem -Path $SourceFolder -Include *.ttf, *.otf -Recurse -File |
Copy-Item -Destination "$env:SystemRoot\Fonts" -Force -Confirm:$false -PassThru |
ForEach-Object {
$WindowsFonts.AddFontFile($_.fullname)
$RegistryValue = @{
Path = 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Fonts'
Name = $WindowsFonts.Families[-1].Name
Value = $_.Fullname
}
$RemoveRegistry = "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Fonts"
Remove-ItemProperty -name $($WindowsFonts.Families[-1].Name) -path $RemoveRegistry
New-ItemProperty @RegistryValue
}

```

<table><tr><td> $\color{red}\textsf{\Large Ahora reinicia tu PC}$ </td></tr></table>

$\color{red}\textsf{Ubuntu se instalará automáticamente al reiniciar}$


```powershell
shutdown /r /t 0 /f
```

---

### 7. Configurar Terminal
* Abrir [Windows Terminal ➡️](http://r.seb.cl/powershell) y seguir instrucciones para dejarlo como predeterminado
* Elegir Ubuntu 🐧 como default, guardar y abrir una nueva pestaña del terminal

### 8. Habilitar sudo sin password
```
sudo sed -i 's/) ALL/) NOPASSWD:ALL/' /etc/sudoers
```

### 9. Instalar Zsh, Node y configuraciones
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
function gg { git clone git@github.com:sebolio/$1 }
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

### 10. Instalaciones por click

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
