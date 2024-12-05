# Documentação de Deploy

**API5**  
*Tânia Cruz*  

---

## 1. O que é Deploy

Deploy (ou "deployment") é o processo de disponibilizar uma aplicação ou sistema em um ambiente específico, como produção, desenvolvimento ou testes. Essa etapa final do ciclo de desenvolvimento de software torna o código desenvolvido e testado acessível para usuários finais ou outras partes interessadas.

A automatização do Deploy permite que atualizações no GitHub sejam publicadas automaticamente, sem intervenção manual, garantindo maior eficiência e consistência.

---

## 2. Pré-requisitos

- Utilização de serviços Azure.

---

## 3. Configuração do Deploy e Ferramentas Utilizadas

### Infraestrutura
- **Servidores**:
  - 2 para bancos de dados:
    - **DB**: Azure Database for PostgreSQL - Flexible Server.
    - **DW**: Azure Database for PostgreSQL - Flexible Server.
  - 2 para aplicações:
    - **Backend** e **Frontend**: Azure Container Apps.

### Ferramentas
- **Docker**: Para criação das imagens das aplicações (backend e frontend).
- **Azure Container Registry**: Para armazenamento das imagens Docker.
- **GitHub Actions**: Para automatizar o processo de Deploy.

---

## 4. Fluxo para Realização do Deploy

1. **Configuração de Bancos de Dados**:
   - Criar dois Azure Database for PostgreSQL - Flexible Server, para o DB e o DW.
   - Inserir as credenciais desses bancos no arquivo `.env` local, permitindo que a aplicação local alimente os bancos de dados hospedados na Azure.

2. **Configuração de Ambiente de Produção**:
   - Criar o arquivo `.env.production` contendo as credenciais dos bancos de dados do ambiente de produção (Azure).

3. **Configuração de Imagens Docker**:
   - Criar arquivos `Dockerfile` separados para backend e frontend, incluindo o comando:
     ```dockerfile
     COPY .env.production .env
     ```
     Isso garante que o arquivo `.env` seja sobrescrito pelo `.env.production`.

4. **Build e Registro de Imagens**:
   - Fazer build das imagens Docker.
   - Criar dois Container Registry na Azure e, via terminal, fazer login no Azure e enviar (`push`) as imagens Docker seguindo as instruções de "Quick Start" da Azure.

5. **Configuração de Container Apps**:
   - Criar dois Azure Container Apps e configurar cada um para utilizar as imagens correspondentes no Container Registry.

---

## 5. Medida de Segurança

- Mensagens de erro no código podem expor credenciais sensíveis. Para mitigar esse risco:
  - Definir `LOCALHOST=FALSE` no `.env.production` e `LOCALHOST=TRUE` no `.env`.
  - Implementar um mecanismo para que, quando `LOCALHOST=FALSE`, as mensagens de erro sejam genéricas, como "Erro".

---

## 6. Fluxo para Automatização do Deploy com GitHub Actions

1. **Autenticação da Azure**:
   - Criar credenciais para autenticação seguindo [esta documentação](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-github-action).

2. **Integração do GitHub com Azure Container Registry**:
   - Configurar o GitHub para realizar `push` e `pull` das imagens Docker, utilizando as credenciais geradas no passo anterior.

3. **Configuração de Credenciais no GitHub**:
   - Registrar as credenciais no GitHub como *secrets*.

4. **Configuração do Workflow**:
   - Criar o arquivo `.github/workflows/deploy.yml` com o YAML abaixo, utilizando as credenciais configuradas como *secrets*:
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
             ..." > .env.production

         - name: 'Build and Push Docker Image'
           uses: azure/docker-login@v1
           ...
     ```

> **Nota**: Este processo deve ser realizado tanto para o backend quanto para o frontend.

---

## 7. Validação Pós-Deploy

### Checklist de Validação
- Verificar o status dos Azure Container Apps.
- Testar manualmente as principais rotas da API nos endereços:
  - Frontend: [https://api5frontend.kindmushroom-02aec086.brazilsouth.azurecontainerapps.io](https://api5frontend.kindmushroom-02aec086.brazilsouth.azurecontainerapps.io).
  - Backend: [https://api5backend.kindmushroom-02aec086.brazilsouth.azurecontainerapps.io/swagger/index.html](https://api5backend.kindmushroom-02aec086.brazilsouth.azurecontainerapps.io/swagger/index.html).

---
