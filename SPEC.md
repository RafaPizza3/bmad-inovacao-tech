---
id: SPEC-gerenciador-de-tarefas
companions: []
sources: []
---

# Gerenciador individual de tarefas

Status: tarefas 1–3 autorizadas; persistência com localStorage e regra R1 confirmadas pelo usuário em 18/09/2026. As demais regras aguardam confirmação antes das tarefas afetadas.

## Por quê

Organizar o trabalho de uma pessoa em uma aplicação inspirada no Jira, com backlog para preparar demandas, sprints para escolher um conjunto de trabalho e Kanban para acompanhar a execução.

## Capacidades

| ID | Intenção | Critério de sucesso |
| --- | --- | --- |
| CAP-1 | Organizar tarefas por projeto. | Criar, editar e selecionar projetos; cada visão mostra apenas dados do projeto selecionado. |
| CAP-2 | Registrar e manter tarefas. | Criar, consultar, editar e excluir uma tarefa com título, descrição, prioridade e prazo opcional; alterações aparecem nas visões correspondentes. |
| CAP-3 | Preparar trabalho no backlog. | Consultar tarefas sem sprint, priorizá-las e associá-las a uma sprint planejada. |
| CAP-4 | Planejar sprints. | Criar e editar nome, objetivo e período de uma sprint; adicionar e retirar tarefas antes de iniciá-la. |
| CAP-5 | Acompanhar execução no Kanban. | Visualizar tarefas da sprint ativa em A fazer, Em andamento e Concluído, e mudar seu estado. |
| CAP-6 | Iniciar e encerrar sprints. | Iniciar uma sprint planejada e concluir seu ciclo sem perder tarefas; consultar o resultado de sprints encerradas. |
| CAP-7 | Encontrar tarefas. | Buscar por título ou identificador e filtrar por prioridade e estado, podendo limpar todos os filtros. |
| CAP-8 | Manter os dados entre sessões. | Recarregar a aplicação e recuperar projetos, tarefas, sprints e seus vínculos salvos no navegador. |
| CAP-9 | Usar a interface em diferentes telas e por teclado. | Navegar, preencher formulários e mudar o estado de uma tarefa sem mouse; usar as funções principais em tela de 360 px e desktop. |

## Restrições

- Sistema individual, sem login ou compartilhamento entre pessoas.
- Implementação integral em um único `index.html`, com HTML, CSS e JavaScript nativos; sem framework, npm ou arquivos adicionais de implementação.
- Interface e mensagens em português.
- `SPEC.md` e `TASKS.md` são as únicas exceções autorizadas para novos documentos. O formato BMAD foi adaptado a essa restrição, sem arquivos auxiliares de memória ou histórias.
- Ler esta especificação antes de codificar. Executar somente a tarefa solicitada, marcar sua conclusão em `TASKS.md`, executar `git add -A` e criar um commit exclusivo `tarefa N: <descrição curta>`; então parar.
- Texto informado pelo usuário deve ser exibido como texto, sem executar HTML ou JavaScript.
- Falhas de leitura ou gravação não podem apagar silenciosamente dados existentes nem informar salvamento bem-sucedido.
- Persistência local não implica sincronização entre dispositivos ou recuperação após limpar os dados do navegador.

## Fora do escopo

- Contas, equipes, permissões, servidor, banco remoto e colaboração simultânea.
- Integração com Jira, reprodução integral do Jira, anexos, notificações externas e automações.
- Relatórios avançados, estimativas por pontos e workflows configuráveis nesta versão.

## Sinal de sucesso

Uma pessoa cria um projeto e tarefas, organiza o backlog, planeja e inicia uma sprint, movimenta tarefas no quadro, encerra a sprint e consulta seu resultado. Após recarregar, os dados e vínculos permanecem corretos. O fluxo funciona por teclado e em tela estreita.

## Decisões técnicas propostas e justificativas

- Usar `localStorage` com versão do formato: atende à persistência individual sem servidor. Validar a estrutura ao carregar e tratar indisponibilidade ou limite de armazenamento.
- Separar estado, persistência, operações e renderização em funções no mesmo HTML: permite evoluir uma tarefa de cada vez sem duplicar regras entre as telas.
- Usar identificadores estáveis e referências entre entidades: evita perder vínculos ao editar nomes ou títulos.
- Usar controles explícitos para mudar estado e associação de sprint: torna o fluxo utilizável por teclado; arrastar cartões não é requisito desta versão.
- Não incluir campo de responsável inicialmente: o único usuário executa o próprio trabalho.

## Regras de produto propostas — confirmar antes das tarefas afetadas

- R1: permitir vários projetos e no máximo uma sprint ativa por projeto.
- R2: manter tarefas sem sprint no backlog; cada tarefa pertence a um projeto e a no máximo uma sprint. O quadro mostra a sprint ativa do projeto.
- R3: iniciar tarefas em A fazer; oferecer prioridades Baixa, Média e Alta, com Média inicialmente. Título é obrigatório; descrição e prazo são opcionais.
- R4: exigir nome e datas válidas na sprint, com fim igual ou posterior ao início; objetivo é opcional. Permitir iniciar sprint vazia, sem transições automáticas por data.
- R5: ao encerrar uma sprint, manter tarefas concluídas nela e devolver as pendentes ao backlog, preservando seu estado. Registrar um resumo do encerramento com identificadores, títulos e estados daquele momento para preservar o histórico.
- R6: permitir excluir tarefas mediante confirmação; não oferecer exclusão de projetos ou sprints nesta versão. Bloquear edição de sprints encerradas e de suas tarefas concluídas para preservar o resultado.

## Questões abertas

- As regras R1–R6 e as decisões técnicas propostas atendem à primeira versão? Ajustar os documentos antes de implementar qualquer ponto não aprovado.

## Registro do planejamento

- Confirmado em 18/09/2026: salvar neste navegador com localStorage e permitir vários projetos, com no máximo uma sprint ativa por projeto. Implementar as tarefas 2 e 3 em commits separados, preservando a tarefa 1 já concluída.
- Implementação das tarefas 2–3: estado versionado e validado, IDs estáveis, gravação antes de atualizar o estado em memória e mensagens de erro em português; formulário de criação/renomeação e seleção persistente em `index.html`. Verificação sem criar arquivos auxiliares.

- Pedido: gerenciador no estilo Jira, com HTML, CSS e JavaScript; criar todas as tarefas e orientar pelo BMAD.
- Confirmado pelo usuário: uso individual, backlog e sprints na primeira versão, criação de `SPEC.md` e `TASKS.md`.
- Adaptação de processo: lista de tarefas em `TASKS.md`, sem `stories.yaml` ou `.memlog.md`, respeitando a limitação de arquivos.
- Verificação de coerência: nove capacidades com intenção e sucesso verificáveis; regras ainda não confirmadas identificadas explicitamente.
- Verificação de preservação: tecnologia, uso individual, Kanban, backlog, sprints e execução de uma tarefa por commit contemplados. Nenhuma implementação foi realizada nesta etapa.
