## Corrigindo Tearing Monitor HDMI & Monitor INTEL - _*Somente para maquina com nvidia_

### 1. Primeiro, vamos criar um script shell separado:

```bash
mkdir -p ~/.local/bin
nano ~/.local/bin/fix-monitors.sh
# Cole o conteúdo do script & 
chmod +x ~/.local/bin/fix-monitors.sh
```
>Trecho que precisar ser copiado para o fix-monitors.sh
```bach
#!/bin/bash

if /usr/bin/xrandr | grep -q 'DP-1-1 connected'; then
    /usr/bin/xrandr --output DP-1-1 --pos 0x0
else
    /usr/bin/xrandr --output DP-1-1 --mode 1920x1080 --rate 74.97 --pos 0x0
fi

/usr/bin/xrandr --output HDMI-0 --mode 1920x1080 --rate 74.97 --pos 1080x447 --rotate normal
/usr/bin/nvidia-settings --assign CurrentMetaMode='HDMI-0: 1920x1080_75 +1080+447 { ForceCompositionPipeline=On, ForceFullCompositionPipeline=On }'
```

### 2. Agora, vamos criar o arquivo .desktop:

```bash
mkdir -p ~/.config/autostart
nano ~/.config/autostart/fix-monitors.desktop
# Cole o conteúdo do arquivo .desktop
```

>Adicionar o conteúdo ao fix-monitors.desktop

```ini
[Desktop Entry]
Type=Application
Name=Fix Monitors
Exec=/home/user/.local/bin/fix-monitors.sh
Terminal=false
X-GNOME-Autostart-enabled=true
```
>Você também pode adicionar um pequeno delay no arquivo .desktop para garantir que o X server esteja completamente iniciado:
>"sleep 2 && /home/user/.local/bin/fix-monitors.sh"

### 4. Salvar utilizando nano

Salva (`Ctrl+O`, Enter, `Ctrl+X`) 

### Objetivo
```
1. Verifica se o monitor DP-1-1 está conectado
2. Se estiver conectado, apenas define sua posição (--pos 0x0)
3. Se não estiver conectado, configura modo, taxa de atualização e posição
4. Configura o monitor HDMI-0
5. Aplica configurações NVIDIA para evitar screen tearing
```
---
