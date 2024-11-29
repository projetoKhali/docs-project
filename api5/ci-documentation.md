# Configuração de CI (Continuous Integration)

## 1. O que é CI (Continuous Integration)?
**Continuous Integration (CI)** é uma prática de desenvolvimento que automatiza a integração de código de diferentes desenvolvedores em um único repositório. O objetivo é detectar erros rapidamente, garantindo que o código seja testado e validado antes de ser integrado ao projeto principal.

No projeto **api5**, utilizamos o **GitHub Actions** como ferramenta de CI. Os pipelines estão definidos em arquivos YAML localizados na pasta `.github` de cada submódulo (front-end e back-end).

---

## 2. Configuração da CI
No projeto, configuramos quatro pipelines principais:

- **Build Pipeline**: Responsável por compilar o código para produção, garantindo que ele pode ser executado em ambiente de produção.
- **Unit Tests**: Executa os testes unitários, validando partes específicas do código.
- **Integration Tests**: Valida a integração entre diferentes componentes do sistema.
- **Deploy**: Automatiza o envio do projeto para o ambiente de produção.

---

## 3. Gatilhos e Rotina de CI

### 3.1 Gatilhos das pipelines de testes
Os pipelines de testes são disparados em dois cenários:

- **Push**: Para qualquer branch.
- **Pull Request**: Apenas para as branches `dev` e `main`.

  - **Branch `dev`**: Garante a consistência do código antes de integrar na branch principal. Geralmente, isso ocorre cerca de uma semana antes do término da sprint.
  - **Branch `main`**: Última etapa de validação antes do deploy final, assegurando a ausência de falhas.

### 3.2 Gatilhos das pipelines de build
Os pipelines de build são executados nos seguintes cenários:

- **Push**: Para todas as branches.
- **Pull Request**: Para todas as branches.

Essa configuração permite que o processo de build seja validado em qualquer etapa do ciclo de desenvolvimento.

### 3.3 Gatilhos das pipelines de deploy
O pipeline de deploy é acionado apenas em:

- **Pull Request na branch `main`**: Isso garante que apenas o código final, revisado e validado, seja enviado para o ambiente de produção.

---

## 4. Como contribuir com a CI
Para trabalhar de forma integrada ao pipeline de CI, siga estas etapas:

1. **Commit** regularmente em sua branch de trabalho.
2. Antes de abrir um **pull request** para `dev` ou `main`, verifique se os testes e o build estão funcionando localmente.
3. Consulte os arquivos YAML para entender os requisitos e comandos específicos utilizados em cada pipeline. Estes estão localizados na pasta `.github` do repositório.