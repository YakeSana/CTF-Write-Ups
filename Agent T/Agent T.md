![Logotipo Guardian](./media/image1.png)

# Relatório de CTF: Agent T -- TryHackMe

## Informações do Documento

| Campo | Detalhe |
| :--- | :--- |
| **Referência** | CTF de estudo -- Mitchell Santana Miyake |
| **N° Revisão** | 1 |
| **Data de publicação** | 10/10/2025 |
| **Link** | https://tryhackme.com/room/agentt |

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
  * [Task 1: Find the Flag](#task-1-find-the-flag)
* [Conclusão](#conclusão)
* [Referências](#referências)

---

## Contextualização

O CTF Agent T sugere que há algo errado com o servidor e desafia o atacante a obter acesso a ele e obter uma flag, por meio de varredura de portas, análise de requisições web e escalonamento de privilégios.

## Desenvolvimento

### Task 1: Find the Flag

Utilizando o nmap é possível observar que o servidor está com a porta 80 aberta, logo aceita requisições HTTP.

![Resultado Nmap](./media/image2.png)

Logo acessamos a máquina virtual pelo navegador e somos recebidos com um dashboard de administrador.

![Dashboard Administrador](./media/image3.png)

Ao clicar no ícone do canto esquerdo superior a seguinte tela aparece, demonstrando que há algum acesso mal configurado ou vulnerabilidade, visto que o `index.html` não está acessível.

![Erro de Acesso](./media/image4.png)

Seguindo a dica da AI do TryHackMe de olhar com atenção os headers, utilizamos as ferramentas de desenvolvedor, que nos possibilitaram observar que o header da requisição que obtém o html do site apresenta a seguinte característica: `X-Powered-By: PHP/8.1.0-dev`.

![Headers na ferramenta de desenvolvedor](./media/image5.png)

Após uma busca na internet sobre vulnerabilidades desta versão do PHP, encontrei um exploit, o qual se trata de um código python, como consta na referência.

![Pesquisa de Exploit](./media/image6.png)

![Código do Exploit](./media/image7.png)

A execução do código e a inserção da url do servidor resultam no escalonamento de privilégio, como demonstra a execução dos comandos `id` e `whoami`.

![Escalonamento de privilégio no terminal](./media/image8.png)

Após obter privilégios, basta achar a flag dentro do servidor com comandos como o `find` e abri-la com o `cat`.

![Busca pela Flag](./media/image9.png)

![Flag encontrada](./media/image10.png)

## Conclusão

Apesar do desafio proposto ser do nível fácil ele me proporcionou um aprendizado significativo em investigação digital e resolução de problemas. Ao longo das etapas, foi necessário pesquisar, testar abordagens e interpretar pistas, o que estimulou o desenvolvimento do meu pensamento crítico. Dito isso, ele é um ótimo CTF para estimular a busca ativa de informação e interpretação de informações.

## Referências

* https://www.exploit-db.com/exploits/49933
* https://tryhackme.com/echo
* https://chatgpt.com