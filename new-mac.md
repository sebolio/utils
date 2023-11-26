## Super Instalador para macOS

Antes de empezar, desactivar password de `sudo`
```
sudo sed -i '' 's/) ALL/) NOPASSWD:ALL/' /etc/sudoers
```

### Iniciar instalador
```
bash <(curl -Ls instalador.seb.cl)
```

<img width="532" alt="image" src="https://user-images.githubusercontent.com/197329/285684289-819c8728-0e5e-40bd-8529-faa52c08bff5.png">

Script: https://gist.github.com/sebolio/8126c531c17e8b0da74e652c2e85ab1e

<details>
<summary></summary>

```
mkdir ~/.ssh
cp $HOME/Library/Mobile\ Documents/com~apple~CloudDocs/ssh/* ~/.ssh
chmod 600 ~/.ssh/*
```

```
git clone github:sebolio/enti.git
git clone github:sebolio/seb.cl.git
git clone -b master github:sebolio/fichero.git vetmaster
```
</details>
