

# Resumo

Esta anotação reúne scripts Shell (.sh) para geração automática de relatórios de diagnóstico e manutenção preventiva em diferentes famílias Linux.

O objetivo é automatizar tarefas comuns realizadas por administradores de sistemas e profissionais de suporte.

Cada script foi adaptado para sua respectiva distribuição, aproveitando as ferramentas nativas de cada ecossistema.

---

# Distribuições Suportadas

- Debian
- Ubuntu
- Linux Mint
- Fedora
- Arch Linux
- openSUSE
- Alpine Linux

---

# Estrutura Recomendada

```text
Linux-Health-Check
│
├── Debian
│   └── revisao-debian.sh
│
├── Ubuntu
│   └── revisao-ubuntu.sh
│
├── Linux-Mint
│   └── revisao-mint.sh
│
├── Fedora
│   └── revisao-fedora.sh
│
├── Arch
│   └── revisao-arch.sh
│
├── openSUSE
│   └── revisao-opensuse.sh
│
└── Alpine
    └── revisao-alpine.sh
```

---

# Debian

## Dependências

```bash
sudo apt update

sudo apt install \
smartmontools \
lm-sensors \
htop -y
```

## Script

```bash
#!/bin/bash

ARQ="$HOME/Revisao-Debian.txt"

echo "===== REVISAO DEBIAN =====" > "$ARQ"

date >> "$ARQ"

echo "" >> "$ARQ"
echo "===== DISTRIBUICAO =====" >> "$ARQ"
cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== ATUALIZACOES =====" >> "$ARQ"
apt list --upgradable 2>/dev/null >> "$ARQ"

echo "" >> "$ARQ"
df -h >> "$ARQ"

echo "" >> "$ARQ"
free -h >> "$ARQ"

echo "" >> "$ARQ"
lscpu >> "$ARQ"

echo "" >> "$ARQ"
systemctl --failed >> "$ARQ"

echo "" >> "$ARQ"
journalctl -p 3 -xb -n 50 >> "$ARQ"

echo "" >> "$ARQ"
smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
sensors >> "$ARQ" 2>/dev/null
```

---

# Ubuntu

## Dependências

```bash
sudo apt update

sudo apt install \
smartmontools \
lm-sensors \
htop -y
```

## Script

```bash
#!/bin/bash

ARQ="$HOME/Revisao-Ubuntu.txt"

echo "===== REVISAO UBUNTU =====" > "$ARQ"

date >> "$ARQ"

cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== SNAPS =====" >> "$ARQ"
snap list >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
echo "===== ATUALIZACOES =====" >> "$ARQ"
apt list --upgradable 2>/dev/null >> "$ARQ"

df -h >> "$ARQ"

free -h >> "$ARQ"

lscpu >> "$ARQ"

systemctl --failed >> "$ARQ"

journalctl -p 3 -xb -n 50 >> "$ARQ"

smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

sensors >> "$ARQ" 2>/dev/null
```

---

# Linux Mint

## Dependências

```bash
sudo apt update

sudo apt install \
smartmontools \
lm-sensors \
htop -y
```

## Script

```bash
#!/bin/bash

ARQ="$HOME/Revisao-Mint.txt"

echo "===== REVISAO LINUX MINT =====" > "$ARQ"

date >> "$ARQ"

cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== ATUALIZACOES =====" >> "$ARQ"
apt list --upgradable 2>/dev/null >> "$ARQ"

echo "" >> "$ARQ"
echo "===== DISCO =====" >> "$ARQ"
df -h >> "$ARQ"

echo "" >> "$ARQ"
echo "===== MEMORIA =====" >> "$ARQ"
free -h >> "$ARQ"

echo "" >> "$ARQ"
echo "===== CPU =====" >> "$ARQ"
lscpu >> "$ARQ"

echo "" >> "$ARQ"
echo "===== SERVICOS =====" >> "$ARQ"
systemctl --failed >> "$ARQ"

echo "" >> "$ARQ"
echo "===== LOGS =====" >> "$ARQ"
journalctl -p 3 -xb -n 50 >> "$ARQ"

echo "" >> "$ARQ"
smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
sensors >> "$ARQ" 2>/dev/null
```

---

# Fedora

## Dependências

```bash
sudo dnf install \
smartmontools \
lm_sensors \
htop
```

## Script

