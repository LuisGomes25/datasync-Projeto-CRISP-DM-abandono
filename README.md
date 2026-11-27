# DATASYNC · Identificação de escolas públicas com alto abandono escolar

Projeto final da disciplina **Data Project: Modeling & Implementation** (Faculdade Impacta de Tecnologia), professor Gilberto Alves Pereira. Metodologia **CRISP-DM**.

**Objetivo:** identificar escolas públicas com maior chance de registrar taxas altas de abandono, em cada etapa de ensino, e caracterizar seus perfis de vulnerabilidade, para apoiar a priorização de ações de permanência por secretarias de educação.

> **Leia antes de usar.** O modelo é **associativo**: taxas e características das escolas são do mesmo período (Censo Escolar e Indicadores Educacionais 2025, INSE 2023). Ele aponta escolas com perfil associado ao alto abandono; não prevê o ano seguinte nem indica causas. As conclusões valem para escolas, não para estudantes, e a lista não deve ser usada como ranking punitivo.

## Unidade de análise e alvo

- **Unidade:** a escola em cada etapa que oferece (**escola × etapa**): 136.713 registros de 96.231 escolas públicas. Uma mesma escola pode ter alto abandono em uma etapa e não em outra.
- **Alvo (alto abandono)**, definido por etapa após a EDA:

| Etapa | Regra | Prevalência |
|---|---|---|
| Ensino médio | taxa de abandono ≥ P80 (4,4%) | 20,0% |
| Anos finais | taxa de abandono ≥ P80 (1,8%) | 20,1% |
| Anos iniciais | taxa de abandono > 0 (o P80 é zero) | 15,3% |

- Aprovação, reprovação e Ideb **não** entram como preditores (vazariam o alvo).

## Principais resultados

| Etapa | Modelo | PR-AUC (Reg. Logística) | Precisão nos 10% de maior risco | Vezes o acaso |
|---|---|---|---|---|
| Ensino médio | Random Forest | 0,517 (0,494) | 0,594 | 3,0× |
| Anos finais | Hist Gradient Boosting | 0,516 (0,472) | 0,590 | 2,9× |
| Anos iniciais | Hist Gradient Boosting | 0,468 (0,412) | 0,533 | 3,5× |

Validação cruzada agrupada por município (5 dobras). **Critério de aceite:** precisão no top 10% ≥ 2× a prevalência e PR-AUC acima da Regressão Logística; atendido nas três etapas. Valores exatos e relatórios em PDF em `resultados/` (um por fase).

## Estrutura do repositório

Os notebooks estão numerados na **ordem de execução**. A preparação vem antes da EDA porque a exploração foi feita sobre a tabela analítica já integrada (o CRISP-DM prevê esse vaivém entre as fases 2 e 3).

| Ordem | Notebook | Fase CRISP-DM | Saída |
|---|---|---|---|
| — | — (relatório) | 1. Entendimento do negócio | — |
| 01 | `notebooks/01_preparacao.ipynb` | 3. Preparação dos dados | `dados/tabela_analitica.csv` |
| 02 | `notebooks/02_eda.ipynb` | 2. Entendimento dos dados | `resultados/02_eda/` |
| 03 | `notebooks/03_modelagem.ipynb` | 4. Modelagem | `resultados/03_modelagem/` |
| 04 | `notebooks/04_avaliacao_implantacao.ipynb` | 5. Avaliação e 6. Implantação | `resultados/04_avaliacao/` e `resultados/05_implantacao/` |

## Como executar

1. Abra um notebook de `notebooks/` no Google Colab (em colab.research.google.com → Abrir notebook → GitHub, cole `LuisGomes25/datasync-Projeto-CRISP-DM-abandono`).
2. Use **Ambiente de execução → Executar tudo**. A primeira célula clona este repositório.
3. Os notebooks 02 a 04 partem de `dados/tabela_analitica.csv` e rodam sem outros arquivos. Ordem recomendada: 02 → 03 → 04 (o PDF do 04 usa gráficos do 02).
4. Tempo aproximado no Colab gratuito: 02 ≈ 2 min; 03 ≈ 7 min; 04 ≈ 10–15 min. Os números podem variar na 3ª–4ª casa decimal entre execuções.

**Notebook 01 (preparação):** usa os dados brutos do Inep, que não estão no repositório por tamanho. Ele monta o Google Drive e espera a pasta `DATASYNC_abandono_escolar_2025` com as bases abaixo.

## Fontes de dados (Inep)

- Censo Escolar 2025 (microdados)
- Indicadores Educacionais 2025: taxas de rendimento, TNR, AFD, ATU, DSU, HAD, ICG, IED, IRD, TDI
- INSE 2023 por escola
- Ideb 2025 (não usado como preditor)

Portal: https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos

## Limitações

- Modelo associativo (ver aviso acima); o ano de referência das taxas está a confirmar na nota técnica do Inep.
- Nos anos iniciais, o rótulo "taxa > 0" é sensível ao porte da escola (escolas pequenas têm mais chance de taxa zero).
- XGBoost, previsto no planejamento, foi substituído por Hist Gradient Boosting (scikit-learn); hiperparâmetros fixos, sem busca.
- Equipe de apoio, conectividade e EJA não estão na base; essas hipóteses não foram testadas.

## Equipe

DATASYNC · Curso Superior de Tecnologia em Banco de Dados · turma EAD - BD 5A

- Danieli Santos Queiroz
- Deysianne de Lima Tarcha
- Divonzi Barbosa do Amaral
- Jaqueline Luzinete Izidio Silva Sousa
- Luís Eduardo Gomes
- Ricardo Carvalho Santos
- Rodrigo Lima Cunha
- Rubens Vitorio de Oliveira Santos
