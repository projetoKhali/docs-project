# Configuração de CI (Continuous Integration)

Esta documentação explica como funciona a configuração do fluxo de **Integração Contínua (CI)** no projeto api5, tanto para o **front-end** quanto para o **back-end**, e como os desenvolvedores podem trabalhar de forma integrada com o pipeline de testes e builds.

---

## 1. O que é CI (Continuous Integration)?

CI é uma prática de desenvolvimento que automatiza a integração de código de diferentes desenvolvedores em um único repositório. O objetivo é detectar erros rapidamente, garantir que o código seja testado e esteja funcionando corretamente antes de ser integrado ao projeto principal.

No nosso caso, usamos **GitHub Actions** como ferramenta de CI, que executa pipelines definidas em arquivos YAML para verificar builds, rodar testes e outros processos automatizados. Esses arquivos se encontram dentro da pasta `.github`, na raiz de cada submódulo (front e back-end) do projeto.

---

## 2. Configuração da CI

Em ambos submódulos, temos três pipelines principais configuradas:

- **Build Pipeline**
- **Unit tests (Testes unitários)**
- **Integration tests (Testes de integração)**

### Build Pipeline
Pipeline responsável por compilar o código para produção.

### Unit tests
Pipeline responsável por rodar os testes unitários.

### Integration tests
Pipeline responsável por rodar os testes unitários.


## 3. Rotina de CI

### Gatilhos para pipelines de testes
Nossa pipeline de CI roda com os gatilhos de `push` em todas as branches, e de `pull request` em branches específicas, sendo elas:
    Dev: com o objetivo de garantir a consistência do código na branch dev, que é a penúltima branch para qual os commits vão antes da finalização de uma sprint, geralmente com a antecedência de 1 semana antes do pull request para Main.
    Main: como uma segunda etapa para assegurar a ausência de falhas no projeto, sendo a última branch que recebe o código, e portanto, precisa estar perfeita.

### Gatilhos para pipelines de build
As pipelines de build rodam com os mesmos gatilhos, porém em todas as branches para as duas ações, `push` e `pull request`, e isso se da pela necessidade ainda maior que é o build estar funcionando sempre, independente de que momento a equipe de desenvolvimento esteja, seja no início, meio ou fim da sprint.