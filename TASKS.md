# Tarefas — gerenciador individual

Planejamento baseado em [SPEC.md](SPEC.md). Todas as tarefas de implementação começam pendentes. A numeração indica a ordem sugerida, não autorização para executar automaticamente.

## Processo

- Ler `SPEC.md` e confirmar as regras propostas antes da implementação afetada.
- Executar apenas a tarefa escolhida pelo usuário e respeitar suas dependências.
- Cada tarefa inclui implementar, verificar seus critérios, marcar apenas seu checkbox e registrar um commit exclusivo.
- Usar `git add -A` e `git commit -m "tarefa N: <descrição curta>"`; depois parar.
- Todo código e eventuais dados de demonstração ficam em `index.html`. Não criar testes ou outros arquivos adicionais; registrar a verificação na própria tarefa.
- Para cada conclusão, acrescentar abaixo da tarefa a verificação realizada e suas limitações. Não marcar como concluída se os critérios não forem atendidos.

## Fundação

- [x] **Tarefa 1 — Criar estrutura visual e navegação**
  - Capacidades: CAP-9. Dependências: nenhuma.
  - Criar `index.html` com CSS e JS internos, menu de projetos, navegação Backlog/Quadro/Sprints e área de conteúdo.
  - Aceite: abrir no navegador sem erro; alternar as três telas; indicar a tela selecionada; exibir estados vazios em português; foco visível e estrutura semântica.
  - Verificação: abrir localmente, navegar com Tab e Enter e testar largura de 360 px.
  - Verificação realizada: sintaxe JavaScript válida e revisão independente do código sem defeitos bloqueantes. Usuário validou a entrega e autorizou continuar (“me parece bom. pode continuar”). Limitação: não houve verificação automatizada em navegador de Tab/Enter e largura de 360 px, pois nenhum navegador estava disponível na sessão; a validação do usuário não detalhou esses testes.

- [x] **Tarefa 2 — Implementar estado e persistência local**
  - Capacidades: CAP-8. Dependências: 1. Decisão prévia: persistência proposta.
  - Definir estruturas de projetos, tarefas e sprints, IDs estáveis, versão de dados e funções de leitura/gravação.
  - Aceite: estado válido sobrevive à recarga; armazenamento vazio inicializa sem erro; dados inválidos e falhas de gravação geram mensagem e não sobrescrevem silenciosamente o conteúdo anterior.
  - Verificação: usar o console para salvar e recuperar estado de exemplo, simular JSON inválido e falha de gravação; restaurar o estado de teste ao terminar.
  - Verificação realizada: JavaScript executado com Node/VM e armazenamento isolado em memória; carga vazia, recarga com projetos/tarefas/sprints, 1.000 IDs distintos, versão inválida, JSON corrompido, falhas de leitura/gravação e mudança externa passaram. Nenhum dado real foi alterado. Revisão independente sem defeitos bloqueantes; operações futuras devem salvar cópias do estado. Objetos programáticos com toJSON personalizado estão fora do fluxo implementado. Limitação: navegador integrado indisponível; localStorage real e apresentação do alerta não foram testados visualmente.

- [x] **Tarefa 3 — Criar e selecionar projetos**
  - Capacidades: CAP-1, CAP-8. Dependências: 2. Regras: R1.
  - Criar formulário para nome do projeto, edição do nome e seleção persistente.
  - Aceite: nome vazio ou apenas espaços é rejeitado; projetos têm IDs distintos; renomear preserva ID; recarregar mantém projetos e seleção; ausência de projetos mostra ação para criar o primeiro.
  - Verificação: criar dois projetos, renomear um e alternar seleção antes e depois de recarregar.
  - Verificação realizada: Node/VM com DOM e armazenamento simulados validou criação de dois projetos com IDs distintos, rejeição de nome vazio/espaços, renomeação preservando ID, nome semelhante a HTML tratado como texto, seleção após duas recargas, cancelamento e retorno de foco, falha de gravação preservando texto/estado e restauração da seleção anterior. Sintaxe JavaScript e git diff --check aprovados. Revisão independente sem defeitos bloqueantes; trocar de projeto fecha o rascunho aberto, comportamento sem exigência de confirmação no escopo atual. Limitação: navegador integrado indisponível; renderização, teclado real e responsividade não foram verificados visualmente.

## Tarefas e backlog

- [x] **Tarefa 4 — Criar tarefas no backlog**
  - Capacidades: CAP-2, CAP-3, CAP-8. Dependências: 3. Regras: R2, R3.
  - Criar formulário com título, descrição, prioridade e prazo opcional; gerar identificador visível estável.
  - Aceite: título vazio é rejeitado; tarefa é criada no projeto selecionado, inicia em A fazer e permanece sem sprint no backlog; valores persistem; textos com marcação são exibidos literalmente; não é possível criar sem projeto.
  - Verificação: criar tarefas com campos mínimos e completos, tentar título vazio e inserir texto semelhante a HTML.
  - Verificação realizada: revisão do código confirma rejeição de título vazio/espaços, criação apenas com projeto selecionado, estado inicial A fazer, `sprintId` nulo, IDs visíveis `T-` estáveis, persistência via `saveState`/`copyState` e exibição com `textContent`. `node` parseou o script sem erro de sintaxe. Limitação: o navegador integrado e o MCP de browser não estavam disponíveis nesta sessão; o fluxo visual de formulário, recarga e texto semelhante a HTML não foi exercido na interface.

