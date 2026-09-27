---
name: bmad-build
description: 'Implementa funcionalidades, tarefas e correções com planejamento, verificação e revisão do próprio diff. Use para mudanças de implementação delegadas pelo usuário ou pedidos explícitos de BMad Build. Não use para simples ajustes mecânicos ou operações que apenas registram trabalho existente.'
---

# BMad Build — adaptação local

Esta é uma adaptação autônoma para este projeto, autorizada pelo usuário. Execute o fluxo abaixo diretamente. Não depende de uv, setup, renderizador, snapshots ou diretório _bmad. Atualizações do pacote original podem sobrescrever esta adaptação.

Os arquivos workflow.md e step-*.md distribuídos nesta pasta são templates do fluxo original e não fazem parte desta adaptação. Não os execute nem tente resolver seus placeholders. Outras skills instaladas mantêm suas próprias dependências; esta alteração não as converte automaticamente.

## Contexto e escopo

1. Leia AGENTS.md, SPEC.md e as tarefas solicitadas em TASKS.md na raiz do projeto. Verifique o estado do Git e preserve mudanças anteriores do usuário.
2. Identifique critérios de aceite, dependências e regras aplicáveis. Use decisões já autorizadas na conversa. Pergunte somente sobre ambiguidades relevantes ainda não resolvidas.
3. Explique em português as decisões e o plano proporcional à tarefa. Use os documentos existentes; não crie histórias, logs, planos ou artefatos auxiliares obrigatórios.

## Implementação e verificação

4. Implemente somente o escopo autorizado. Neste projeto, código HTML, CSS e JavaScript ficam em index.html, sem framework ou npm. A autorização para adicionar skills não autoriza novos arquivos de aplicação.
5. Trabalhe em uma tarefa por vez. Se o usuário pediu várias tarefas, conclua e registre cada uma antes de iniciar a seguinte; pare após a última solicitada.
6. Verifique os critérios de aceite com as ferramentas disponíveis. Para fluxos de interface, prefira executar no navegador; verificação estática não substitui teclado, foco, responsividade ou persistência real. Não declare testes que não executou e não crie arquivos de teste neste projeto.
7. Revise o próprio diff buscando regressões, perda de dados, acessibilidade e desvios do escopo. Corrija defeitos necessários à tarefa e repita apenas as verificações afetadas. Revisões com outras skills ou agentes não são requisito desta adaptação.

## Conclusão

8. Marque somente a tarefa concluída com [x] no TASKS.md, registrando a verificação realizada e suas limitações. Se os critérios não forem atendidos, mantenha a tarefa pendente e explique o bloqueio.
9. Inspecione o diff antes de registrar. Para cada tarefa de implementação concluída, execute git add -A e git commit -m "tarefa N: <descrição curta>", conforme AGENTS.md. Não misture duas tarefas em um commit. Se houver alterações anteriores de terceiros, não as inclua silenciosamente.
10. Informe o resultado, a verificação, as limitações e o commit. Não inicie tarefas fora do pedido.
