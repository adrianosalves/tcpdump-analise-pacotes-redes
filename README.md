# TCPDUMP - Analise de pacotes de redes

Uso dessa ferramenta é para analise do trafego de rede.

Usado por profisionais/administradores de redes de computadores para analise de vulnerabilidade, por exemplo caso seu servidor web esteja sofrendo algum ataque externo na rede, é possivel realizar a captura dos pacotes de rede e analisas as informações.

## Exemplo 1: Instalando o **TCPDUMP** no linux.

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

## Exemplo 2: Analisando pacote na rede.

![image](https://user-images.githubusercontent.com/33209944/210156323-1d0afb28-52d4-4792-9c22-dc74d0a252d0.png)

O **TCPDUMP** ele faz um **DUMP** do trafego de rede mostrando em tela a descrição da conexão e do conteúdo dos pacotes que está passando na rede durante a interface de rede que foi selecionada no comando, o exemplo acima está analisando a interface de rede **eth0** do Linux. 

Observe que temos muita informação!

Imagine que queremos analisar um servidor Web que pode estar sofrendo um ataque externo?

É necessário filtrar essas informações!

Existe muitas opções de parametros que pode ser usado. Caso tenha interesse em saber digite o comando **man tcpdump**.

## Exemplo 3: Capturar e Gravar um arquivo!

Vamos colocar um situação em que você deseja capturar o trafego e analsar o conteúdo mais tarde.

Podemos usar o seguintes comando:

tcpdump -w "nome-do-arquivo.cap"

Primeiro vamos identificar o ip do nosso computador Linux:

![image](https://user-images.githubusercontent.com/33209944/210157430-cf4262dc-3fa6-4438-b255-aa164b814324.png)

Observer que fizemos uma consulta onde o IP do nosso Linux é **172.23.56.168**

Segundo vamos deixar atraves de um computador Windows realizar uma consulta de **ping** (ICMP) para o IP do Linux **172.23.56.168**:

![image](https://user-images.githubusercontent.com/33209944/210157492-da48a9f1-4b66-4c9f-9ff8-775bc7588a8e.png)

Terceiro iremos interceptar essas informações e gravar em um arquivo usando a flag **-w**.

```
┌──(kali㉿ALVESNET-NT001)-[/mnt/c/Install/tcpdump-analise]
└─$ sudo tcpdump -w minha-analise.cap
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
^C167 packets captured
167 packets received by filter
0 packets dropped by kernel

┌──(kali㉿ALVESNET-NT001)-[/mnt/c/Install/tcpdump-analise]
└─$

```

Se fizermos uma consulta do arquivo com o simples comando **cat** não será possivel ler essas informações pois o aplicativo padrão que ler esse tipo de arquivo com a extensão .cap é o **Wireshark**:

![image](https://user-images.githubusercontent.com/33209944/210157560-e9e2ffd9-1e8d-4ff5-8f2d-f09533b1d686.png)

Porem o **tcpdump** utiliza um outro tipo de flag **-r** que possibilita ler o conteúdo do arquivo em modo texto:

![image](https://user-images.githubusercontent.com/33209944/210157587-a4f40d46-57fc-416f-b249-9052a56afe31.png)

Agora gostariamos de filtrar as informações do arquivo apenas das consultas **ICMP**, podemos usar o seguinte comando:

![image](https://user-images.githubusercontent.com/33209944/210157700-7dcd746e-9fe4-4752-b4f9-4e31a6c566f8.png)

## Exemplo 4: Captura de pacotes e filtrando ao mesmo tempo sem gravar arquivo...

No exemplo abaixo fizemos uma consulta apenas do **protocolo ICMP** para descobrir quem está fazendo solicitação de **ping** dentro da rede. Podemos fazendo consulta e filtrar outros protocolos (http, udp, tcp etc...).

![image](https://user-images.githubusercontent.com/33209944/210157907-1cf50a61-639d-4a6f-acad-f48ae9a231cd.png)

## Exemplo 5: Captura de pacotes e filtrando o protocolo ARP...

No exemplo abaixo a consulta ao protocolo ARP podemos descobrir quem está fazendo o ataque **man-in-the-middle** se existe algum atacante tentando se passar pelo roteador dentro da rede.

![image](https://user-images.githubusercontent.com/33209944/210158028-6a3a0327-005e-4e39-9d9c-b30a58f870d4.png)

## Exemplo 6: Captura de pacotes e filtrando com limite...

No exemplo abaixo limitando o nosso filtro com até 4 consultas *ICMP*

![image](https://user-images.githubusercontent.com/33209944/210158075-2628c826-5045-4f79-af83-ea4529de1c38.png)

## Exemplo 7: Captura de pacotes e filtrando, sem resolução de nome de computadores...

No exemplo abaixo eliminando com a flag **-n** a resolução do nome de computadores.

![image](https://user-images.githubusercontent.com/33209944/210158119-40dc4db2-b4af-476a-9f5f-16d0c984abb2.png)

## Exemplo 8: ...filtrando, para descobrir a origem dos pacotes...

Vamos descobrir o IP da nossa estação windows (Possivel atacante!) de origem, com o uso das seguintes flag **-src** e o IP.

![image](https://user-images.githubusercontent.com/33209944/210158258-2bd93c66-e343-4e05-8508-352924e88d8f.png)

A situação mencionada acima lembra muito bem um possivel ataque de **DDOS** caso não se tenha um IDS (Sistema de Detecção de Intruso) podemos usar o **tcpdump** para analisar os pacotes da rede, e caso identifique um possivel ataque sabendo a origem pelo **IP** podemos bloquea esse ataque restringir a origem do IP. 

