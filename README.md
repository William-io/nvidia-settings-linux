# Corrigindo Tearing no HDMI & Monitor via USB-C/HDMI - _*Somente para maquina com nvidia_

### 1. Criar a pasta necessária

Antes de abrir o nano, você precisa criar a pasta. Só rodar:

```bash
mkdir -p ~/.config/autostart
```

Esse `-p` garante que tanto o `~/.config` quanto o `autostart` existam.

### 2. Criar o arquivo de configuração

```bash
nano ~/.config/autostart/fix-monitors.desktop
```

### 3. Adicionar o conteúdo

```ini
[Desktop Entry]
Type=Application
Exec=bash -c "/usr/bin/xrandr --output DP-1-1 --pos 0x0 && /usr/bin/xrandr --output HDMI-0 --mode 1920x1080 --pos 1080x447 --rotate normal && /usr/bin/nvidia-settings --assign CurrentMetaMode='HDMI-0: nvidia-auto-select +1080+447 { ForceCompositionPipeline=On, ForceFullCompositionPipeline=On }'"
Hidden=false
X-GNOME-Autostart-enabled=true
Name=Fix Monitors Layout
Comment=Repositions DP-1-1 and applies ForceFullPipeline to HDMI-0
```

### 4. Salvar e dar permissão

Salva (`Ctrl+O`, Enter, `Ctrl+X`) e certifique-se que o arquivo é legível:

```bash
chmod 644 ~/.config/autostart/fix-monitors.desktop
```

---
