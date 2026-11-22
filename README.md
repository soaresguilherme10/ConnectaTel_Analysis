📱 Análise de Clientes ConnectaTel

Análise exploratória de uma empresa de telecomunicações na América Latina, a ConnectaTel, com foco em qualidade de dados, perfil de uso, segmentação de clientes e oportunidades comerciais. Projeto desenvolvido como parte do Sprint 8 do MBA.

🎯 Objetivo do projeto

Avaliar o comportamento dos clientes da ConnectaTel com base nos dados registrados até 2024, para:

verificar a qualidade e a confiabilidade dos dados (ausentes, sentinels e datas impossíveis);
construir um perfil estatístico dos usuários (idade, mensagens, chamadas e minutos);
detectar comportamentos atípicos (outliers);
criar segmentos de clientes por idade e nível de uso;
propor recomendações comerciais (retenção e melhoria de planos).
🗂️ Datasets utilizados
Arquivo	Linhas	Descrição
plans.csv	2	Catálogo de planos: preço mensal, mensagens, minutos e GB incluídos, e custo dos extras
users_brasil.csv	4.000	Dados dos clientes: user_id, nome, age, city, reg_date, plan e churn_date
usage.csv	40.000	Registros de uso: id, user_id, type (call/text), date, duration (chamadas) e length (mensagens)

Os arquivos são carregados diretamente pelas URLs públicas, dentro do próprio notebook:

https://practicum-content.s3.us-west-1.amazonaws.com/datasets/plans.csv

https://practicum-content.s3.us-west-1.amazonaws.com/datasets/users_brasil.csv

https://practicum-content.s3.us-west-1.amazonaws.com/datasets/usage.csv

A coluna churn_date vazia indica que o cliente continua ativo; ela não é tratada como erro.

🔄 Etapas da análise
Carregar e explorar: leitura dos três datasets, .head(), .shape e .info().
Identificação de problemas de qualidade:
contagem e proporção de valores ausentes;
detecção de sentinels (-999 em age, "?" em city);
conversão de datas e revisão de anos impossíveis (ex.: 2026).
Limpeza básica:
age: sentinel -999 substituído pela mediana;
city: sentinel "?" convertido em ausente;
datas posteriores a 2024 marcadas como NaT;
ausentes de duration e length mantidos como NA (padrão MAR: dependem de type).
Estatísticas resumidas: agregação do uso por usuário (quant_mensagens, quant_chamadas, quant_minutos_chamada), união com users e resumo estatístico.
Visualização e outliers: histogramas por plano e boxplots; limites pelo método IQR. Os outliers foram mantidos, por serem valores plausíveis que representam clientes de maior consumo.
Segmentação: criação de grupo_uso (Baixo uso, Uso médio, Alto uso) e grupo_idade (Jovem, Adulto, Idoso), com visualização por countplot.
Insight executivo: conclusões e recomendações para o negócio.
🔍 Principais achados
Qualidade dos dados: sentinel -999 em age (55 usuários), "?" em city (96), 469 cidades ausentes, 40 datas de cadastro em 2026 e 50 registros de uso sem data.
Perfil de uso: a maioria dos usuários tem uso baixo a médio; o total de minutos é assimétrico à direita, com um pequeno grupo de usuários de consumo muito alto.
Segmentos: o grupo Adulto (30 a 59 anos) é o maior, e o Uso médio concentra a maior parte da base.
Idade não explica o comportamento: a proporção de Premium e o nível de uso são semelhantes entre as faixas etárias.
Planos: Básico e Premium têm padrão de uso praticamente idêntico, mesmo com franquias e preços bem diferentes, o que sugere espaço para um plano intermediário.

As conclusões completas e as recomendações estão na Etapa 7 do notebook.

▶️ Como executar o notebook
Opção A: Google Colab (recomendada)
Acesse o Google Colab.
Vá em File → Open notebook → GitHub e cole a URL deste repositório (ou Upload do arquivo .ipynb).

Opção B: Jupyter local
bash
git clone https://github.com/soaresguilherme10/ConnectaTel_Analysis.git
cd SEU_REPOSITORIO
pip install pandas seaborn matplotlib numpy jupyter
jupyter notebook

Abra o arquivo .ipynb e execute com Kernel → Restart & Run All.

Requisitos: Python 3.9+ e conexão com a internet (os dados são lidos das URLs).

🔁 Guia rápido de reprodução
Abra o notebook e execute todas as células na ordem, de cima para baixo. As etapas dependem das anteriores (ex.: user_profile só existe após a Etapa 4).
Se aparecer NameError, o kernel foi reiniciado: rode novamente desde a primeira célula.
Antes de publicar, confirme que o notebook roda do início ao fim sem erros (Restart & Run All).
🛠️ Tecnologias
Python
Pandas e NumPy
Matplotlib e Seaborn
Jupyter / Google Colab
📁 Estrutura do repositório
├── README.md
└── notebooks/
    └── analise_connectatel.ipynb
👤 Autor

Guilherme Soares · GitHub
