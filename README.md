# Azure Frontier Girls - Challenge - AI Foundry – Guia de Criação de Conta e Agent com Consulta a Base JSON

Este guia explica como:

1. Criar uma conta no **AI Foundry**  
2. Criar um **Agent**  
3. Configurar uma **base de dados JSON**  
4. Fazer o Agent consultar e responder usando esses dados

### 🧩 Neste Challenge criaremos:
1. Um Agent que tem por *finalidade*:  **Confirmar se o cliente está cadastrado na base de dados**.
2. A consulta é feita por **Nome ou E-mail**.
3. Quando encontrado os dados do cliente são exibidos: **Nome, E-mail e a Data de Nascimento**.
   Note que a data de nascimento é uma informação que o cliente não irá informar, apenas o Agent conhece (através da busca à base dados) e exibirá esse dado.

---

## 🚀 1. Criar uma conta e um Projeto AI Foundry

1. Acesse o Portal da Azure e crie um Recurso do Tipo Fábrica de IA do Azure:  
   **https://portal.azure.com/** 
2. Clique Microsoft Foundry e Criar Recurso .
Vai aparecer uma tela para informar os dados da Conta e o Nome do Projeto do Foundry
   - Escolha uma assinatura  
   - Crie um novo Grupo de Recursos que será utilizado exclusivamente para os recursos criados para o seu Agent
   - Nome da Conta do AI Fondry   
   - Região de sua preferência 
   - Nome do Projeto (Default project name)
   
<picture>  
  <img alt="criação da conta no AI Foundry" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/cria%C3%A7%C3%A3o%20da%20conta%20no%20AI%20Foundry.JPG" heigth="100%">
</picture>

3. Acesse o painel principal (**Dashboard**) do AI Foundry.

<picture>  
  <img alt="criação da conta no AI Foundry" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/pagina%20inicial%20do%20projeto%20no%20AI%20Foundry.JPG" heigth="100%">
</picture>

---

## 🤖 2. Criar um novo Agent

1. No Dashboard, no menu esquerdo clique em **Agent**.
2. Selecione o Agent que já está cadastrado. Dê um nome ao Agent (ex.: *AgentConfirmaDados*).
3. Escolha o modelo de IA (ex.: GPT-4, GPT-5, Claude etc., de acordo com o Foundry).
Neste exemplo usamos: GPT-4o-MINI
4. Defina o propósito do agente **Campo Instruções**, exemplo:

'Você é um agente chamado WomakersIA e você confirma se os dados informados estão cadastrados no sistema. Recebe como parâmetro de entrada o Nome ou o E-mail e consulta na base de dados se o cliente está cadastrado. Se encontrar os dados informa "Obrigada por confirmar seus dados". E exibe o Nome, E-mail e Data de nascimento. Se não encontrar os dados na base, informa "Dados não encontrados, por favor, informe Nome ou E-mail para confirmar seu cadastro". Você não responde sobre outros assuntos, apenas solicita os dados, faz a consulta na base e informa se o cadastro foi ou não encontrado.'

<picture>  
  <img alt="Criar um Novo Agent" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/configuração%20do%20agent.jpg" heigth="100%">
</picture>

5. Clique em **Create**.

---

## 📁 3. Adicionar a base de dados JSON

### 🔹 Opção A — Upload de arquivo JSON

1. Acesse a aba **Conhecimento**do Agent.
2. Clique em **Upload File**.
3. Envie seu arquivo, por exemplo:

