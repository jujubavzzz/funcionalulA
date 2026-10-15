# Avaliação: GitHub Actions com IA

> Preencha este documento com links e resultados reais depois de executar os testes. Não invente links, logs ou resultados.

## Tarefa 1 — CI
- Execução verde: [cole o link real]
- Execução vermelha: [cole o link real]
- Erro observado no log: [copie a mensagem real]
- Por que testar migrações em SQLite: detectar erros antes de aplicar no D1 remoto.

## Tarefa 2 — Proteção da main
- PR bloqueado: [cole o link real]
- PR liberado: [cole o link real]
- Push direto recusado: [cole a saída/evidência real]

## Tarefa 3 — Revisão por IA
- PR com comentários da IA: [cole o link real]
- Erro de permissão: [cole o link/log real]
- Crítica à IA: [afirmação real observada + justificativa técnica]

## Tarefa 4 — Migrações D1
- Execução após merge: [cole o link real]
- Saída de `PRAGMA table_info(notas)`: [cole a saída real]
- Merge sem mudança em `migrations/`: [cole a evidência real]

## Perguntas finais

1. **Por que `ci.yml` roda duas vezes com `push` numa ramificação que tem PR aberto? Qual execução conta?**  
   O workflow tem dois gatilhos: `push` executa quando o commit é enviado à ramificação, e `pull_request` executa quando o PR é aberto ou atualizado. São eventos distintos e podem gerar duas execuções. Para proteger a `main`, confira no próprio PR qual status check está configurado como obrigatório.

2. **Por que um PR vindo de fork não pode usar `secrets.COPILOT_PAT`? Qual ataque isso impede?**  
   Por padrão, workflows disparados por `pull_request` de um fork não recebem os segredos do repositório de destino. Isso reduz o risco de código não confiável usar um token privilegiado para roubar credenciais ou agir em nome do mantenedor.

3. **Por que declarar `permissions` em vez de usar as permissões padrão do `GITHUB_TOKEN`?**  
   Permissões explícitas aplicam o princípio do menor privilégio: o workflow recebe somente os acessos necessários, reduzindo o impacto de uma etapa ou dependência comprometida.

4. **A revisão da IA pode substituir o status check da Tarefa 2?**  
   Não. A IA pode errar ou deixar de identificar problemas. O status check do CI é uma verificação automatizada exigida pela regra da `main`; a revisão da IA é complementar.