- [x] **Tarefa 5 — Consultar e editar tarefas**
  - Capacidades: CAP-2, CAP-8. Dependências: 4. Regras: R3, R6.
  - Abrir detalhes e editar os campos permitidos da tarefa, com ações Salvar e Cancelar.
  - Aceite: edição mantém ID e projeto; ID, projeto e vínculos com sprint não são alterados pela edição; cancelar preserva dados; validações da criação continuam válidas; alterações aparecem na lista e sobrevivem à recarga.
  - Verificação: editar cada campo, cancelar outra edição e comparar os dados após recarregar.
  - Verificação realizada: o formulário reutilizado mostra ID, projeto e vínculo de sprint só como texto; Salvar copia título, descrição, prioridade e prazo sem mudar `id`, `projectId`, `sprintId`, `status` nem `order`; Cancelar fecha sem `saveState`; título vazio continua rejeitado. Tarefas concluídas de sprint encerrada não abrem edição (R6). Limitação: navegador integrado indisponível; persistência após recarga e o cancelamento visual não foram exercidos na interface.

- [x] **Tarefa 6 — Excluir tarefas com confirmação**
  - Capacidades: CAP-2, CAP-8. Dependências: 5. Regras: R6.
  - Permitir exclusão identificando a tarefa na confirmação; centralizar a remoção para não deixar referências inválidas.
  - Aceite: cancelar não altera o estado; confirmar remove somente a tarefa indicada; contagens e listas se atualizam; exclusão persiste.
  - Verificação: cancelar e confirmar exclusões em um projeto com várias tarefas.
  - Verificação realizada: a ação Excluir identifica a tarefa por ID e título em `window.confirm`; cancelamento não chama `saveState`; confirmação remove apenas o ID indicado pelo `deleteTask`, atualiza a lista e persiste a alteração; falhas de gravação preservam o estado anterior. Sintaxe JavaScript e `git diff --check` aprovados. Limitação: navegador integrado indisponível; confirmação, foco e persistência após recarga não foram exercidos visualmente.

- [x] **Tarefa 7 — Ordenar o backlog manualmente**
  - Capacidades: CAP-3, CAP-9. Dependências: 4. Regras: R2, R7.
  - Adicionar ações acessíveis para subir e descer tarefas, persistindo sua ordem por projeto.
  - Aceite: a ordem sobrevive à recarga e à troca de projeto; controles nos extremos não produzem movimentos inválidos; nenhuma tarefa é perdida ou duplicada.
  - Verificação: reordenar três tarefas por teclado e repetir com lista vazia e com apenas uma tarefa.
  - Verificação realizada: cada cartão recebeu controles Subir/Descer com rótulos acessíveis, os extremos são desabilitados e `reorderTask` troca apenas as posições das tarefas do backlog do projeto selecionado, normalizando sua ordem antes de salvar. Sintaxe JavaScript, presença dos controles e `git diff --check` aprovados. Limitação: navegador integrado indisponível; teclado real, recarga, troca de projeto e os cenários vazio/uma tarefa não foram exercidos visualmente.

## Planejamento de sprints

- [ ] **Tarefa 8 — Criar e editar sprints planejadas**
  - Capacidades: CAP-4, CAP-8. Dependências: 3. Regras: R4, R6.
  - Criar lista e formulário de sprint com nome, objetivo e datas, associada ao projeto atual.
  - Aceite: rejeitar nome vazio e período inválido; editar sprint planejada preserva seu ID; datas não mudam por conversão de fuso; sprints persistem e ficam isoladas por projeto.
  - Verificação: criar e editar sprints em dois projetos; testar fim anterior ao início e datas iguais.

- [ ] **Tarefa 9 — Distribuir tarefas entre backlog e sprints**
  - Capacidades: CAP-3, CAP-4. Dependências: 7, 8. Regras: R2, R6.
  - Adicionar controles para associar tarefas a sprints planejadas e devolvê-las ao fim do backlog.
  - Aceite: uma tarefa não aparece simultaneamente no backlog e na sprint; transferência atualiza ambas as listas e persiste; não aceita sprint de outro projeto ou encerrada.
  - Verificação: associar, transferir entre sprints planejadas e retirar tarefas; recarregar e conferir os vínculos.

