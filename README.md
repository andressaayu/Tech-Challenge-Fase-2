# Tech Challenge — Fase 2 | POSTECH Data Analytics

> **INSTRUÇÕES:** este README é um template. Substitua **todos** os blocos marcados com
> `<!-- PREENCHER -->` e apague as linhas de instrução antes de submeter.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Turma | 2DTATBB |
| Grupo | Grupo 21 |
| Data de entrega | 10/10/2026 |

### Integrantes

| Nome completo | RM | E-mail |
|---|---|---|
| Andressa Ayumi Adati Kogati | RM377737 | ayumikogati@gmail.com |
| Janice Angélica Lorenço | RM377757 | janice.lourenco@hotmail.com |
| Luiz Gustavo Tavares da Costa  | RM377791 | pr.luizgustavo@gmail.com |
| Tatiane Bispo Ribeiro  | RM377738 | ribeiro.tati@yahoo.com.br |
| | | |

---

## 2. Links da entrega

Estes três links são **obrigatórios** e devem ser idênticos aos do PDF de submissão.

| Item | Link |
|---|---|
| Repositório | <!-- PREENCHER: URL pública do GitHub --> |
| Vídeo executivo (≤ 5 min) | <!-- PREENCHER: YouTube não listado / Drive com acesso liberado --> |
| Apresentação | https://drive.google.com/file/d/1Cgpa8oUL2ZG2CUsSp5LNz6LaIFUriFkC/view?usp=sharing |

> ⚠️ Repositório privado ou inacessível inviabiliza a avaliação da entrega.
> Confira o acesso em uma janela anônima antes de enviar.

---

## 3. O problema

A concessão de crédito é uma atividade relevante para as instituições financeiras, mas envolve riscos associados à inadimplência. Nesse contexto, a análise dos solicitantes deve buscar identificar perfis com maior ou menor probabilidade de apresentar dificuldades no pagamento, equilibrando a redução do risco de perdas com a oportunidade de conceder crédito a clientes com bom comportamento financeiro. 

O grande volume de solicitações e a diversidade de informações disponíveis tornam o uso de técnicas de análise de dados uma oportunidade para tornar esse processo mais eficiente. O Machine Learning permite explorar padrões presentes nos dados históricos e utilizá-los para classificar novos solicitantes entre perfis de bons e maus pagadores, apoiando o processo de avaliação de crédito. 

### Variável alvo

A variável-alvo definida no projeto foi a MAU_PAGADOR, utilizada para classificar os clientes em bom pagador (0) ou mau pagador (1). A classificação foi construída considerando exclusivamente o comportamento de pagamento na janela dos últimos 12 meses, correspondente aos valores de MONTHS_BALANCE de −11 a 0.

Foi definido como mau pagador (1) o cliente que apresentou pelo menos um STATUS 2, 3, 4 ou 5 nesse período, indicando atraso de 60 dias ou mais. Como bom pagador (0), foram considerados os clientes com registro nos 12 meses da janela, sem ocorrência de STATUS 2–5 e cuja janela não fosse composta exclusivamente por X, que representa ausência de empréstimo no mês. Os demais casos foram classificados como histórico insuficiente e não utilizados na definição das classes.

A escolha da janela de 12 meses busca representar o comportamento de crédito mais recente do cliente, reduzindo a influência de eventos muito antigos. O limiar de 60 dias de atraso foi adotado por representar uma situação de inadimplência mais relevante, permitindo diferenciar atrasos pontuais de um comportamento de pagamento potencialmente mais problemático.

### Dataset

| Campo | Valor |
|---|---|
| Fonte | https://drive.google.com/drive/folders/1rKpbaYI4vOweYaG-TXpGKEmM400uuGzw |
| Linhas × colunas | application_record: (438557 x 18); credit_record: (1048575 x 3) |
| Período / versão | 5 de Agosto de 2026 |

Descrição das variáveis:

**application_record.csv** (cadastro do solicitante)

