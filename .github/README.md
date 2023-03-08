# Dotfiles
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/m/DeathGabox/DotFiles/main?color=blueviolet&label=Commit&logo=github&logoColor=black&style=for-the-badge)


https://ohmyposh.dev/

## THANKSYOU
https://ohmyposh.dev/docs/installation/customize

## Obtener Winget
```
https://github.com/microsoft/winget-cli/releases
  Descargar .mixbundle
```

## Configuracion Previa
```
Set-ExecutionPolicy Unrestricted
winget install --id Microsoft.Powershell --source winget
winget install --id Microsoft.WindowsTerminal -e
```

---

## WINGET
```
winget install rclone 
winget install Mozilla.Firefox
winget install zyedidia.micro
```

## Install Winfetch (Test with Export-Alias)
```
Install-Script -Name pwshfetch-test-1
Set-Alias winfetch pwshfetch-test-1
```

---

## Install Oh-my-posh
```
winget install JanDeDobbeleer.OhMyPosh -s winget
notepad $PROFILE
  oh-my-posh --init --shell pwsh --config ~/AppData/Local/Programs/oh-my-posh/themes/jandedobbeleer.omp.json | Invoke-Expression
exit
```

## Descargar e Instalar Fuentes
```
https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Hack/Regular/complete/Hack%20Regular%20Nerd%20Font%20Complete%20Mono%20Windows%20Compatible.ttf
https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Hack/Regular/complete/Hack%20Regular%20Nerd%20Font%20Complete%20Windows%20Compatible.ttf
NOTE: Instalar para todos los usuarios y reiniciar la terminal
```

## Actualizar Paquetes
```
winget update
winget upgrade --all
```


---

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
