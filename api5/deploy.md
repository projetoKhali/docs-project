# Documentação de Deploy

Documentação de Deploy para API5 Frontend<br>
Tânia Cruz

---

## 1. Objetivo

Este documento detalha o processo de deploy da aplicação API5 Frontend hospedada no serviço Azure Container Apps, configurada para receber atualizações a partir da branch main. O deploy é realizado no final de cada sprint para integrar as demandas desenvolvidas.

---

## 2. Pré-requisitos
#### Ferramentas Necessárias
- Conta de acesso ao repositório no GitHub.
- Acesso ao Azure com permissões para gerenciar o serviço de container.
- GitHub Actions configurado com as seguintes permissões:
    - Secrets para credenciais e variáveis de ambiente.

#### Branch para Deploy
- O deploy ocorre somente a partir da branch main.

#### Checklist Pré-Deploy
- Todas as tarefas da sprint foram concluídas.
- Todos os testes automatizados passaram com sucesso.
- O pipeline de CI/CD foi validado sem erros na branch main.

---

## 3. Fluxo de Deploy

#### Gatilho
O deploy é acionado automaticamente ao realizar um push na branch main.

#### Pipeline do GitHub Actions
- O arquivo de configuração usado para gerenciar o deploy é o seguinte:
```yaml
name: Deploy

on:
  push:
    branches: [ "main" ]

jobs:

  deploy:
    runs-on: ubuntu-latest
    environment: production
    env:
      # Variáveis de banco de dados
      DB_HOST: ${{ secrets.DB_HOST }}
      ...
      
    steps:
    - uses: actions/checkout@v4

    - name: 'Login via Azure CLI'
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}

    - name: Env
      shell: bash
      run: echo -e "
        DB_HOST=${DB_HOST}\r
        DB_PORT=${DB_PORT}\r
        ..." > .env.production

    - name: 'Build and push image'
      uses: azure/docker-login@v1
      ...
```

#### Etapas do Deploy
1. Login no Azure CLI: O pipeline autentica automaticamente na conta da Azure usando o secret AZURE_CREDENTIALS.
2. Configuração de Variáveis de Ambiente: Um arquivo .env.production é gerado a partir dos valores armazenados nos secrets do GitHub.
3. Build da Imagem: A aplicação é empacotada em uma imagem Docker.
4. Push para o Registro Azure: A imagem é enviada para o Azure Container Registry configurado.

---

## 4. Validação Pós-Deploy
#### Checklist de Validação
- Verificar se o container está em execução no Azure.
- Testar manualmente as principais rotas da API no endereço:
https://api5frontend.kindmushroom-02aec086.brazilsouth.azurecontainerapps.io
- Monitorar logs e métricas por 24 horas para identificar erros ou falhas.
- Conferir a comunicação entre os serviços, incluindo a conexão com o banco de dados e o Data Warehouse.