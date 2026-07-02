![Logo](./media/image1.png)

# Relatório de CTF: Take Over -- TryHackMe

## Informações do Documento

| Campo | Detalhe |
| :--- | :--- |
| **Referência** | Take Over-- Mitchell Santana Miyake |
| **N° Revisão** | 1 |
| **Data de publicação** | 10/10/2025 |
| **Link** | https://tryhackme.com/room/takeover |

## Equipe Responsável

| Função | Nome | Cargo |
| :--- | :--- | :--- |
| **Redação** | Mitchell Santana Miyake | Estudante |
| **Revisão** | Nome do revisor | Orientador |
| **Aprovação** | Nome do aprovador | Diretor |

## Histórico de Revisões

| N° | Entregas | Descrição |
| :---: | :--- | :--- |
| **0** | 10/10/2025 | Produção |
| **1** | DD/MM/AAAA | Revisão |
| **2** | DD/MM/AAAA | Aprovação |

---

## Sumário
* [Contextualização](#contextualização)
* [Desenvolvimento](#desenvolvimento)
  * [What's the value of the flag?](#whats-the-value-of-the-flag)
* [Conclusão](#conclusão)
* [Referências](#referências)

---

## Contextualização

O CTF TakeOver envolve numeração de subdomínios e simula uma situação de sequestro de subdomínio.

## Desenvolvimento

### What's the value of the flag?

Iniciamos com o **nmap** para obter as portas abertas, com isso percebemos que a porta 80 está aberta.

![Imagem Nmap](./media/image2.png)

Seguindo a sugestão do CTF, adicionamos o endereço da máquina e seu domínio ao /etc/hosts utilizando o **nano** para editá-lo.

![Imagem Nano](./media/image3.png)

Logo o url se torna acessível e exibe a seguinte página.

![Imagem URL Acessível](./media/image4.png)

As instruções do CTF também citam que o domínio possui um subdomínio de suporte, logo devemos adicioná-lo ao /etc/hosts.

![Imagem Subdomínio Suporte](./media/image5.png)

Ao acessá-lo a seguinte página é exibida:

![Imagem Página Subdomínio](./media/image6.png)

Em seguida clicamos em "View Certificate", e analisamos o certificado da url, onde encontramos outro subdomínio.

![Imagem Certificado](./media/image7.png)

Novamente devemos adicionar este domínio ao /etc/hosts, utilizando o **nano**.

![Imagem Adição Nano](./media/image8.png)

Por fim, ao acessar este último domínio, somos recebidos com a url de um bucket s3 da AWS que contém a flag.

![Imagem Bucket AWS Flag](./media/image9.png)

## Conclusão

O CTF simula uma situação real de sequestro de domínio e me proporcionou um aprendizado relevante sobre interpretar o contexto do cliente e contribuiu para o meu entendimento de estruturas web. Logo, se trata de um ótimo CTF para introduzir e explicar sequestro de domínio.

## Referências
* https://github.com/Cyberretta/Write-Ups-THM/blob/main/TakeOver.md