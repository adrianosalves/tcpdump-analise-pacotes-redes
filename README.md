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

Observe que temos muita informação!

Imagine que queremos analisar um servidor Web que pode estar sofrendo um ataque externo?

É necessário filtrar essas informações!

Existe muitas opções de parametros que pode ser usado. Caso tenha interesse em saber digite o comando **man tcpdump**.

Exemplo 3:

Vamos colocar um situação em que você deseja capturar o trafego e analsar o conteúdo mais tarde.

Podemos usar o seguintes comando:

tcpdump -w "nome-do-arquivo.cap"

Primeiro vamos identificar o ip do nosso computador Linux:

![image](https://user-images.githubusercontent.com/33209944/210157430-cf4262dc-3fa6-4438-b255-aa164b814324.png)

Observer que fizemos uma consulta onde o IP do nosso Linux é **172.23.56.168**

Segundo vamos deixar atraves de um computador Windows realizar uma consulta de **ping** (ICMP) para o IP do Linux **172.23.56.168**:

![image](https://user-images.githubusercontent.com/33209944/210157492-da48a9f1-4b66-4c9f-9ff8-775bc7588a8e.png)

Terceiro iremos interceptar essas informações e gravar em um arquivo.

```
┌──(kali㉿ALVESNET-NT001)-[/mnt/c/Install/tcpdump-analise]
└─$ sudo tcpdump -w minha-analise.cap
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
^C167 packets captured
167 packets received by filter
0 packets dropped by kernel

┌──(kali㉿ALVESNET-NT001)-[/mnt/c/Install/tcpdump-analise]
└─$
´´´

Se fizermos uma consulta do arquivo com o simples comando **cat** não será possivel ler essas informações:

![image](https://user-images.githubusercontent.com/33209944/210157560-e9e2ffd9-1e8d-4ff5-8f2d-f09533b1d686.png)

O **tcpdump** utiliza um outro tipo de flag (-r) que possibilita ler o conteúdo do arquivo em modo texto:

![image](https://user-images.githubusercontent.com/33209944/210157587-a4f40d46-57fc-416f-b249-9052a56afe31.png)




