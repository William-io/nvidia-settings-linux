# nvidia-settings-linux

# Corrigindo Tearing no HDMI com NVIDIA

## Passo a Passo Manual

### 1. Criar a pasta necessária

Antes de abrir o nano, você precisa criar a pasta. Só rodar:

```bash
mkdir -p ~/.config/autostart
```

Esse `-p` garante que tanto o `~/.config` quanto o `autostart` existam.

### 2. Criar o arquivo de configuração

Depois disso, o comando vai funcionar:

```bash
nano ~/.config/autostart/nvidia-hdmi-fix.desktop
```

### 3. Adicionar o conteúdo

Agora sim você cola o conteúdo:

```ini
[Desktop Entry]
Type=Application
Exec=nvidia-settings --assign CurrentMetaMode="HDMI-0: nvidia-auto-select { ForceFullCompositionPipeline = On }"
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name=Fix HDMI Tearing
Comment=Active ForceFullCompositionPipeline on HDMI-0
```

### 4. Salvar e dar permissão

Salva (`Ctrl+O`, Enter, `Ctrl+X`) e dá permissão de execução:

```bash
chmod +x ~/.config/autostart/nvidia-hdmi-fix.desktop
```

**Da próxima vez que você fizer login, vai rodar esse comando e aplicar a correção de tearing só no HDMI-0.**

---
