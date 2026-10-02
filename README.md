# Gerenciador Individual de Tarefas

Uma plataforma web para organizar projetos, tarefas, backlog e sprints em um único fluxo de trabalho.

O projeto foi desenvolvido com uma proposta inspirada em ferramentas como Jira, mas com foco em simplicidade, uso individual e acompanhamento visual das atividades.

## Sobre o projeto

A plataforma permite que uma pessoa:

- Crie e selecione projetos;
- Cadastre, edite e exclua tarefas;
- Organize tarefas no backlog;
- Defina prioridade e prazo;
- Ordene manualmente as tarefas;
- Crie e planeje sprints;
- Associe tarefas às sprints;
- Acompanhe o trabalho em um quadro Kanban;
- Mova tarefas entre diferentes estados;
- Encerre sprints e consulte seu histórico;
- Busque e filtre tarefas;
- Continue utilizando os dados após recarregar a página.

## Fluxo principal

```text
Projeto
  ↓
Backlog
  ↓
Sprint planejada
  ↓
Sprint ativa
  ↓
Quadro Kanban
  ↓
Encerramento e histórico
```

## Funcionalidades

### Projetos

- Criação de projetos;
- Seleção entre diferentes projetos;
- Renomeação de projetos;
- Isolamento das tarefas e sprints por projeto.

### Tarefas

Cada tarefa possui:

- Identificador estável;
- Título obrigatório;
- Descrição opcional;
- Prioridade baixa, média ou alta;
- Prazo opcional;
- Estado: A fazer, Em andamento ou Concluído;
- Vínculo com projeto;
- Vínculo opcional com sprint.

Também é possível:

- Editar tarefas;
- Excluir tarefas com confirmação;
- Ordenar tarefas manualmente no backlog;
- Pesquisar por título ou identificador;
- Filtrar por prioridade e estado.

### Sprints

- Criação de sprints planejadas;
- Definição de nome, objetivo e período;
- Validação das datas;
- Associação de tarefas;
- Início de uma sprint;
- Limite de uma sprint ativa por projeto;
- Encerramento com confirmação;
- Histórico do resultado da sprint.

### Quadro Kanban

O quadro apresenta três colunas:

- A fazer;
- Em andamento;
- Concluído.

As tarefas podem ser movimentadas entre os estados, com atualização das contagens e persistência das alterações.

## Regras de negócio

- Um projeto pode possuir várias tarefas e sprints;
- Cada tarefa pertence a um único projeto;
- Uma tarefa pode estar no backlog ou em uma sprint;
- Uma tarefa não pode pertencer a mais de uma sprint ao mesmo tempo;
- Cada projeto pode ter no máximo uma sprint ativa;
- Toda tarefa começa no estado A fazer;
- A prioridade Média é utilizada como valor inicial;
- O título da tarefa é obrigatório;
- O objetivo da sprint é opcional;
- A data final da sprint deve ser igual ou posterior à data inicial;
- Ao encerrar uma sprint, tarefas concluídas permanecem nela;
- Tarefas pendentes retornam para o backlog;
- O histórico preserva o resumo do encerramento;
- A ordem do backlog é independente para cada projeto.

## Como o projeto foi construído

O desenvolvimento foi organizado utilizando o BMad como método de planejamento e execução.

A especificação do produto foi registrada no `SPEC.md`, contendo:

- Objetivos;
- Capacidades;
- Restrições;
- Regras de negócio;
- Decisões técnicas;
- Critérios de sucesso.

Depois, o trabalho foi dividido no `TASKS.md`, organizando as funcionalidades por dependência:

1. Fundação e navegação;
2. Estado, persistência e projetos;
3. Tarefas e backlog;
4. Planejamento de sprints;
5. Kanban e execução;
6. Histórico e encerramento;
7. Busca, acessibilidade e validação final.

Cada tarefa foi implementada e verificada individualmente antes da próxima etapa.

## Critérios de aceite

Os critérios de aceite foram utilizados para definir quando uma funcionalidade estava realmente pronta.

Por exemplo, para uma tarefa ser considerada criada corretamente, era necessário:

- Rejeitar título vazio;
- Associar a tarefa ao projeto selecionado;
- Iniciar no estado A fazer;
- Mantê-la sem sprint;
- Gerar um identificador estável;
- Persistir os dados;
- Exibir textos informados pelo usuário com segurança.

Esse processo garantiu que cada funcionalidade tivesse um resultado verificável.

## Tecnologias utilizadas

- HTML5;
- CSS3;
- JavaScript nativo;
- `localStorage`;
- Playwright para validação de fluxos;
- Git e GitHub para controle de versão;
- BMad para organização do desenvolvimento.

Não foram utilizados:

- Frameworks;
- npm;
- Banco de dados externo;
- Backend;
- APIs externas.

## Como executar

Como a aplicação é composta por um único arquivo HTML, não é necessário instalar dependências.

Basta:

1. Baixar ou clonar o repositório;
2. Abrir o arquivo `index.html` em um navegador;
3. Criar um projeto;
4. Começar a cadastrar tarefas.

Também é possível executar utilizando um servidor local, como a extensão Live Server do Visual Studio Code.

## Persistência dos dados

Os dados são armazenados no `localStorage` do navegador.

Isso significa que:

- Os dados permanecem após recarregar a página;
- Cada navegador possui seu próprio armazenamento;
- Os dados não são sincronizados entre dispositivos;
- Limpar os dados do navegador remove as informações salvas.

## Acessibilidade e responsividade

A aplicação foi construída considerando:

- Navegação por teclado;
- Foco visível;
- Botões e campos com rótulos;
- Mensagens de validação;
- Diálogos com retorno de foco;
- Layout adaptado para telas estreitas;
- Uso de texto e controles, sem depender apenas de cores.

## Objetivo do produto

O objetivo da plataforma é transformar tarefas dispersas em um fluxo organizado de trabalho:

> Organizar, planejar, executar e aprender com o que foi realizado.

A solução foi pensada para ser simples, visual e funcional, permitindo que uma pessoa acompanhe suas demandas desde o backlog até o encerramento de uma sprint.

## Escopo

O projeto foi desenvolvido para uso individual.

Não fazem parte do escopo atual:

- Login;
- Equipes;
- Permissões;
- Compartilhamento entre usuários;
- Servidor;
- Banco de dados remoto;
- Integração com o Jira;
- Notificações externas;
- Anexos;
- Relatórios avançados.

## Status do projeto

Projeto concluído com o ciclo principal validado:

```text
Projeto → Backlog → Sprint → Kanban → Encerramento → Histórico
```

Todas as tarefas planejadas foram implementadas e verificadas conforme os critérios definidos no `TASKS.md`.

