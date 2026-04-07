# Deep-Learning-for-Survival-Analysis-Mortality-Risk-Prediction

Deep Learning para Análise de Sobrevivência: Predição de Risco de Mortalidade
Este repositório contém a implementação do meu Trabalho de Conclusão de Curso (TCC), focado em aplicar técnicas de Deep Learning para Análise de Sobrevivência, superando as limitações dos modelos estatísticos tradicionais ao lidar com dados censurados e relações não lineares complexas.

O projeto utiliza uma rede neural profunda para estimar o risco relativo de mortalidade de pacientes, tendo como base os registros do SEER (Surveillance, Epidemiology, and End Results Program) focados em câncer de mama, processando uma base de dados em larga escala com mais de 1,3 milhão de registros clínicos.

🎯 Objetivo do Projeto
Desenvolver um modelo de estratificação de risco clínico capaz de aprender representações não lineares a partir de características dos pacientes, utilizando a função matemática de Cox Partial Likelihood diretamente no processo de otimização (backpropagation) da rede neural.

🧠 Metodologia e Diferenciais Técnicos
Este projeto se fundamenta no estado da arte em aprendizado de máquina para tempo-até-o-evento, englobando as seguintes abordagens:

Função de Perda de Cox (Negative Log Partial Likelihood): Substituição de métricas tradicionais (como MSE ou Cross-Entropy) por uma função especializada que modela o Risco Relativo (Hazard Ratio) e assimila naturalmente os pacientes censurados no Risk Set. Baseado na arquitetura proposta pelo DeepSurv (Katzman et al., 2018).

Learning Rate Finder (LR Finder): Implementação da técnica de Leslie N. Smith (2017) para descobrir empiricamente a taxa de aprendizado ideal, garantindo uma descida de gradiente rápida e segura.

Otimização com CyclicLR: Utilização de política de taxa de aprendizado cíclica (modo triangular2) para evitar mínimos locais e garantir uma convergência estável dos pesos do modelo.

Processamento Otimizado (Out-of-Memory handling): Pipeline de engenharia de dados construído com pandas e torch.tensor (float32) projetado para evitar o estouro de memória RAM ao aplicar One-Hot Encoding em datasets de altíssima cardinalidade.

Avaliação Métrica (C-Index): Validação do modelo utilizando o Índice de Concordância para medir a exatidão do modelo em ordenar corretamente os tempos de sobrevida dos pacientes.

🛠️ Tecnologias Utilizadas
Linguagem: Python 3

Deep Learning Framework: PyTorch (torch, torch.nn, torch.optim)

Manipulação de Dados: Pandas, NumPy, Scikit-learn

Métricas de Sobrevivência: Lifelines (concordance_index)

Otimização de Hiperparâmetros: torch-lr-finder

📊 Estrutura dos Dados (Input)
O modelo espera um pipeline de entrada estruturado contendo:

X_tensor: Matriz esparsa (float32) contendo características clínicas (ex: Idade, Estágio do Tumor, Status de Receptores).

y_combined: Tensor de duas colunas contendo o tempo de sobrevivência em meses (Survival months) e o indicador binário do evento (Event: 1 = Óbito, 0 = Censura).
