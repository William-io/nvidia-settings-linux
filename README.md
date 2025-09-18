## Corrigindo Tearing Monitor HDMI & Monitor via USB-C/HDMI INTEL - _*Somente para maquina com nvidia_

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
Exec=bash -c "export INTEL_DEBUG=sync && if /usr/bin/xrandr | grep -q 'DP-1-1 connected'; then /usr/bin/xrandr --output DP-1-1 --pos 0x0; else /usr/bin/xrandr --output DP-1-1 --mode 1920x1080 --rate 74.97 --pos 0x0; fi && /usr/bin/xrandr --output HDMI-0 --mode 1920x1080 --rate 74.97 --pos 1080x447 --rotate normal && /usr/bin/nvidia-settings --assign CurrentMetaMode='HDMI-0: 1920x1080_75 +1080+447 { ForceCompositionPipeline=On, ForceFullCompositionPipeline=On }'"
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
### Mudanças
```
Como funciona a condição:
if /usr/bin/xrandr | grep -q 'DP-1-1 disconnected' - Verifica se o DP-1-1 está desconectado

Se desconectado:

Aplica --mode 1920x1080 --rate 74.97 --pos 0x0 para forçar a conexão
Se conectado:

Aplica apenas --pos 0x0 sem especificar modo/taxa
HDMI-0: Sempre configurado normalmente (não muda)

Vantagens:
Só força o modo específico quando o DP-1-1 estiver realmente desconectado
Preserva configurações automáticas quando o monitor já está funcionando
Evita conflitos de resolução desnecessários
Mais eficiente quando tudo está funcionando corretamente
Agora o sistema só aplicará a configuração forçada --mode 1920x1080 --rate 74.97 no DP-1-1 quando ele realmente precisar!
```

---
