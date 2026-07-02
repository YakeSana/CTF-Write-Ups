![Uma imagem contendo Logotipo Descrição gerada
automaticamente](./media/image1.png){width="5.905555555555556in"
height="2.3361111111111112in"}

Relatório de CTF

RootMe -- TryHackMe

+:-----------------------------------:+:------------------------------------:+
| **Informações do documento**                                               |
+-------------------------------------+--------------------------------------+
| **Referência**                      | RootMe -- Mitchell Santana Miyake    |
+-------------------------------------+--------------------------------------+
| **N° Revisão**                      | 1                                    |
+-------------------------------------+--------------------------------------+
| **Data de publicação**              | 13/11/2025                           |
+-------------------------------------+--------------------------------------+
| **Link**                            | <https://tryhackme.com/room/rrootme> |
+-------------------------------------+--------------------------------------+

  ----------------------- ----------------------- -----------------------
  **Redação**             Nome do realizador      Mitchell Santana Miyake

  **Revisão**             Nome do revisor         Orientador

  **Aprovação**           Nome do aprovador       Diretor
  ----------------------- ----------------------- -----------------------

+:-----------------------:+:-----------------------:+:---------------------------------------------:+
| **Histórico de revisões**                                                                         |
+-------------------------+-------------------------+-----------------------------------------------+
| **N°**                  | **Entregas**            | **Descrição**                                 |
+-------------------------+-------------------------+-----------------------------------------------+
| **0**                   | DD/MM/AAAA              | Produção                                      |
+-------------------------+-------------------------+-----------------------------------------------+
| **1**                   | DD/MM/AAAA              | Revisão                                       |
+-------------------------+-------------------------+-----------------------------------------------+
| **2**                   | DD/MM/AAAA              | Aprovação                                     |
+-------------------------+-------------------------+-----------------------------------------------+

**Sumário**