| Variável | Tipo | Descrição | 
|---|---|---|
| ID | Identificador (inteiro) | Número do cliente | 
| CODE_GENDER | Categórica binária (M/F) | Gênero | 
| FLAG_OWN_CAR | Categórica binária (Y/N) | Tem carro | 
| FLAG_OWN_REALTY | Categórica binária (Y/N) | Existe alguma propriedade | 
| CNT_CHILDREN | Numérica discreta | Número de filhos | 
| AMT_INCOME_TOTAL | Numérica contínua | Renda anual | 
| NAME_INCOME_TYPE | Categórica nominal | Categoria de renda | 
| NAME_EDUCATION_TYPE | Categórica ordinal | Nível educacional | 
| NAME_FAMILY_STATUS | Categórica nominal | Estado civil | 
| NAME_HOUSING_TYPE | Categórica nominal | Modo de vida | 
| DAYS_BIRTH | Numérica discreta (dias) | Aniversário (Contagem regressiva a partir do dia atual (0); -1 significa ontem.) |
| DAYS_EMPLOYED | Numérica discreta (dias) | Data de início do emprego (Contagem regressiva a partir do dia atual (0). Se positivo, a pessoa está atualmente desempregada.) |
| FLAG_MOBIL | Binária (0/1) | Existe celular |
| FLAG_WORK_PHONE | Binária (0/1) | Existe telefone de trabalho | 
| FLAG_PHONE | Binária (0/1) | Tem telefone | 
| FLAG_EMAIL | Binária (0/1) | Existe algum e-mail | 
| OCCUPATION_TYPE | Categórica nominal | Ocupação | 
| CNT_FAM_MEMBERS | Numérica discreta | Tamanho da família | 

**credit_record.csv** (histórico mensal de crédito)

| Variável | Tipo | Descrição | 
|---|---|---|
| ID | Identificador (inteiro) | Número do cliente | |
| MONTHS_BALANCE | Numérica discreta (meses) | Mês do registro (O mês de extração dos dados é o ponto de partida, contando para trás: 0 é o mês atual, -1 é o mês anterior, e assim por diante) |
| STATUS | Categórica ordinal | Status (0: 1-29 dias de atraso; 1: 30-59 dias; 2: 60-89 dias; 3: 90-119 dias; 4: 120-149 dias; 5: dívidas atrasadas ou incobráveis, perdas por mais de 150 dias; C: quitadas naquele mês; X: sem empréstimo no mês.)|

---

## 4. Como reproduzir

```bash
git clone <URL_DO_REPOSITORIO>
cd <NOME_DO_REPOSITORIO>

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
jupyter notebook
```

Baixe o dataset e coloque o arquivo bruto em `data/raw/` (os dados **não** são versionados —
veja `data/README.md`).

Depois execute os notebooks nesta ordem:

| # | Notebook | O que faz |
|---|---|---|
| 1 | `notebooks/01_eda.ipynb` | Análise exploratória |
| 2 | `notebooks/02_preprocessamento.ipynb` | Limpeza, escala e feature engineering |
| 3 | `notebooks/03_modelagem.ipynb` | Treino e comparação dos modelos |
| 4 | `notebooks/04_avaliacao.ipynb` | Métricas, importância de variáveis e conclusões |

**Semente fixa:** `RANDOM_STATE = 42`, declarada na primeira célula de cada notebook.
Rodar os notebooks na ordem acima, a partir de um ambiente limpo, deve reproduzir
exatamente os números da seção 5.

---

## 5. Resultados

| Modelo | Acurácia | Precisão | Recall | F1 | ROC AUC | PR AUC |
|---|---|---|---|---|---|---|
| KNN (A-padrão) | 0.9865 | 0.0000 | 0.0000 | 0.0000 | 0.4973 | 0.0153 |
| Logit (A-padrão) | 0.9865 | 0.0000 | 0.0000 | 0.0000 | 0.5634 | 0.0200 |
| Árvore de Decisão (A-padrão) | 0.9680 | 0.0341 | 0.0500 | 0.0405 | 0.5380 | 0.0163 |
| Random Forest (A-padrão) | 0.9851 | 0.1250 | 0.0167 | 0.0294 | 0.5691 | 0.0355 |
| SVM (A-padrão) | 0.9865 | 0.0000 | 0.0000 | 0.0000 | 0.4846 | 0.0175 |
| KNN (B-balanceada) | 0.5214 | 0.0164 | 0.5833 | 0.0319 | 0.5391 | 0.0150 |
| Logit (B-balanceada) | 0.5387 | 0.0151 | 0.5167 | 0.0294 | 0.5624 | 0.0206 |
| Árvore de Decisão (B-balanceada) | 0.6720 | 0.0159 | 0.3833 | 0.0306 | 0.5167 | 0.0160 |
| Random Forest (B-balanceada) | 0.9397 | 0.0273 | 0.1000 | 0.0429 | 0.5616 | 0.0181 |
| SVM (B-balanceada) | 0.7008 | 0.0115 | 0.2500 | 0.0221 | 0.4351 | 0.0118 |

