# Roteiro — Vídeo Executivo (até 5min)

> Formato: simula reunião executiva com gestor público. Fala em primeira
> pessoa, tom direto, sem jargão de ML não traduzido. Cada bloco tem o texto
> de apoio (não decoreba, guia) e o que mostrar na tela.

## Bloco 1 — O problema (0:00–0:40)

**Fala:**
> "Alfabetização até o 2º ano é meta nacional do PDE. Hoje o gestor sabe qual
> *município* está em risco — a Fase 2 deste projeto já resolveu isso. A
> pergunta que ficou foi: dá pra saber qual *aluno*, dentro da escola,
> precisa de intervenção agora?"

**Tela:** slide com a pergunta, ou o cabeçalho do README.

## Bloco 2 — O que foi testado, e o resultado negativo (0:40–1:50)

**Fala:**
> "Construímos o modelo que o desafio pediu: prever aluno por aluno. Rigor
> total — vazamento de dado removido, três algoritmos testados, validação
> temporal. E ele **perdeu** para a coisa mais simples possível: pegar a
> meta que o município já tem e aplicar pra todos os alunos dele. Perdeu
> com significância estatística, não por pouco.
>
> Por quê? Porque essa base nunca observou o aluno individualmente — ela
> observa o município, e empresta esse dado pra cada aluno dele. Não é
> falha de algoritmo, é o que o dado disponível permite enxergar."

**Tela:** tabela §7.2 (referência aleatória / baseline fraco / modelo / baseline forte) — a que mostra o modelo perdendo.

**Por que esse bloco existe:** o enunciado avalia "interpretação dos
resultados" e "limitações" — declarar um resultado negativo com dado é
mais forte, não mais fraco, do que esconder atrás de uma métrica boa
isolada. É a tese central do projeto (ver README, resumo de 30s).

## Bloco 3 — O que funciona: priorização entre municípios (1:50–3:00)

**Fala:**
> "Quando o modelo de aluno não passou, testamos um nível acima: dá pra
> prever quais *municípios* vão furar a meta no próximo ciclo? Aí sim havia
> sinal — mas só quando a comparação é *dentro do mesmo estado*, nunca
> entre estados, porque cada estado aplica sua própria prova.
>
> Testamos isso de verdade: treinamos com 2023 e 2024, e comparamos contra
> o resultado real de 2025, que na época do treino ainda não existia. O
> modelo venceu a regra simples em 14 estados, perdeu num, e em 8 o dado
> honesto diz 'não dá pra saber ainda' — e o produto respeita isso."

**Tela:** tabela do entregável 3 (AUC 0,6167 vs 0,4523) ou o painel ao vivo.

## Bloco 4 — Demonstração do painel (3:00–4:00)

**Fala:**
> "Isso virou uma ferramenta." *(abrir o link do GitHub Pages)* "O gestor
> escolhe o estado dele. Aqui" *(UF vencedora)* "ele vê o ranking do
> modelo. Aqui" *(CE)* "o painel recomenda a regra simples, porque foi o
> que funcionou melhor nesse estado. E aqui" *(UF inconclusiva)* "ele vê só
> diagnóstico — a ferramenta se recusa a sugerir uma ordem de ação onde o
> dado não sustenta isso."

**Tela:** captura de tela ao vivo do painel, trocando de estado 2-3 vezes pra mostrar os 3 modos.

## Bloco 5 — Valor estratégico e recomendação (4:00–4:40)

**Fala:**
> "Duas recomendações, as duas com número e intervalo de confiança atrás:
>
> Primeiro, pra busca ativa de aluno, usar a meta que o município já tem —
> é mais simples, mais barato, e estatisticamente melhor que qualquer
> modelo que testamos.
>
> Segundo, pra priorizar entre municípios, comparar só dentro do mesmo
> estado, e usar esse painel — que já sabe onde ajuda e onde não ajuda."

**Tela:** as duas recomendações do §10, ou tela dividida com o painel.

## Bloco 6 — Fechamento (4:40–5:00)

**Fala:**
> "O valor aqui não foi construir o modelo mais sofisticado. Foi definir o
> critério de sucesso antes de treinar, testar com rigor, e quando o
> resultado não veio como esperado, confiar no dado, não no modelo — e
> achar, no caminho, onde a inteligência de dado realmente ajuda."

---

## Checklist de gravação

- [ ] Cronometrar cada bloco lendo em voz alta antes de gravar (meta: 4:30–5:00 total)
- [ ] Testar o link do GitHub Pages ao vivo antes de gravar (conexão, zoom da página)
- [ ] Ter as 2-3 UFs de exemplo já escolhidas (uma vencedora, CE, uma inconclusiva) pra não procurar ao vivo
- [ ] Gravar tela + voz junto, ou narrar por cima depois — decidir antes, muda o roteiro de fala
- [ ] Revisar se o tom soa "reunião com gestor público", não "aula de ML" — cortar qualquer termo técnico não traduzido (ROC-AUC, IC95%, etc. não aparecem na fala, só na tela)
