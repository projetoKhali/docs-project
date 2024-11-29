# Configuração de CI (Continuous Integration)

Esta documentação explica como funciona a configuração do fluxo de **Integração Contínua (CI)** no projeto api5, tanto para o **front-end** quanto para o **back-end**, e como os desenvolvedores podem trabalhar de forma integrada com o pipeline de testes e builds.

---

## **1. O que é CI (Continuous Integration)?**

CI é uma prática de desenvolvimento que automatiza a integração de código de diferentes desenvolvedores em um único repositório. O objetivo é detectar erros rapidamente, garantir que o código seja testado e esteja funcionando corretamente antes de ser integrado ao projeto principal.

No nosso caso, usamos **GitHub Actions** como ferramenta de CI, que executa pipelines definidas em arquivos YAML para verificar builds, rodar testes e outros processos automatizados. Esses arquivos se encontram dentro da pasta `.github`, na raiz de cada submódulo (front e back-end) do projeto.

---

## **2. Configuração da CI**

Em ambos submódulos, temos três pipelines principais configuradas:

- **Build Pipeline**
- **Unit tests (Testes unitários)**
- **Integration tests (Testes de integração)**

### Build Pipeline
Pipeline responsável por compilar o código para produção.

#### Back-end

- **Arquitetura do Pipeline**:
  - **Configuração do ambiente Go**: Utiliza a ação `setup-go` para configurar o Go no ambiente de CI.
  - **Geração de arquivos**: Executa o script de geração de arquivos necessários para o funcionamento do projeto.
  - **Execução dos testes unitários**: Utiliza o comando `make test` para rodar os testes unitários, com as tags de produção definidas.

#### Front-end

- **Arquitetura do Pipeline**:
  - **Configuração do ambiente Node.js**: Utiliza a ação `setup-node` para configurar o ambiente Node.js, especificando a versão necessária.
  - **Instalação das dependências**: O comando `npm install` é executado para garantir que todas as dependências do projeto estejam instaladas.
  - **Execução dos testes unitários**: Utiliza o comando `npm run test`, que por sua vez roda os testes com Jest, garantindo que o código front-end esteja funcionando conforme o esperado.

### Unit tests
Pipeline responsável por executar os testes unitários do projeto.

#### Back-end
  - **Execução dos testes unitários**: Utiliza o comando `make test` para rodar os testes unitários. Este comando é configurado para rodar os testes com as tags de produção, garantindo que o código seja testado em um ambiente de produção adequado.

#### Front-end
  - **Execução dos testes unitários**: Utiliza o comando `npm run test` para rodar os testes com Jest. O Jest executa os testes unitários, verificando se o código front-end está funcionando corretamente e validando as funcionalidades de cada componente do sistema.

### Integration tests
Pipeline responsável por executar os testes de integração, garantindo que as diferentes partes do sistema funcionem corretamente juntas.

#### Back-end

- **Arquitetura do Pipeline**:
  - **Execução dos testes de integração**: Utiliza o comando `make test-integration` para rodar os testes de integração. Este comando executa os testes em um ambiente que simula a interação entre diferentes componentes do sistema, validando que as integrações entre os módulos estejam funcionando corretamente.

#### Front-end




