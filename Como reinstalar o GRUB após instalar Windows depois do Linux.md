# Resumo

Esta nota apresenta o processo de recuperação do boot do Linux quando o Windows é instalado posteriormente, sobrescrevendo o GRUB e impedindo o acesso ao sistema Linux. Também aborda a utilização de um ambiente Live para reinstalação do bootloader e restauração do menu de inicialização.

## Tópicos abordados

- Passos
- Comandos
- Finalização 

O Windows só entende a si mesmo, então quando é instalado depois de um Linux ele não vê o outro sistema operacional.

---

## Passos

Para a instalação, plug o mesmo pendrive que utilizou para baixar o sistema Linux na máquina e acesse a BIOS.  
Em boot, selecione para dar boot com o pendrive.

---

Acesse Linux distributions

Selecione o sistema OS  
Selecione a opção triy versão de teste

---

Procure o terminal

---

## Comandos

bash
sudo fdisk -l

sudo mount /dev/sda(numero da partição linux) /mnt/

Exemplo:

sudo mount /dev/sda4 /mnt/


---

Próximo comando:

sudo grub-install --root-directory=/mnt/ /dev/sda


---

## Finalização

Reinicie o computador e retire o pendrive.


