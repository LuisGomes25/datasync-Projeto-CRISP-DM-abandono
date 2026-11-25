# DATASYNC · Identificação de escolas públicas com alto abandono escolar

Projeto final da disciplina **Data Project: Modeling & Implementation** (Faculdade Impacta de Tecnologia), professor Gilberto Alves Pereira. Metodologia **CRISP-DM**.

**Objetivo:** identificar escolas públicas com maior probabilidade de registrar taxas altas de abandono e caracterizar seus perfis de vulnerabilidade, para apoiar a priorização de ações de permanência por secretarias de educação.

> O modelo é **associativo**: taxas e características das escolas são do mesmo período (Censo Escolar e Indicadores 2025, INSE 2023). Ele aponta escolas com perfil associado ao alto abandono; não prevê o ano seguinte nem indica causas. As conclusões valem para escolas, não para estudantes, e não se destinam a rankings punitivos.

## Principais resultados

| Etapa | Modelo | PR-AUC | Precisão nos 10% de maior risco | Vezes o acaso |
|---|---|---|---|---|
| Ensino médio | Random Forest | ~0,52 | ~0,59 | ~3,0× |
| Anos finais | Hist Gradient Boosting | ~0,52 | ~0,59 | ~2,9× |
| Anos iniciais | Hist Gradient Boosting | ~0,47 | ~0,53 | ~3,5× |

Validação cruzada agrupada por município (5 dobras). Valores exatos em `resultados/`.

## Estrutura do repositório

| Fase CRISP-DM | Notebook | Resultados |
|---|---|---|
| 1. Entendimento do negócio | — (relatório) | — |
| 2. Entendimento dos dados | `notebooks/02_eda.ipynb` | `resultados/02_eda/` |
| 3. Preparação dos dados | `notebooks/01_preparacao.ipynb` | `dados/tabela_analitica.csv` |
| 4. Modelagem | `notebooks/03_modelagem.ipynb` | `resultados/03_modelagem/` |
| 5. Avaliação | `notebooks/04_avaliacao.ipynb` | `resultados/04_avaliacao/` |
| 6. Implantação | `notebooks/04_avaliacao.ipynb` (lista priorizada) | `resultados/05_implantacao/` |

A preparação vem antes da EDA na numeração porque a exploração foi feita sobre a tabela analítica já integrada; o CRISP-DM prevê esse vaivém entre as fases 2 e 3.

## Como executar

1. Abra um notebook de `notebooks/` no Google Colab (botão *Open in Colab* no topo de cada arquivo).
2. Use **Ambiente de execução → Executar tudo**. A primeira célula clona este repositório e instala as dependências de `requirements.txt`.
3. Os notebooks 02 a 04 partem de `dados/tabela_analitica.csv` (136.713 linhas escola × etapa, 27 colunas) e rodam sem outros arquivos.

**Notebook 01 (preparação):** usa os dados brutos do Inep, que não estão no repositório por tamanho. Para reproduzi-lo, baixe as bases abaixo e ajuste o caminho na primeira célula.

## Fontes de dados (Inep)

- Censo Escolar 2025 (microdados)
- Indicadores Educacionais 2025: taxas de rendimento, TNR, AFD, ATU, DSU, HAD, ICG, IED, IRD, TDI
- INSE 2023 por escola
- Ideb 2025 (não usado como preditor: o componente de rendimento deriva da aprovação, o que vazaria o alvo)

Portal: https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos

## Equipe

DATASYNC (grupo 11) — nomes e RAs no relatório final.