**Modelo escolhido:** Regressão Logística Balanceada (`class_weight='balanced'`) — foi escolhida pela interpretabilidade e pela robustez, e não por ter o maior desempenho isolado. Os coeficientes e odds ratios são coerentes com o negócio (por exemplo, mais tempo de emprego reduz o risco) e podem ser explicados a áreas de risco e de compliance, o que é essencial em decisão de crédito. Ela teve a melhor PR AUC e AUC média de 0,585, estatisticamente equivalente aos demais modelos, já que as diferenças ficam dentro da margem de erro (IC 95% de 0,42 a 0,64). Como nenhum modelo mais complexo trouxe ganho claro, não há motivo para abrir mão da transparência. O balanceamento também evita o problema dos modelos padrão, que chegam a 98% de acurácia apenas por classificar todos como bons pagadores (recall zero para maus pagadores).

**Métricas priorizadas:** ROC AUC e PR AUC, com recall da classe "mau pagador" e Lift nos decis de maior risco como apoio.

---

## 6. Principais conclusões

1. Os dados cadastrais sozinhos dão um sinal fraco de risco. O modelo campeão (Regressão Logística Balanceada) chegou a AUC média de 0,585, e o intervalo de confiança (0,42 a 0,64) inclui 0,50. Na prática, o modelo ajuda a priorizar, mas não deve ser o único critério para aprovar ou negar crédito.
2. A estabilidade profissional é o fator que mais reduz o risco. Quanto maior o tempo de emprego, menor a chance de inadimplência. Ter carro, ter imóvel e ter mais pessoas na família também reduzem o risco estimado, o que sugere que patrimônio e estabilidade de vida pesam a favor do cliente.
3. Gênero e idade aparecem como fatores de aumento de risco, mas o gênero deve ser removido. O modelo estimou maior risco para homens e, em menor grau, para clientes mais velhos. Como usar gênero na decisão traz risco de discriminação, a recomendação é retirar essa variável preventivamente, o que praticamente não altera o desempenho (perda de AUC desprezível). Renda e escolaridade influenciam muito pouco o resultado.
4. O principal ganho está em priorizar quem acompanhar, não em barrar clientes. Focar nos 5% de clientes mais arriscados captura cerca de 10% da inadimplência (Lift de 2,0x), o dobro do que se obteria por sorteio. Isso serve para direcionar análise manual, limites mais conservadores ou monitoramento, e não para recusa automática.

### Limitações e próximos passos

Limitações
1. Sinal preditivo fraco. A AUC média de 0,585 tem intervalo de confiança (0,42 a 0,64) que inclui 0,50, então o modelo serve como apoio, não como critério único de decisão.
2. Poucos maus pagadores. São 244 casos em 15.371 clientes (1,59%), o que deixa as métricas instáveis.
3. Cadastro pouco discriminante. 79,9% dos clientes têm “gêmeos” e 54,1% dos maus pagadores têm gêmeos bons pagadores, ou seja, perfis iguais com desfechos opostos.
4. Sem dados de comportamento. Faturas, uso do limite e atrasos recentes ficam fora do modelo.
5. Risco de viés. Gênero e idade influenciam o risco estimado, o que traz exposição a discriminação.

Próximos passos
1. Evoluir para scoring comportamental, com análise de faturas e uso do limite.
2. Remover CODE_GENDER (perda de AUC desprezível) e avaliar equidade para idade.
3. Usar o modelo para priorizar, não para recusar: os 5% mais arriscados concentram cerca de 10% da inadimplência (Lift 2,0x).
4. Ampliar a base e validar em outro período, com monitoramento contínuo após a implantação.

---

## 7. Estrutura do repositório

```
.
├── data/          dados brutos (raw) e tratados (processed) — não versionados
├── notebooks/     análise em ordem numerada
└── docs/          apresentação executiva
```

Detalhes e convenções em [`ESTRUTURA.md`](ESTRUTURA.md).
Antes de enviar, percorra o [`CHECKLIST.md`](CHECKLIST.md).

---

## 8. Tecnologias

Python, pandas, NumPy, scikit-learn, matplotlib, seaborn (Jupyter Notebook)
