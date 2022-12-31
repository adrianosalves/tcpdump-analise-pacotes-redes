# TCPDUMP - Analise de pacotes de redes

Uso dessa ferramenta analise de rede.

Usado por profisionais/administradores de rede para analise de vulnerabilidade exemplo caso seu servidor web esteja sofrendo algum ataque exeterno na rede, realizando a captura do pacote de rede.

Exemplo 1:

Instalando o **TCPDUMP** no linux.

```
└─$ sudo apt install tcpdump
[sudo] password for kali:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libperl5.34 perl-modules-5.34
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  tcpdump
0 upgraded, 1 newly installed, 0 to remove and 21 not upgraded.
Need to get 469 kB of archives.
After this operation, 1,368 kB of additional disk space will be used.
Get:1 http://http.kali.org/kali kali-rolling/main amd64 tcpdump amd64 4.99.1-4+b1 [469 kB]
Fetched 469 kB in 2s (299 kB/s)
Selecting previously unselected package tcpdump.
(Reading database ... 68282 files and directories currently installed.)
Preparing to unpack .../tcpdump_4.99.1-4+b1_amd64.deb ...
Unpacking tcpdump (4.99.1-4+b1) ...
Setting up tcpdump (4.99.1-4+b1) ...
Processing triggers for man-db (2.11.0-1+b1) ...
Scanning processes...
Scanning processor microcode...
Scanning linux images...
```

Exemplo 2:

Analisando pacote na rede.

![image](https://user-images.githubusercontent.com/33209944/210156323-1d0afb28-52d4-4792-9c22-dc74d0a252d0.png)

O **TCPDUMP** ele faz um **DUMP** do trafego de rede mostrando em tela a descrisção da conexão e do conteúdo dos pacotes que está passando na rede durante a interface de rede que foi selecionada no comando, o exemplo acima está analisando a interface de rede **eth0** do Linux.

Existe muitas opções de parametros que pode ser usado. Caso tenha interesse em saber digite o comando **man tcpdump**.

