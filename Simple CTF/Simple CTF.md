![Uma imagem contendo Logotipo Descrição gerada
automaticamente](./media/image1.png){width="5.905555555555556in"
height="2.3361111111111112in"}

Relatório de CTF

Simple CTF -- TryHackMe

+:-----------------------------------:+:-----------------------------------:+
| **Informações do documento**                                              |
+-------------------------------------+-------------------------------------+
| **Referência**                      | Simple CTF -- Mitchell Santana      |
|                                     | Miyake                              |
+-------------------------------------+-------------------------------------+
| **N° Revisão**                      | 1                                   |
+-------------------------------------+-------------------------------------+
| **Data de publicação**              | 10/10/2025                          |
+-------------------------------------+-------------------------------------+
| **Link**                            | https://tryhackme.com/room/easyctf  |
+-------------------------------------+-------------------------------------+

  ----------------------- ----------------------- -----------------------
  **Redação**             Mitchell Santana Miyake Estudante

  **Revisão**             Nome do revisor         Orientador

  **Aprovação**           Nome do aprovador       Diretor
  ----------------------- ----------------------- -----------------------

+:-----------------------:+:-----------------------:+:---------------------------------------------:+
| **Histórico de revisões**                                                                         |
+-------------------------+-------------------------+-----------------------------------------------+
| **N°**                  | **Entregas**            | **Descrição**                                 |
+-------------------------+-------------------------+-----------------------------------------------+
| **0**                   | 10/10/2025              | Produção                                      |
+-------------------------+-------------------------+-----------------------------------------------+
| **1**                   | DD/MM/AAAA              | Revisão                                       |
+-------------------------+-------------------------+-----------------------------------------------+
| **2**                   | DD/MM/AAAA              | Aprovação                                     |
+-------------------------+-------------------------+-----------------------------------------------+

**Sumário**

