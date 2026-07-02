![Uma imagem contendo Logotipo Descrição gerada
automaticamente](./media/image1.png){width="5.905555555555556in"
height="2.3361111111111112in"}

Relatório de CTF

Neighbour -- TryHackMe

+:-----------------------------------:+:--------------------------------------:+
| **Informações do documento**                                                 |
+-------------------------------------+----------------------------------------+
| **Referência**                      | Neighbour -- Mitchell Santana Miyake   |
+-------------------------------------+----------------------------------------+
| **N° Revisão**                      | 1                                      |
+-------------------------------------+----------------------------------------+
| **Data de publicação**              | 09/11/2025                             |
+-------------------------------------+----------------------------------------+
| **Link**                            | <https://tryhackme.com/room/neighbour> |
+-------------------------------------+----------------------------------------+

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

[Contextualização [2](#_heading=h.gjdgxs)](#_heading=h.gjdgxs)

[Desenvolvimento [3](#_heading=h.1fob9te)](#_heading=h.1fob9te)

[Find the flag on your neighbor\'s logged in page!
[3](#_Toc1879902603)](#_Toc1879902603)

[Conclusão [5](#_heading=h.1t3h5sf)](#_heading=h.1t3h5sf)

[Referências [5](#_heading=h.4d34og8)](#_heading=h.4d34og8)

[]{#_heading=h.gjdgxs .anchor}

Contextualização

A sala \"Neighbour\" da TryHackMe é um desafio de nível fácil, focado em
atividades de *red team* em um ambiente Linux. O objetivo é explorar
falhas em um novo serviço de nuvem, denominado \"Authentication
Anywhere\", onde o jogador deve tentar encontrar e acessar segredos
pertencentes a outros usuários, o que geralmente envolve a exploração de
referências de objetos diretos inseguras.

[]{#_heading=h.1fob9te .anchor}Desenvolvimento

[]{#_Toc1879902603 .anchor}Find the flag on your neighbor\'s logged in
page!

Primeiramente, utilizamos o nmap para verificar quais portas estão
abertas na máquina alvo.

![](./media/image4.png){width="5.90625in" height="3.4375in"}

Verificamos que a porta 80 está aberta, logo podemos acessar o endereço
da máquina pelo navegador.

![](./media/image5.png){width="5.90625in" height="2.71875in"}

Somos recebidos por uma página de login, a qual sugere que usuários sem
conta utilizem a conta de convidado para logar, ao apertar Ctrl+U como
sugerido o código fonte da página é exibido, onde se encontra o login de
convidado nos comentários do código.

![](./media/image6.png){width="5.90625in" height="4.604166666666667in"}

Utilizando as credenciais de convidado guest:guest obtemos acesso à
seguinte página.

![](./media/image7.png){width="5.90625in" height="1.3541666666666667in"}

O parâmetro user se encontra na url da página, previamente foi citado a
existência de um usuário admin, logo podemos tentar substituir guest por
admin.

![](./media/image8.png){width="5.90625in" height="1.1979166666666667in"}

Dessa maneira encontramos a flag :
**flag{66be95c478473d91a5358f2440c7af1f}**

[]{#_heading=h.1t3h5sf .anchor}Conclusão

O CTF Neighbour proporcionou um aprendizado valioso, especialmente no
reconhecimento de falha de controle de acesso a dados e exploração de
vulnerabilidades do tipo IDOR. Demonstrou a importância de validar e
restringir estritamente as permissões de acesso aos recursos de um
usuário, garantindo que ids não possam ser manipulados para acessar
informações de terceiros. Além disso, a sala reforçou as habilidades de
enumerar serviços e a importância de revisar o código ou o comportamento
da aplicação web para identificar padrões de falhas de autenticação e
autorização em ambientes Linux e serviços baseados em nuvem.

[]{#_heading=h.4d34og8 .anchor}Referências