```bash
#!/bin/bash

ARQ="$HOME/Revisao-Fedora.txt"

echo "===== REVISAO FEDORA =====" > "$ARQ"

date >> "$ARQ"

cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== UPDATES =====" >> "$ARQ"
dnf check-update >> "$ARQ" 2>/dev/null

df -h >> "$ARQ"

free -h >> "$ARQ"

lscpu >> "$ARQ"

systemctl --failed >> "$ARQ"

journalctl -p 3 -xb -n 50 >> "$ARQ"

smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

sensors >> "$ARQ" 2>/dev/null
```

---

# Arch Linux

## Dependências

```bash
sudo pacman -S \
smartmontools \
lm_sensors \
htop
```

## Script

```bash
#!/bin/bash

ARQ="$HOME/Revisao-Arch.txt"

echo "===== REVISAO ARCH =====" > "$ARQ"

date >> "$ARQ"

cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== PACOTES ORFAOS =====" >> "$ARQ"
pacman -Qdtq >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
echo "===== DISCO =====" >> "$ARQ"
df -h >> "$ARQ"

echo "" >> "$ARQ"
echo "===== MEMORIA =====" >> "$ARQ"
free -h >> "$ARQ"

echo "" >> "$ARQ"
echo "===== CPU =====" >> "$ARQ"
lscpu >> "$ARQ"

echo "" >> "$ARQ"
echo "===== SERVICOS =====" >> "$ARQ"
systemctl --failed >> "$ARQ"

echo "" >> "$ARQ"
echo "===== LOGS =====" >> "$ARQ"
journalctl -p 3 -xb -n 50 >> "$ARQ"

echo "" >> "$ARQ"
smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
sensors >> "$ARQ" 2>/dev/null
```

---

# openSUSE

## Dependências

```bash
sudo zypper install \
smartmontools \
sensors \
htop
```

## Script

```bash
#!/bin/bash

ARQ="$HOME/Revisao-openSUSE.txt"

echo "===== REVISAO OPENSUSE =====" > "$ARQ"

date >> "$ARQ"

cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== PACOTES ORFAOS =====" >> "$ARQ"
zypper packages --orphaned >> "$ARQ"

echo "" >> "$ARQ"
df -h >> "$ARQ"

echo "" >> "$ARQ"
free -h >> "$ARQ"

echo "" >> "$ARQ"
lscpu >> "$ARQ"

echo "" >> "$ARQ"
systemctl --failed >> "$ARQ"

echo "" >> "$ARQ"
journalctl -p 3 -xb -n 50 >> "$ARQ"

echo "" >> "$ARQ"
smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
sensors >> "$ARQ" 2>/dev/null
```

---

# Alpine Linux

## Dependências

```bash
sudo apk add \
smartmontools \
lm-sensors \
htop
```

## Script

```bash
#!/bin/sh

ARQ="$HOME/Revisao-Alpine.txt"

echo "===== REVISAO ALPINE =====" > "$ARQ"

date >> "$ARQ"

cat /etc/os-release >> "$ARQ"

echo "" >> "$ARQ"
echo "===== PACOTES =====" >> "$ARQ"
apk info >> "$ARQ"

echo "" >> "$ARQ"
echo "===== DISCO =====" >> "$ARQ"
df -h >> "$ARQ"

echo "" >> "$ARQ"
echo "===== MEMORIA =====" >> "$ARQ"
free -h >> "$ARQ"

echo "" >> "$ARQ"
echo "===== CPU =====" >> "$ARQ"
cat /proc/cpuinfo >> "$ARQ"

echo "" >> "$ARQ"
smartctl -H /dev/sda >> "$ARQ" 2>/dev/null

echo "" >> "$ARQ"
sensors >> "$ARQ" 2>/dev/null
```

---

# Como Executar

Dar permissão:

```bash
chmod +x revisao.sh
```

Executar:

```bash
./revisao.sh
```

---

# Resultado

Cada script gera um relatório próprio:

```text
Revisao-Debian.txt
Revisao-Ubuntu.txt
Revisao-Mint.txt
Revisao-Fedora.txt
Revisao-Arch.txt
Revisao-openSUSE.txt
Revisao-Alpine.txt
```

---

# Observação Importante

Os scripts acima assumem que o disco principal é:

```text
/dev/sda
```

Caso utilize SSD NVMe, substitua por:

```text
/dev/nvme0
```

Você pode descobrir o nome correto utilizando:

```bash
lsblk
```

---

# Objetivo Educacional

Além da manutenção preventiva, estes scripts servem como material de estudo para:

- Shell Script;
- Administração Linux;
- Monitoramento de sistemas;
- Diagnóstico de hardware;
- Coleta automática de informações;
- Geração de relatórios.
