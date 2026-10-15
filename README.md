# Avaliação — GitHub Actions com IA

Este pacote contém modelos iniciais de workflows e um modelo de relatório.

## Estrutura

- `.github/workflows/ci.yml`: procura alguns padrões de possíveis segredos, testa migrações SQL em SQLite e valida arquivos HTML.
- `.github/workflows/revisao-ia.yml`: modelo de revisão de Pull Request com IA.
- `.github/workflows/migrar.yml`: aplica migrações ao D1 remoto quando arquivos de `migrations/` mudam na `main`.
- `AVALIACAO.md`: relatório para preencher com evidências reais.

## Antes de enviar ao GitHub

1. Confira se o projeto já tem `migrations/` com arquivos `.sql` reais. O pacote não cria migrações de exemplo porque elas precisam corresponder ao esquema do seu projeto.
2. Confira se existe `wrangler.toml` e se ele contém a configuração correta do D1.
3. No workflow `migrar.yml`, substitua `NOME_DO_BANCO` pelo nome real do banco D1.
4. No GitHub, abra **Settings → Secrets and variables → Actions** e cadastre:
   - `COPILOT_PAT`
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID`
5. Nunca coloque os valores dos tokens nos arquivos, commits ou logs.
6. Confira a documentação atual da action `actions/ai-inference@v1`: os inputs e outputs podem variar. O workflow de revisão está baseado no modelo da resolução e pode exigir ajustes antes de funcionar.
7. Confirme que a conta/plano tem acesso à integração de IA usada pela avaliação e que o token tem as permissões exigidas.
8. Faça commit e abra **Actions** para conferir os resultados.

## Observações

- A verificação de segredos do `ci.yml` procura apenas alguns padrões; ela não detecta todos os tipos de credenciais.
- A validação em SQLite ajuda a encontrar alguns erros, mas não garante compatibilidade completa com D1.
- Teste migrações em ambiente apropriado antes de aplicá-las ao banco remoto.
- Os links, logs e resultados do relatório devem ser preenchidos somente depois de executar os testes reais.
