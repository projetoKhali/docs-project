# Testes de Integração

## 1. O que são testes de integração?

São testes projetados para validar a interação entre diferentes componentes do sistema. No projeto **api5back**, eles garantem que a comunicação entre módulos e serviços está funcionando como esperado e que os fluxos de dados entre as camadas do sistema estão corretos.

Esses testes verificam cenários mais próximos do uso real do sistema, como operações de banco de dados, manipulação de entidades, e interações entre serviços. Isso é essencial para assegurar que os módulos, mesmo que estejam isoladamente corretos (testados com Unit Tests), também funcionem adequadamente em conjunto.

---

## 2. Estrutura de Testes de Integração

Os testes de integração no projeto estão organizados em subdiretórios dentro de cada módulo correspondente. Eles utilizam o **Go testing framework** e bibliotecas como:

- **`testcontainers-go`**: para configurar e gerenciar instâncias de banco de dados em containers Docker durante os testes.
- **`github.com/stretchr/testify`**: para asserções.
- **`ent`**: ORM para interagir com o banco de dados.

### Cada teste segue um fluxo comum:

1. Configuração de um ambiente de integração utilizando `IntegrationEnvironment`.
2. Migração e preparação do banco de dados.
3. Execução das operações necessárias e validação dos resultados esperados.

## 2.1. `IntegrationEnvironment`

Para auxiliar com a conexão com o banco de dados e a execução de migrações, foi criado o módulo `integration` que contém a estrutura `IntegrationEnvironment` e funções auxiliares. O `IntegrationEnvironment` facilita a execução dos containers de banco de dados durante os testes e a execução de migrações e seeds necessários, especificados pelos próprios testes.

O `IntegrationEnvironment` utiliza a biblioteca `testcontainers-go` para gerenciar os containers de banco de dados e o `ent` para interagir com o banco de dados. Containers Docker são criados e iniciados automaticamente antes dos testes e encerrados após o término da execução de todos os testes solicitados, podendo reutilizar o mesmo container para diferentes testes em uma mesma execução.

### Configurando o `IntegrationEnvironment`:

```go
	ctx := context.Background()
	intEnv = database.
		DefaultIntegrationEnvironment(ctx).
		WithSeeds(seeds.DataWarehouse)
```

Neste exemplo, o ambiente de integração é configurado com as configurações padrão, e os seeds do `DataWarehouse` são executados.

### Configuração padrão:

```go
func DefaultIntegrationEnvironment(ctx context.Context) *IntegrationEnvironment {
	...
	return newIntegrationEnvironment(ctx, credentials).
		WithClient().
		WithSleep().
		WithWipe().
		WithMigration()
```

O ambiente padrão inclui:

- **`WithClient()`**: Configuração do `ent.Client` para interagir com o banco de dados, que poderá ser acessado através do campo `intEnv.Client`.
- **`WithSleep()`**: Tempo de espera necessário para garantir que o banco de dados esteja pronto para aceitar conexões antes de dar continuidade aos testes.
- **`WithWipe()`**: Limpeza do banco de dados após a execução dos testes. Para garantir que os testes não deixem resíduos que possam interferir em outros testes ao reutilizar containers entre testes.
- **`WithMigration()`**: Aplicação de migrações no banco de dados antes da execução dos testes. Para garantir que o banco contenha as tabelas necessárias para os testes.

---

## 3. Como executar os testes de integração

O projeto inclui comandos no **Makefile** para facilitar a execução dos testes de integração. Dependendo do módulo ou do escopo desejado, os testes podem ser executados de forma abrangente ou específica.

### Comando principal

O comando **`make test-integration`** executa os testes de integração em todo o projeto ou em um módulo específico.

#### Execução de todos os testes de integração:

```bash
make test-integration
```

Este comando irá:

1. Gerar os arquivos necessários (se aplicável) utilizando o comando `make gen`.
2. Executar os testes em todos os módulos do projeto, exceto os subdiretórios `ent/` e `docs/`.

#### Execução de testes em um módulo específico:

```bash
make test-integration module=<nome-do-modulo>
```

Substitua `<nome-do-modulo>` pelo diretório do módulo, por exemplo, `database`, `processing`, ou `service`. Isso é útil para depurar e validar um módulo individualmente.

Exemplo:

```bash
make test-integration module=database
```

---

## 4. Convenções e Boas Práticas para Integração de Testes

### 4.1 Estrutura dos testes

Os testes de integração seguem uma estrutura comum:

1. **Configuração do ambiente de integração**:
   Cada teste inicializa um `IntegrationEnvironment` que configura uma conexão com o banco de dados, aplica migrações, e popula o banco com dados necessários utilizando os seeds, como o `seeds.DataWarehouse`.

2. **Operações principais**:
   São realizadas interações com o banco de dados ou outros serviços, como:

   - Inserção, recuperação e validação de entidades.
   - Testes de relacionamento e consultas complexas entre tabelas.

3. **Validação de resultados**:
   Utiliza bibliotecas como `testify` para garantir que os dados retornados correspondam aos esperados.

### 4.2 Configuração de ambiente

Antes de rodar os testes, certifique-se de que:

- A infraestrutura necessária (como Docker) esteja configurada para executar containers para os testes.
- O arquivo `.env.integration` esteja devidamente configurado, incluindo variáveis como tempo de inicialização do banco de dados.

### 4.3 Organização dos arquivos

Os testes de integração podem estar localizados em qualquer subdiretório dentro de `src/`:

- **`src/database/`**: Testes de operações básicas no banco de dados.
- **`src/processing/`**: Testes envolvendo cálculos e transformações de dados.
- **`src/service/`**: Testes de funcionalidades de alto nível, como sugestões e agregações.

---

## 5. Exemplos de Casos de Testes

### 5.1 Testes de operações básicas no banco de

Local: `src/database/database_integration_test.go`

- **Fluxo principal**:
  - Configuração do ambiente de integração.
  - Aplicação de migrações no banco.
  - Inserção, consulta e exclusão de registros em tabelas como `dim_user` e `hiring_process_candidate`.

### 5.2 Testes de cálculo e transformações

Local: `src/processing/cards_computing_integration_test.go`

- **Fluxo principal**:
  - Criação de dados de teste em tabelas de processos e candidatos.
  - Validação de agregações, como tempo médio de contratação e número de processos em aberto.

### 5.3 Testes de funcionalidades de sugestão

Local: `src/service/suggestions_integration_test.go`

- **Fluxo principal**:
  - Execução de funções de sugestão para entidades como `users`, `processes`, e `vacancies`.
  - Validação de deduplicação e contagem de resultados.

---

## 6. Resolução de Problemas

- **Erro de conexão com o banco de dados**:
  Verifique se o Docker está ativo e se as configurações no `.env.integration` estão corretas. Certifique-se também que nenhum outro serviço esteja utilizando a mesma porta.

- **Testes falhando devido ao tempo de inicialização**:
  Experimente aumentar o tempo de espera configurado para os containers de teste no arquivo `.env.integration`. Máquinas mais lentas podem precisar de um tempo maior para inicializar o banco de dados.

- **Problemas de migração**:
  Certifique-se de que as migrações estão atualizadas e foram geradas corretamente antes de executar os testes.

---

Seguindo essas diretrizes, os testes de integração podem ser usados de maneira eficiente para garantir a confiabilidade e a robustez do sistema como um todo.