- [ ] **Tarefa 10 — Iniciar uma sprint**
  - Capacidades: CAP-6. Dependências: 9. Regras: R1, R4.
  - Implementar transição Planejada → Ativa e indicar a sprint ativa do projeto.
  - Aceite: impedir segunda sprint ativa no mesmo projeto; permitir sprint ativa independente em outro projeto; início persiste e disponibiliza as tarefas para o quadro.
  - Verificação: iniciar sprint, tentar iniciar outra no mesmo projeto e repetir em projeto diferente.

## Execução e encerramento

- [ ] **Tarefa 11 — Exibir o quadro Kanban da sprint ativa**
  - Capacidades: CAP-5, CAP-9. Dependências: 5, 10. Regras: R2, R3.
  - Exibir colunas A fazer, Em andamento e Concluído com cartões, contagens e acesso aos detalhes.
  - Aceite: mostrar apenas tarefas da sprint ativa do projeto; cartões exibem ID, título, prioridade e prazo quando houver; ausência de sprint ativa orienta o usuário; colunas vazias têm mensagem apropriada.
  - Verificação: comparar quadro e sprint em dois projetos e conferir comportamento em tela estreita.

- [ ] **Tarefa 12 — Mover tarefas entre estados**
  - Capacidades: CAP-5, CAP-8, CAP-9. Dependências: 11.
  - Oferecer controle de estado acessível em cada tarefa do quadro, usando uma única operação de atualização do estado.
  - Aceite: mover entre quaisquer das três colunas atualiza contagens e detalhes sem duplicar cartões; mudança persiste; operação funciona por teclado e mantém foco utilizável.
  - Verificação: percorrer todos os estados e retornar ao inicial; recarregar; editar e excluir tarefa da sprint ativa para conferir sincronização.

- [ ] **Tarefa 13 — Encerrar sprint e consultar histórico**
  - Capacidades: CAP-3, CAP-6, CAP-8. Dependências: 6, 12. Regras: R5, R6.
  - Exibir resumo e confirmação do encerramento; arquivar resultado e tratar pendências conforme R5.
  - Aceite: cancelar não altera dados; confirmar encerra a sprint, mantém concluídas e devolve pendentes ao backlog sem perder estado; histórico preserva o resumo mesmo que pendências sejam editadas ou excluídas posteriormente; impede alterações de sprint encerrada e suas tarefas concluídas.
  - Verificação: encerrar sprint vazia, totalmente concluída e mista; recarregar; conferir histórico após editar uma pendência e iniciar nova sprint.

## Busca e acabamento

- [ ] **Tarefa 14 — Buscar e filtrar tarefas**
  - Capacidades: CAP-7. Dependências: 13.
  - Implementar busca por título/ID e filtros combinados de prioridade e estado nas listas de tarefas e no quadro.
  - Aceite: busca ignora diferenças entre maiúsculas e minúsculas; filtros respeitam projeto e visão; limpar restaura a lista; distinguir ausência de dados de ausência de resultados; reordenação do backlog fica desabilitada enquanto houver filtro para evitar ordem ambígua.
  - Verificação: combinar busca e filtros, limpar, trocar projeto e conferir que nenhum resultado pertence a outro contexto.

- [ ] **Tarefa 15 — Revisar responsividade e acessibilidade dos fluxos**
  - Capacidades: CAP-9. Dependências: 14.
  - Ajustar formulários, cartões, navegação, feedback e eventuais diálogos em todos os fluxos implementados.
  - Aceite: todas as ações principais funcionam por teclado; campos têm rótulos; erros são associados aos campos; diálogos devolvem foco ao fechar; cores não são o único indicador de estado; conteúdo não se sobrepõe em 360 px nem com zoom de 200%.
  - Verificação: percorrer criação de tarefa e mudança de estado sem mouse; testar telas estreita e desktop, zoom e mensagens de erro.

- [ ] **Tarefa 16 — Validar o ciclo completo e corrigir falhas de integração**
  - Capacidades: CAP-1 a CAP-9. Dependências: 15.
  - Executar o sinal de sucesso da especificação, corrigindo somente defeitos necessários para os critérios já definidos.
  - Aceite: completar projeto → backlog → sprint → Kanban → encerramento → histórico → nova sprint; dados corretos após recarga; nenhuma referência órfã; falhas de armazenamento não causam perda silenciosa; console sem erros no percurso.
  - Verificação: executar o fluxo com dois projetos, tarefas concluídas e pendentes; repetir carga vazia, dados inválidos e falha de gravação; registrar aqui navegador, resultado e limitações observadas.

## Conferência do planejamento

- Todas as nove capacidades estão vinculadas a tarefas com critérios verificáveis.
- Dependências apontam somente para tarefas anteriores; tarefas 1, 2 e 3 concluídas. Tarefas 4–16 permanecem pendentes.
- Persistência com localStorage e R1 confirmadas pelo usuário em 18/09/2026. As demais regras propostas aguardam confirmação antes das tarefas afetadas.
