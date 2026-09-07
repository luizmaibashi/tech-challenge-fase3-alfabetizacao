# ADR-0012: Hospedagem do painel em GitHub Pages estático

**Data**: 2026-09-07
**Status**: Accepted
**Proposto por**: Luiz Maibashi
**Contexto**: revisão de deploy do portfólio. Aplica a este projeto a política
registrada em `docs/DECISAO_DEPLOY_PORTFOLIO.md` da base de conhecimento
(`Base_de_Conhecimento`).

---

## 🤔 1. CONTEXTO (O QUÊ?)

O `ADR-0010` definiu o painel `reports/painel_intra_uf.html` como entregável de
Deployment do projeto — uma página HTML autocontida, gerada por
`src/visualization/01_gerar_painel_intra_uf.py` a partir de
`reports/ranking_prospectivo_2025.json`.

O painel existia só como arquivo no repositório. Para servir de vitrine (link
em currículo, conversa, avaliação), precisava estar publicado num endereço que
abra na hora.

Diagnóstico, conforme o playbook `metodologia/AI_ENGINEERING/13_deploy_portfolio.md`
da base:

- **Não há app.** O artefato é HTML estático de 261 KB, tema claro/escuro
  próprio, zero dependência externa exceto Google Fonts.
- **Zero computação de servidor.** O JS embutido só filtra e busca sobre o
  payload JSON injetado no build. Nenhuma chamada externa, nenhum formulário
  que grava.

**Balde 1 (snapshot puro)** da política de deploy. GitHub Pages serve o arquivo
direto, sem build, sem CI, sem runtime.

## ✅ 2. DECISÃO (COMO?)

Publicar via **GitHub Pages a partir de `docs/index.html`**.

1. `01_gerar_painel_intra_uf.py` passa a escrever duas cópias idênticas:
   `reports/painel_intra_uf.html` (contrato do ADR-0010, mantido) e
   `docs/index.html` (a página publicada). Mesma string HTML, sem segunda
   renderização — não há como divergirem.
2. `docs/.nojekyll` (vazio): `docs/` também guarda `adr/`, `aprendizado/`,
   `spec/` e `debitos_minerados.md`. Sem o arquivo, o Jekyll do Pages tenta
   processar os Markdown e o build quebra.
3. GitHub → Settings → Pages → Source: branch `main`, pasta `/docs`. URL:
   `https://luizmaibashi.github.io/tech-challenge-fase3-alfabetizacao/`.

Nenhum número é digitado à mão: `docs/index.html` é saída de script e
`git diff` contra `reports/ranking_prospectivo_2025.json` continua sendo a
verificação de que os valores batem com a fonte.

## 📉 3. ALTERNATIVAS DESCARTADAS

| Alternativa | Motivo da rejeição |
|---|---|
| Streamlit Cloud / outro runtime | Sem computação de servidor a justificar. Cold start de dezenas de segundos afasta quem abre o link uma vez. |
| Servir `reports/painel_intra_uf.html` direto pelo Pages | O Pages publica de `/`, `/docs` ou de um branch dedicado, não de `/reports`. `/docs` é a convenção da política da base. |
| Branch `gh-pages` com CI | Nenhum build a rodar. `main` + `/docs` é mais simples e não some se a Action falhar. |

## 📈 4. IMPACTO E VALIDAÇÃO

**Positivo:** link de portfólio abre instantâneo, sem cold start; zero
dependência de runtime; arquivo versionado, auditável por `git diff` contra o
snapshot.

**Negativo:** atualizar o site exige rodar o gerador e commitar `docs/index.html`
(um passo além de `git push`). O dado do painel é um backtest encerrado
(ciclo 2024→2025) — estático por natureza, não há atualização periódica a
manter.

**Validação:** `diff` dos primeiros bytes de `reports/painel_intra_uf.html` e
`docs/index.html` confirmou cópias idênticas na primeira geração
(2026-09-07). Conferência visual da página publicada fica pendente da
habilitação do Pages pelo Luiz.

## 🔗 Referências

- `docs/spec/deploy-pages.md` — handoff da migração
- `docs/DECISAO_DEPLOY_PORTFOLIO.md` (base) — política, os 3 baldes
- `metodologia/AI_ENGINEERING/13_deploy_portfolio.md` (base) — playbook
- `ADR-0010` — o painel como entregável e seu contrato de uso condicional
- `PROJETOS/02_PORTFOLIO/payflow_inadimplencia/docs/adr/0023-*` — o ADR de outro projeto que originou o padrão