```json
[
  {
    "nome": "Ana Bezerra", 
    "data_nascimento": "1992-04-15", 
    "email": "ana.bezerra@example.com"
  },
  {
    "nome": "Lucas Andrade", 
    "data_nascimento": "1988-11-03", 
    "email": "lucas.andrade@example.com"
  },
  {
    "nome": "Mariana Costa", 
    "data_nascimento": "1995-07-21", 
    "email": "mariana.costa@example.com"
  },
  {
    "nome": "Rafael Lima", 
    "data_nascimento": "1990-02-09", 
    "email": "rafael.lima@example.com"
  },
  {
    "nome": "Beatriz Melo", 
    "data_nascimento": "1998-06-30", 
    "email": "beatriz.melo@example.com"
  }
]
```
4. Crie uma Ação
Neste passo escolhemos o tipo de Ação **Interpréte de código** que é para o Agent entender que sua ação principal deve ser executar as instruções fornecidas no campo **Instruções** e não tem outra ação adicional.

<picture>  
  <img alt="Criar Ação do Agent" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/configuração%20da%20ação%20do%20agent.jpg" heigth="100%">
</picture>
---

## 🎮 6. Testando o Agent

### 🔹 Dados não encontrado na base de dados JSON

1.  Acesse a ícone 🎮 **Abrir no Playground**.
2. Em dados de entrada digite um nome que não tem na base de dados, por exemplo:
**Gabriela Santos**.
3. Resposta esperada do Agent
```
Dados não encontrados, por favor, informe Nome ou E-mail para confirmar seu cadastro
```
1
<picture>  
  <img alt="Dados não encotrados" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/entrada%20de%20dados%20do%20agente%201.JPG" heigth="100%">
</picture>
2
<picture>  
  <img alt="Dados não encotrados" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/entrada%20de%20dados%20do%20agente%202.JPG" heigth="100%">
</picture>

### 🔹 Consulta por Nome na base de dados JSON

1.  Ainda no 🎮 **Playground**.
2. Em dados de entrada digite um nome que não tem na base de dados, por exemplo:
**Rafael Lima**.
3. Resposta esperada do Agent
```
Obrigada por confirmar seus dados. 
Nome: Rafael Lima
E-mail: rafael.lima@example.com
Data de Nascimento: 09/02/1990
```
<picture>  
  <img alt="Dados encontrados por Nome" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/saída%20de%20dados%201.JPG" heigth="100%">
</picture>

### 🔹 Consulta por E-mail na base de dados JSON

1.  Ainda no 🎮 **Playground**.
2. Em dados de entrada digite um nome que não tem na base de dados, por exemplo:
**thiago.mendes@example.com**.
3. Resposta esperada do Agent
```
Obrigada por confirmar seus dados. 
Nome: Thiago Mendes
E-mail: thiago.mendes@example.com
Data de Nascimento: 11/06/1986
```
<picture>  
  <img alt="Dados encontrados por E-mail" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/saída%20de%20dados%202.JPG" heigth="100%">
</picture>

## (Bônus) 🛠️ 7. Como gerar base de dados JSON
1.  No chat GPT digite a seguinte instrução no prompt **Gerar arquivo Json contendo 50 registros com os seguintes campos: Nome, E-mail e Data de Nascimento**.

Você receberá um resultado semelhante ao arquivo anexo **base.json**. Copie e cole o código e salve o arquivo com a extensão **.json**.

<picture>  
  <img alt="Chat GPT - gerar base" src="https://github.com/GabrielaBrazSantos/azurefrotiergirls/blob/main/azure-frontier-girls-images/chat-gpt-gerar%20base.JPG" heigth="100%">
</picture>


## 🛡️ 8. Referências

- [Documentação oficial do Azure AI Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/)
- [O que é Azure AI Foundry?](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry)
- [Treinamento e módulos – Azure AI Foundry](https://learn.microsoft.com/en-us/training/azure/ai-foundry)
- [AI Foundry na Prática - Aula 2](https://github.com/Miyake-Diogo/AzureFrontierGirls-AI-Challenge/blob/main/Aula%202/Azure_AI_Foundry_na_Pratica_aula_2.md)
- [AI Foundry na Prática - Aula 2](https://github.com/Miyake-Diogo/AzureFrontierGirls-AI-Challenge/blob/main/Aula%202/Azure_AI_Foundry_na_Pratica_aula_2.md)
