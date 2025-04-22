# Laboratório: Modelo de Previsão no Azure Machine Learning


## 🌐 Visão Geral
Este projeto implementa um modelo de aprendizado de máquina na nuvem do Azure, desde a criação do workspace até a implantação de um endpoint para consumo via API. O modelo utiliza o Azure Machine Learning Studio para todo o fluxo de trabalho.

## 📚 Índice
1.⚙️ Configuração Inicial no Azure

2.🛠️ Preparando o Ambiente

3.🤖 Criando o Modelo de Previsão

4.🚀 Implantando o Modelo como Web Service

5.🧪 Testando o Endpoint

6.🔌 Consumindo a API

## 🏗️ Crie um workspace de Machine Learning:

- No portal Azure, clique em "Criar um recurso"
- 🔍 Pesquise por "Machine Learning" e selecione o serviço
- ⚙️ Configure com:
  * 📛 Nome do workspace
  * 💳 Assinatura
  * 📦 Grupo de recursos (crie um novo se necessário)
  * 🌍 Região mais próxima
 
2. 🛠️ Preparando o Ambiente:

💻 Acesse o Azure ML Studio:

Acesse ml.azure.com

🔑 Selecione seu workspace criado

⚡ Configure a computação:

- 🖥️ Navegue até "Gerenciar" > "Computação"
- 🆕 Crie uma nova instância de computação:
  * 🔧 Tipo: CPU (Standard_DS3_v2 para início)
  * 🏷️ Nome: minha-instancia-cpu
  * 📊 Tamanho: 16GB RAM, 4 vCPUs
 
## 3. 🤖 Criando o Modelo de Previsão
📓 Crie um novo notebook:

Na seção "Autor" > "Notebooks"

➕ Crie um arquivo chamado modelo_previsao.ipynb

👩💻 Código do modelo (exemplo com Random Forest):

```python
📚 Importações
from azureml.core import Workspace, Experiment
from sklearn.ensemble import RandomForestRegressor
import joblib

 🔌 Conecta ao workspace
ws = Workspace.from_config()
experiment = Experiment(ws, 'experimento-previsao')

[🔡 Seu código de preparação de dados aqui]

🏋️ Treina o modelo
model = RandomForestRegressor(n_estimators=100)
model.fit(X_train, y_train)

💾 Salva o modelo
joblib.dump(model, 'outputs/model.pkl')
```python


