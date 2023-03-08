# Dotfiles
![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/m/DeathGabox/DotFiles/main?color=blueviolet&label=Commit&logo=github&logoColor=black&style=for-the-badge)

## Obtener Winget

[Winget Github Release](https://github.com/microsoft/winget-cli/releases/latest)

---

## Descargar e Instalar Fuentes

[Nerd Fonts Github](https://github.com/ryanoasis/nerd-fonts/releases/latest)

NOTE: Preferir Fuente Hack e Instalar "Regular Windows Complete" y "Regular Mono Windows Complete"

---

## Configuracion Previa
```
Set-ExecutionPolicy Unrestricted
winget install --id Microsoft.VCRedist.2015+.x64
winget install --id Microsoft.Powershell --source winget
winget install --id Microsoft.WindowsTerminal -e
winget install rclone 
winget install Mozilla.Firefox
winget install zyedidia.micro
```

---

## Install Oh-my-posh
```
winget install JanDeDobbeleer.OhMyPosh -s winget
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
  Set-Alias winfetch pwshfetch-test-1
  oh-my-posh --init --shell pwsh --config ~/AppData/Local/Programs/oh-my-posh/themes/jandedobbeleer.omp.json | Invoke-Expression
```

## Install Winfetch (Test with Export-Alias)
```
Install-Script -Name pwshfetch-test-1
```

## Actualizar Paquetes
```
winget update
winget upgrade --all
```

---

https://ohmyposh.dev/docs/installation/windows
https://rclone.org/onedrive/

> NOTA 06-03-2023

Bueno, cualquier cosa sobre el funcionamiento de arch, queda la [documentacion oficial](https://wiki.archlinux.org/), cualquier transpaso hacia este repositorio haria quedar desfasado y ser una vulnerabilidad, por lo que hare una limpieza y redireccion a la wiki con todo lo que pueda :p
