![Logo](./media/image1.png)

# Relatório de CTF: Surfer -- TryHackMe

## Informações do Documento

| Campo | Detalhe |
| :--- | :--- |
| **Referência** | Surfer -- Mitchell Santana Miyake |
| **N° Revisão** | 1 |
| **Data de publicação** | 13/11/2025 |
| **Link** | https://tryhackme.com/room/surfer |

## Equipe Responsável

| Função | Nome | Cargo |
| :--- | :--- | :--- |
| **Redação** | Nome do realizador | Mitchell Santana Miyake |
| **Revisão** | Nome do revisor | Orientador |
| **Aprovação** | Nome do aprovador | Diretor |

## Histórico de Revisões

| N° | Entregas | Descrição |
| :---: | :--- | :--- |
| **0** | DD/MM/AAAA | Produção |
| **1** | DD/MM/AAAA | Revisão |
| **2** | DD/MM/AAAA | Aprovação |

---

## Sumário
* [Contextualização](#contextualização)
* [Desenvolvimento](#desenvolvimento)
  * [Uncover the flag on the hidden application page.](#uncover-the-flag-on-the-hidden-application-page)
* [Conclusão](#conclusão)
* [Referências](#referências)

---

## Contextualização

O CTF Surfer da TryHackMe é um desafio de nível fácil a intermediário focado na exploração de falhas em aplicações web. O principal objetivo é encontrar uma maneira de comprometer a máquina através de vulnerabilidades de injeção de comando, que são introduzidas ao tentar "surfar" a rede e interagir com um backend que manipula a entrada do usuário de forma insegura. A sala exige que o jogador enumere cuidadosamente os parâmetros da URL e os campos de entrada, aplicando técnicas para testar e explorar essas vulnerabilidades em um ambiente Linux.

## Desenvolvimento

### Uncover the flag on the hidden application page.

Primeiramente utilizamos o nmap para escanear e obter as portas abertas

![Imagem Nmap](./media/image4.png)

Podemos observar que a porta 80 está aberta, logo podemos utilizar o navegador para acessar o endereço da máquina.

![Imagem Navegador](./media/image.jpg)

A saída do nmap também citou a existência do robots.txt, logo podemos tentar acessá-lo.

![Imagem Robots.txt](./media/image5.png)

Dentro do robots.txt o subdomínio /backup/chat.txt é citado, vamos acessá-lo.

![Imagem Chat.txt](./media/image6.png)

Obtemos um registro de conversa, em que um dos usuários reclama sobre o usuário admin utilizar seu nome como credenciais, podemos então utilizar admin:admin para logar no sistema.

![Imagem Login](./media/image7.png)

No campo "Recent Activity" o subdomínio /internal/admin.php é mencionado, vamos tentar acessá-lo.

![Imagem Admin.php](./media/image8.png)

O site também possui um botão que retorna o seguinte relatório.

![Imagem Relatório](./media/image9.png)

Podemos utilizar o **burp** no foxyproxy com o **BurpSuite** para realizar o proxy da requisição deste relatório.

![Imagem BurpSuite](./media/imagea.png)

O campo url pode ser modificado da seguinte maneira para obtermos acesso ao subdomínio secreto.

![Imagem URL Modificada](./media/imageb.png)

Dessa maneira obtemos acesso ao subdomínio secreto e obtemos a flag

![Imagem Flag](./media/imagec.png)

## Conclusão

O aprendizado principal na realização do CTF Surfer foi a navegação de plataformas web com foco em interceptar, inspecionar e manipular requisições HTTP, permitindo a identificação e a exploração manual de vulnerabilidades.

## Referências
* https://medium.com/@josephalan17201972/surfer-tryhackme-write-up-1c54b7ea9e22