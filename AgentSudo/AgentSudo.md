![Uma imagem contendo Logotipo Descrição gerada
automaticamente](./media/image1.png){width="5.905555555555556in"
height="2.3361111111111112in"}

Relatório de CTF

Agent Sudo -- TryHackMe

+:-----------------------------------:+:---------------------------------------:+
| **Informações do documento**                                                  |
+-------------------------------------+-----------------------------------------+
| **Referência**                      | Agent Sudo -- Mitchell Santana Miyake   |
+-------------------------------------+-----------------------------------------+
| **N° Revisão**                      | 1                                       |
+-------------------------------------+-----------------------------------------+
| **Data de publicação**              | 07/11/2025                              |
+-------------------------------------+-----------------------------------------+
| **Link**                            | https://tryhackme.com/room/agentsudoctf |
+-------------------------------------+-----------------------------------------+

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

[Contextualização [2](#_Toc1479295293)](#_Toc1479295293)

[Desenvolvimento [3](#_Toc342732802)](#_Toc342732802)

[How many open ports? [3](#_Toc1643360377)](#_Toc1643360377)

[How you redirect yourself to a secret page?
[3](#_Toc869237730)](#_Toc869237730)

[What is the agent name? [4](#_Toc1251126384)](#_Toc1251126384)

[FTP password. [4](#_Toc1971783912)](#_Toc1971783912)

[Zip file password. [4](#_Toc624621439)](#_Toc624621439)

[Steg password. [6](#_Toc1045966290)](#_Toc1045966290)

[Who is the other agent (in full name)?
[7](#_Toc1949463197)](#_Toc1949463197)

[SSH password. [8](#_Toc167478154)](#_Toc167478154)

[What is the user flag? [8](#_Toc1588734368)](#_Toc1588734368)

[CVE number for the escalation. (Format: CVE-xxxx-xxxx)
[9](#_Toc1804197694)](#_Toc1804197694)

[What is the root flag? [10](#_Toc523615562)](#_Toc523615562)

[Who is Agent R? [11](#_Toc103516579)](#_Toc103516579)

[Conclusão [11](#_Toc751811250)](#_Toc751811250)

[Referências [11](#_Toc856275495)](#_Toc856275495)

[]{#_Toc1479295293 .anchor}Contextualização

O CTF Agent Sudo do TryHackMe é um desafio que simula um teste de
invasão a um servidor secreto. O objetivo central foi realizar a
escalada de privilégios, o que exigiu a aplicação de técnicas de
enumeração, força bruta e exploração de vulnerabilidades específicas
para comprometer completamente a máquina alvo e capturar as flags de
usuário e root.

[]{#_Toc342732802 .anchor}Desenvolvimento

[]{#_Toc1643360377 .anchor}How many open ports?

Utilizando o nmap com as configurações -sV e --sC, obtemos que o
endereço da maquina possui três portas abertas.

![](./media/image2.png){width="5.90625in" height="3.5729166666666665in"}

[]{#_Toc869237730 .anchor}How you redirect yourself to a secret page?

Como a porta 80 da máquina está aberta podemos acessá-la pelo navegador.
Ao abrir a página nos deparamos com a resposta **user-agent.**

![](./media/image3.png){width="5.90625in" height="1.5625in"}

[]{#_Toc1251126384 .anchor}What is the agent name?

Utilizando requisições curl com os parâmetros A e L podemos realizar um
spoofing com as iniciais dos agentes, dessa maneira foi obtido o nome
**chris**.

![](./media/image4.png){width="5.90625in" height="2.4166666666666665in"}

[]{#_Toc1971783912 .anchor}FTP password.

Para obter a senha do FTP utilizaremos o Hydra como método de força
bruta, passando o usuário obtido como parâmetro e utilizando a wordlist
rockyou.txt.

![](./media/image5.png){width="5.90625in"
height="0.8020833333333334in"}Dessa maneira foi obtida a senha
**crystal** para o usuário chris.

[]{#_Toc624621439 .anchor}Zip file password.

Primeiramente devemos nos conectar ao servidor FTP utilizando as
credenciais previamente obtidas.

![](./media/image6.png){width="5.90625in"
height="2.7395833333333335in"}Para então obter os arquivos do servidor
utilizando o comando **mget.**

![](./media/image7.png){width="5.90625in" height="2.6770833333333335in"}

Ao ler um dos arquivos obtidos, recebemos uma mensagem que sugere que as
imagens possuem arquivos escondidos.

![](./media/image8.png){width="5.90625in" height="0.6875in"}

Para verificar se as imagens escondem algo e extrair tais conteudos,
utilizaremos o **BinWalk.**

![](./media/image9.png){width="5.90625in" height="1.2291666666666667in"}

Logo percebemos que o diretorio \_cutie.png.extracted foi extraido da
imagem, para obter a senha do arquivo zip dentro dele utilizaremos as
ferramentas do johntheripper, como o zip2john e o john. Dessa maneira
foi obtida a senha **alien**.

![](./media/image10.png){width="5.90625in"
height="1.9791666666666667in"}

[]{#_Toc1045966290 .anchor}Steg password.

Em seguida, utilizamos o 7z para descompactar o pacote.

![](./media/image11.png){width="5.90625in"
height="3.2291666666666665in"}

Para enfim obter a senha criptografada na mensagem a seguir.

![](./media/image12.png){width="5.90625in"
height="1.5520833333333333in"}

Para decodificar a senha utilizamos o
[CyberChef,](https://gchq.github.io/CyberChef/?ref=blog.qz.sg) que
identificou a codificação de base64. Dessa maneira foi obtida a senha
**Area51**.

![](./media/image13.png){width="5.90625in"
height="3.9895833333333335in"}

[]{#_Toc1949463197 .anchor}Who is the other agent (in full name)?

Utilizando a senha obtida e o steghide podemos verificar informações
escondidas na outra imagem. Dessa maneira foi obtida o nome do outro
agente, james.

![](./media/image14.png){width="5.90625in" height="2.53125in"}

[]{#_Toc167478154 .anchor}SSH password.

O último passo também inclui uma senha, neste caso **hackerrules!** é a
senha do SSH.

![](./media/image15.png){width="5.90625in"
height="3.9479166666666665in"}

[]{#_Toc1588734368 .anchor}What is the user flag?

Realizando uma varredura simples nos arquivos do usuário, obtemos a flag
**b03d975e8c92a7c04146cfa7a5a313c7**

![](./media/image16.png){width="5.90625in"
height="0.3854166666666667in"}

**What is the incident of the photo called?**

Realizando uma busca de imagem utilizando o TinEye, obtemos o seguinte
resultado.

![](./media/image17.png){width="5.90625in" height="2.25in"}

O TinEye mostra um artigo que descreve o incidente da foto, neste caso:
**Roswell alien autopsy**

![](./media/image18.png){width="5.90625in"
height="2.4895833333333335in"}

[]{#_Toc1804197694 .anchor}CVE number for the escalation. (Format:
CVE-xxxx-xxxx)

Para realizar o escalamento verificamos as permissoes de usuario do root
que james possui com o comando sudo --l.

![](./media/image19.png){width="5.90625in" height="0.71875in"}

Fazendo uma pesquisa de vulnerabilidades sobre (ALL, !root) /bin/bash
encontramos o seguinte CVE: CVE-2019-14287

![](./media/image20.png){width="5.90625in"
height="2.5104166666666665in"}

[]{#_Toc523615562 .anchor}What is the root flag?

De acordo com o registro de vulnerabilidade, versões do sudo inferiores
a 1.8.28, permitem o login não autorizado ao usuário root utilizando
sudo -u \\#\$((0xffffffff))

![](./media/image21.png){width="5.3340780839895015in"
height="0.8647036307961505in"}

Navegando até os arquivos do usuário root e verificando seus arquivos,
obtemos a a flag **b53a02f55b57d4439e3341834d70c062**

![](./media/image22.png){width="5.90625in"
height="2.1770833333333335in"}

[]{#_Toc103516579 .anchor}Who is Agent R?

O arquivo root.txt também inclui o nome do Agent R, seu nome é
**DesKel.**

[]{#_Toc751811250 .anchor}Conclusão

A conclusão deste CTF demonstrou o valor da metodologia estruturada no
pentesting. O principal aprendizado foi o aprimoramento prático em
técnicas de enumeração eficaz utilizando ferramentas como GoBuster e
Nmap, essenciais para descobrir o acesso inicial. O desafio exigiu
domínio em análise forense básica, utilizando o Binwalk, e culminou em
uma aplicação crítica de escalada de privilégios, reforçando a
capacidade de identificar e explorar vulnerabilidades específicas para
alcançar o controle de root. O sucesso neste CTF traduziu o conhecimento
teórico em habilidades acionáveis, comprovando a importância da
persistência e da correlação de informações para a resolução completa de
um cenário de segurança.

[]{#_Toc856275495 .anchor}Referências

- [WriteUp](https://blog.qz.sg/agent-sudo-ctf-tryhackme/)

- [BinWalk](https://www.kali.org/tools/binwalk/)

- [Exploit](https://www.exploit-db.com/exploits/47502)
