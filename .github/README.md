# Dotfiles
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/m/DeathGabox/DotFiles/main?color=blueviolet&label=Commit&logo=github&logoColor=black&style=for-the-badge)


https://ohmyposh.dev/

## THANKSYOU
https://ohmyposh.dev/docs/installation/customize

## Obtener Winget
´´´
https://github.com/microsoft/winget-cli/releases
  Descargar .mixbundle
´´´

## Configuracion Previa
´´´
Set-ExecutionPolicy Unrestricted
winget install --id Microsoft.Powershell --source winget
winget upgrade
´´´

---

## WINGET
```
winget install rclone 
winget install Mozilla.Firefox
winget install --id Microsoft.WindowsTerminal -e
winget install zyedidia.micro
```

## Install Winfetch
´´´
Install-Script -Name pwshfetch-test-1
Set-Alias winfetch pwshfetch-test-1
´´´

---

> Descargar las fuentes de Hack nerd font
´´´
cd C:\Users\Alumno\Downloads
https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.2/Hack.zip
Expand-Archive -Path ".\Hack.zip"
´´´

---

## Install Oh-my-posh
´´´
winget install JanDeDobbeleer.OhMyPosh
notepad $PROFILE
  oh-my-posh --init --shell pwsh --config ~/AppData/Local/Programs/oh-my-posh/themes/jandedobbeleer.omp.json | Invoke-Expression
Refresh terminal
´´´


https://github.com/PowerShell/PSReadLine
https://github.com/AnderssonPeter/PowerType

https://ohmyposh.dev/docs/installation/windows
https://rclone.org/onedrive/


##### TEST



winget install JanDeDobbeleer.OhMyPosh -s winget
notepad $PROFILE
oh-my-posh --init --shell pwsh --config ~/AppData/Local/Programs/oh-my-posh/themes/jandedobbeleer.omp.json | Invoke-Expression
oh-my-posh font install



> NOTA 06-03-2023

Bueno, cualquier cosa sobre el funcionamiento de arch, queda la [documentacion oficial](https://wiki.archlinux.org/), cualquier transpaso hacia este repositorio haria quedar desfasado y ser una vulnerabilidad, por lo que hare una limpieza y redireccion a la wiki con todo lo que pueda :p
