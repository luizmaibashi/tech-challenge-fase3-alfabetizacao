# Spec: deploy do painel em GitHub Pages

**Contexto:** `docs/DECISAO_DEPLOY_PORTFOLIO.md` da base (`Base_de_Conhecimento`).
**Balde:** 1 — snapshot puro.
**Estado:** executado em 2026-09-07 (sessão da decisão). Falta só o Luiz habilitar o Pages.

## Diagnóstico (2026-09-07)

- Entrypoint: **não há app**. O artefato público é `reports/painel_intra_uf.html`,
  gerado por `src/visualization/01_gerar_painel_intra_uf.py` a partir de
  `reports/ranking_prospectivo_2025.json` (saída do backtest prospectivo).
- O HTML é **autocontido**: 261 KB, tema claro/escuro próprio (três estados),
  zero dependência externa exceto Google Fonts. JS só faz filtro/busca client-side
  sobre o payload embutido. Nenhum compute, nenhuma chamada externa, nenhum form
  que grava.
- Não estava hospedado em lugar nenhum — só existia como arquivo no repo.

Balde 1 inequívoco. A receita se aplica direta, e o artefato já existe.

## O que foi feito

1. `src/visualization/01_gerar_painel_intra_uf.py` — segunda saída: além de
   `reports/painel_intra_uf.html`, escreve `docs/index.html` (mesmo conteúdo).
2. `docs/index.html` — gerado.
3. `docs/.nojekyll` — vazio (`docs/` guarda `adr/`, `aprendizado/`,
   `debitos_minerados.md` — Jekyll processaria os `.md` e quebraria o build).
4. `README.md` — seção "Deploy" com a URL.
5. `docs/adr/0012-hospedagem-do-painel-em-github-pages.md` — ADR da decisão.

## O que o Luiz faz

GitHub → repo `tech-challenge-fase3-alfabetizacao` → Settings → Pages →
Source: branch `main`, pasta `/docs`. URL fica
`https://luizmaibashi.github.io/tech-challenge-fase3-alfabetizacao/`.

## Não muda

- `reports/painel_intra_uf.html` continua sendo gerado (o ADR-0010 do projeto
  referencia esse caminho como contrato).
- O gerador continua a fonte única; `docs/index.html` nunca é editado à mão.

## Passe visual (pendente, sessão futura)

O painel usa `--primary:#0F5C58` — teal-green, quase idêntico ao `payflow`, ao
`caderno-portfolio` e ao domínio. Candidato a trocar de paleta via
`ui-ux-pro-max --design-system` calibrado para governo/educação/dado público.
Fora do escopo da migração de deploy; decisão do Luiz.
