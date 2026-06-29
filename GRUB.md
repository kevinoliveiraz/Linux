# GRUB (GNU GRand Unified Bootloader)

## Resumo
O GRUB é o programa responsável por iniciar o sistema operacional quando o computador liga. Ele funciona como intermediário entre o hardware e o sistema instalado, permitindo escolher e controlar como o sistema vai iniciar.

---

## Tópicos abordados
- O que é o GRUB  
- Como ele funciona  
- O que ele faz além do básico  
- Estrutura básica  
- Reinstalação (casos comuns)  
- Por que ele é importante  

---

## O que é o GRUB
O GRUB é um bootloader (carregador de inicialização), muito usado em sistemas Linux.
Ele organiza qual sistema operacional será iniciado no computador 


---

## Como ele funciona
O processo de inicialização segue uma sequência simples:

1. O computador liga e a BIOS/UEFI inicializa o hardware  
2. O sistema procura o bootloader no disco  
3. O GRUB é carregado  
4. Ele exibe opções de sistemas (se houver mais de um)  
5. O sistema escolhido é enviado para o kernel iniciar  

O GRUB não executa o sistema, ele apenas prepara e entrega o controle.

---

## O que ele faz além do básico
O GRUB vai além de apenas iniciar sistemas:

- Permite dual boot (Linux e Windows no mesmo PC)  
- Oferece modo de recuperação do sistema  
- Permite parâmetros avançados de inicialização  
- Ajuda a recuperar sistemas que não estão iniciando corretamente  

---

## Estrutura básica
O GRUB trabalha com alguns elementos principais:

- `grub.cfg` → arquivo principal de configuração  
- `/boot` → diretório onde ficam kernels e arquivos de inicialização  
- módulos → componentes que adicionam suporte a sistemas de arquivos e recursos  

---

## Reinstalação (casos comuns)
Um cenário comum é quando o Windows é instalado após o Linux.

Isso pode sobrescrever o GRUB.

Solução típica:
- Inicializar um Live USB Linux  
- Reinstalar o GRUB no disco  
- Atualizar a configuração para reconhecer os sistemas instalados  

---

## Por que ele é importante
O GRUB é o ponto inicial da cadeia de inicialização do sistema.

Sem ele:
- o computador não sabe qual sistema iniciar  
- o dual boot deixa de funcionar  
- a recuperação do sistema fica mais limitada  

Ele é o controle central entre o hardware e o sistema operacional.