[Contextualização [2](#_Toc1615540245)](#_Toc1615540245)

[Desenvolvimento [3](#_Toc132958541)](#_Toc132958541)

[Scan the machine, how many ports are open?
[3](#_Toc1897472106)](#_Toc1897472106)

[What version of Apache is running?
[3](#_Toc1156425530)](#_Toc1156425530)

[What service is running on port 22?
[3](#_Toc972120563)](#_Toc972120563)

[Find directories on the web server using the GoBuster tool.
[3](#_Toc772619414)](#_Toc772619414)

[Find a form to upload and get a reverse shell and find the flag. Find
user.txt [4](#_Toc1779449691)](#_Toc1779449691)

[Search for files with SUID permission; which file is weird?
[7](#_Toc720694685)](#_Toc720694685)

[Find a form to escalate your privileges.
[8](#_Toc1767519720)](#_Toc1767519720)

[Root.txt [8](#_Toc482651383)](#_Toc482651383)

[Conclusão [9](#_Toc2018918907)](#_Toc2018918907)

[Referências [9](#_Toc787584339)](#_Toc787584339)

[]{#_Toc1615540245 .anchor}Contextualização

O CTF RootMe da TryHackMe é um desafio de nível para iniciantes focado
em uma jornada completa de capture the flag em um ambiente Linux. A sala
orienta o jogador através das fases essenciais de um teste de
penetração: Reconhecimento (varredura de portas com Nmap e enumeração de
diretórios com GoBuster), Obtenção de Shell (encontrando e explorando
formulários de upload vulneráveis para obter uma reverse shell), e
Escalonamento de Privilégios (procurando por arquivos com permissões
SUID ou outras falhas de configuração para obter acesso root).

[]{#_Toc132958541 .anchor}Desenvolvimento

[]{#_Toc1897472106 .anchor}Scan the machine, how many ports are open?

Utilizando o nmap podemos escanear quantas portas estão abertas, neste
caso duas portas estão abertas.

![](./media/image4.png){width="5.90625in" height="2.78125in"}

[]{#_Toc1156425530 .anchor}What version of Apache is running?

Na mesma saída do nmap, encontramos o Apache rodando na versão 2.4.41

[]{#_Toc972120563 .anchor}What service is running on port 22?

O serviço SSH está rodando na porta 22.

[]{#_Toc772619414 .anchor}Find directories on the web server using the
GoBuster tool.

Seguindo a instrução do CTF, utilizamos o GoBuster para verificar os
subdiretórios do servidor.

![](./media/image5.png){width="5.90625in" height="2.65625in"}\
**What is the hidden directory?**

O diretório escondido é /panel.

![](./media/image6.png){width="5.90625in" height="2.8958333333333335in"}

[]{#_Toc1779449691 .anchor}Find a form to upload and get a reverse shell
and find the flag. Find user.txt

Utilizando /panel podemos fazer o upload de arquivos como o user.txt

![](./media/image7.png){width="5.90625in" height="2.1041666666666665in"}

O arquivo user.txt foi enviado com sucesso e está sendo exibido na tela,
logo podemos tentar utilizar o seguinte script para obter o reverse
shell.

![](./media/image8.png){width="5.90625in" height="4.09375in"}Devemos
também configurar o **netcat** para receber a conexão deste reverse
shell

![](./media/image9.png){width="5.90625in" height="0.6354166666666666in"}

O resultado da tentativa foi o seguinte:

![](./media/imagea.png){width="5.90625in" height="2.90625in"}Arquivos no
formato .php estão sendo bloqueados, portanto podemos tentar utilizar
formatos como .php.jpg ou .php5

Utilizando o formato .php5 no script, obtivemos acesso no **netcat** que
havíamos configurado.

![](./media/imageb.png){width="5.90625in" height="3.6979166666666665in"}

Logo podemos realizar uma busca utilizando o find para encontrar o
user.txt

![](./media/imagec.png){width="5.90625in" height="3.9375in"}Dessa
maneira encontramos o user.txt e sua flag

![](./media/imaged.png){width="5.90625in" height="0.875in"}

[]{#_Toc720694685 .anchor}Search for files with SUID permission; which
file is weird?

Para procurar onde o usuário possui permissões SUID utilizamos o comando
find / -user root --perm /4000 2\>/dev/null

![](./media/imagee.png){width="5.90625in" height="3.40625in"}Nesta saída
o diretório **/usr/bin/python2.7** parece estar fora de lugar.

[]{#_Toc1767519720 .anchor}Find a form to escalate your privileges.

Realizando uma busca de como se aproveitar da vulnerabilidade de
permissão do diretório **/usr/bin/python2.7** encontramos o seguinte
comando **python --c 'import os; os.execl("/bin/sh","sh","-p")'**, após
sua utilização podemos rodar o comando whoami para verificar nosso
usuário, neste caso obtemos acesso ao usuário root.

![](./media/imagef.png){width="5.90625in" height="3.1770833333333335in"}

[]{#_Toc482651383 .anchor}Root.txt

Por fim, após obter acesso ao usuário root, utilizamos o comando find
para encontrar o arquivo root.txt e sua flag

![](./media/image10.png){width="5.90625in"
height="1.2291666666666667in"}

[]{#_Toc2018918907 .anchor}Conclusão

A conclusão do desafio RootMe está centrada na consolidação de uma
metodologia de pentest ponta a ponta. O aprendizado reforçou a
importância da enumeração como passo inicial, bem como a exploração de
vulnerabilidades de upload de arquivos para obter acesso inicial à
máquina. Mais significativamente, o CTF destacou técnicas de
escalonamento de privilégios no Linux, ensinando a identificar binários
SUID mal configurados e a utilizar recursos do sistema operacional para
passar de um usuário comum para o utilizador root, obtendo domínio total
do sistema.

[]{#_Toc787584339 .anchor}Referências

- [Write
  Up](https://beginninghacking.net/2020/09/09/try-hack-me-rootme/)

<!-- -->

- Script [ReverseShell
  PHP](https://pentestmonkey.net/tools/web-shells/php-reverse-shell)

<!-- -->

- [Python SUID Exploit](https://gtfobins.github.io/gtfobins/python/)