[Contextualização [2](#_Toc1764544402)](#_Toc1764544402)

[Desenvolvimento [2](#_Toc1380808917)](#_Toc1380808917)

[How many services are running under port 1000?
[3](#_Toc1157777064)](#_Toc1157777064)

[What is running on the higher port?
[3](#_Toc802388050)](#_Toc802388050)

[What\'s the CVE you\'re using against the application?
[3](#_Toc1230158064)](#_Toc1230158064)

[To what kind of vulnerability is the application vulnerable?
[5](#_Toc613982002)](#_Toc613982002)

[What\'s the password? [6](#_Toc982728234)](#_Toc982728234)

[Where can you login with the details obtained?
[7](#_Toc1888000575)](#_Toc1888000575)

[What\'s the user flag? [7](#_Toc1940629014)](#_Toc1940629014)

[Is there any other user in the home directory? What\'s its name?
[7](#_Toc723487049)](#_Toc723487049)

[What can you leverage to spawn a privileged shell?
[8](#_Toc1697195865)](#_Toc1697195865)

[What\'s the root flag? [8](#_Toc937511169)](#_Toc937511169)

[Conclusão [8](#_Toc1688449924)](#_Toc1688449924)

[Referências [9](#_Toc2032091373)](#_Toc2032091373)

[]{#_Toc1764544402 .anchor}Contextualização

Aqui se encontram as informações básicas do CTF.

**[Subtítulo caso necessário]{.smallcaps}**

Espaço de tópico extra caso necessário

[]{#_Toc1380808917 .anchor}Desenvolvimento

[]{#_Toc1157777064 .anchor}How many services are running under port
1000?

Utilizando o seguinte comando "nmap -A -sV --sC 10.201.20.250
\--traceroute", obtemos a seguinte imagem, que nos permite afirmar que
existem **dois serviços** rodando neste endereço.

![](./media/image2.png){width="5.90625in" height="2.5833333333333335in"}

[]{#_Toc802388050 .anchor}What is running on the higher port?

Utilizando o resultado do mesmo comando **nmap** podemos notar que a
maior porta é a 2222 e nela está configurada o **SSH**.

[]{#_Toc1230158064 .anchor}What\'s the CVE you\'re using against the
application?

Aplicamos o **GoBuster** no endereço para descobrir possíveis
subdomínios e obtivemos os seguintes resultados.

![](./media/image3.png){width="5.90625in" height="2.3645833333333335in"}

Ao acessar o subdomínio /simple encontramos a seguinte página, nela
podemos observar que ela utiliza da versão CMS Made Simple 2.2.8.

![](./media/image4.png){width="5.90625in" height="2.4479166666666665in"}

Após uma busca de vulnerabilidades desta versão, encontrei um exploit
que realiza uma injeção de sql no servidor.

![](./media/image5.png){width="4.52753937007874in"
height="3.7929122922134733in"}

Este exploit se trata de um script python que apresenta a seguinte
versão do CVE: **CVE-2019-9053**

![](./media/image6.png){width="5.90625in" height="3.09375in"}

[]{#_Toc613982002 .anchor}To what kind of vulnerability is the
application vulnerable?

Como descrito no passo anterior a vulnerabilidade se trata de um SQL
injection ou **sqli.**

![](./media/image5.png){width="5.90625in" height="4.947916666666667in"}

[]{#_Toc982728234 .anchor}What\'s the password?

Utilizamos o seguinte comando para rodar o script.

![](./media/image7.png){width="5.90625in" height="0.1875in"}

Em sequência obtemos as informações de login de um usuário.

![](./media/image8.png){width="5.90625in" height="1.2708333333333333in"}

Como a senha não foi disponibilizada utilizaremos a ferramenta **hydra**
para encontrá-la.

![](./media/image9.png){width="5.90625in" height="1.1354166666666667in"}

Após sua execução, a senha **secret** é revelada.

[]{#_Toc1888000575 .anchor}Where can you login with the details
obtained?

Agora que possuímos todos os dados de login podemos logar no **ssh**
pela porta 2222.

![](./media/image10.png){width="5.90625in" height="1.96875in"}

[]{#_Toc1940629014 .anchor}What\'s the user flag?

Já logado com a credencial mitch, fiz uma busca simples buscando dentro
dos diretórios onde encontrei a seguinte flag: **G00d j0b, keep up!**

![](./media/image11.png){width="5.90625in"
height="2.0416666666666665in"}

[]{#_Toc723487049 .anchor}Is there any other user in the home directory?
What\'s its name?

Após ir até o diretório home descobrimos que o outro usuário é
**sunbath**.

![](./media/image12.png){width="3.2252799650043746in"
height="1.0584251968503937in"}

[]{#_Toc1697195865 .anchor}What can you leverage to spawn a privileged
shell?

Utilizando o sudo --l, verificamos se o usuário mitch possui alguma
permissão de executar algo com permissões root sem a necessidade de
logar no root, logo podemos aproveitar o **vim** para obter uma cli
privilegiada.

[]{#_Toc937511169 .anchor}What\'s the root flag?

Utilizando a vulnerabilidade referenciada na última questão, rodamos o
comando **sudo vim --c '!sh'** para obter acesso ao usuário root.

![](./media/image13.png){width="5.90625in"
height="2.7916666666666665in"}

Por fim, navegamos até o usuário root e obtemos a flag: **W3ll d0n3. You
made it!**

![](./media/image14.png){width="5.90625in" height="1.46875in"}

[]{#_Toc1688449924 .anchor}Conclusão

O *Simple* CTF do TryHackMe trata de enumeração, escalonamento de acesso
e exploração de vulnerabilidades. Durante o desafio ele promoveu uso de
ferramentas essenciais como nmap, gobuster e scripts de pós-exploração e
me estimulou a pensar na lógica por trás das vulnerabilidades. Portanto,
ele é um ótimo CTF para adquirir conhecimento sobre ganho de acesso e
exploração de vulnerabilidades.

[]{#_Toc2032091373 .anchor}Referências

- <https://www.codecademy.com/resources/docs/cybersecurity/nmap/aggressive-scan>

- <https://tryhackme.com/echo>

- <https://github.com/OJ/gobuster>

- <https://github.com/advisories/GHSA-rrqg-2h39-2567>

- <https://packetstorm.news/files/id/152356>

- <https://www.kali.org/tools/hydra/>

- <https://medium.com/@akerkar34/simple-ctf-tryhackme-walkthrough-13fae8abe32d>
