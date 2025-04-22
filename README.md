# Modelo de Previsão no Azure Machine Learning

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
```
## 🌐4. Implantando o Modelo como Web Service:

📝 Registro do modelo:

- 📂 Vá para "Ativos" > "Modelos"
- 🆕 Clique em "Registrar modelo"
- 🔍 Selecione o arquivo model.pkl
- 📋 Forneça metadados:
  * 🏷️ Nome: modelo-previsao-v1
  * ⚙️ Framework: Scikit-learn
 
 🌐 Criação do endpoint:

 - 🖥️ Navegue até "Endpoints" > "Endpoints em tempo real"
- 🆕 Clique em "Criar":
  * 📛 Nome: endpoint-previsao-prod
  * 🤖 Modelo: modelo-previsao-v1
  * 💻 Tipo de computação: Azure Container Instance (para testes)
  * 📜 Arquivo de scoring: score.py
  * 🏞️ Ambiente: AzureML-Minimal


## 5. 🧪 Testando o Endpoint
🔑 Obtenha as credenciais:

No endpoint criado, vá para a guia "Consumir"

📝 Anote:

🔗 URL do endpoint

🔑 Chave de autenticação

👨💻 Exemplo de chamada:

```python
import requests
import json

endpoint = "SUA_URL_AQUI"
key = "SUA_CHAVE_AQUI"

data = {"data": [[valor1, valor2, valor3]]}
headers = {
    'Content-Type': 'application/json',
    'Authorization': f'Bearer {key}'
}

response = requests.post(endpoint, json.dumps(data), headers=headers)
print(response.json())
```

## 6. 🔌 Consumindo a API

📨 Exemplo de Requisição:
```json
POST https://seu-endpoint.azurecontainer.io/score
Headers:
- Content-Type: application/json
- Authorization: Bearer sua-chave

Body:
{
  "data": [
    [6.5, 3.2, 5.1, 2.2],
    [5.9, 3.0, 5.1, 1.8]
  ]
}
```

## 📌Conclusão: 

🌐 Criei um workspace completo no Azure ML e configurei recursos de computação em nuvem

🤖 Desenvolvi e treinei um modelo preditivo (Random Forest) usando Python e scikit-learn

🚀 Implementei um endpoint de API para servir previsões em tempo real

🔐 Aprendi sobre autenticação e consumo seguro de APIs com chaves de acesso

📝 Documentei todo o processo em Markdown com emojis e formatação profissional

💡 Adquiri habilidades de MLOps para levar modelos do protótipo à produção na nuvem

✨ Resultado: Pipeline completo de Machine Learning pronto para produção, desde o treinamento até a disponibilização via API consumível!


