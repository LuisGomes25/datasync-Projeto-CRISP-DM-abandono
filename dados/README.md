# Dados

`tabela_analitica.csv`: base analítica gerada pelo notebook 01. Uma linha por escola × etapa (136.713 linhas, 96.231 escolas públicas, 27 colunas).

- Chave: `codigo_escola` + `etapa` (`anos_iniciais`, `anos_finais`, `ensino_medio`).
- `taxa_abandono`: taxa de abandono da etapa (Indicadores Educacionais 2025).
- `alvo_alto_abandono`: rótulo de referência (≥ P80 da etapa; > 0 nos anos iniciais). Os notebooks 03 e 04 recalculam o alvo a partir de `taxa_abandono`.
- `tnr` e `matriculas` ficam fora do modelo (usa-se `log_matriculas`).
- `CO_MUNICIPIO` é usado só para agrupar a validação cruzada.
