# Questionario ao cliente 


## Perguntas enviadas no dia 02/09/24 


Em um processo seletivo, tem vagas diferentes em questão de cargos e níveis, ou são as mesmas vagas em todos os quesitos?  

As vagas possuem prazo para serem encerradas. O processo seletivo também possui um prazo? Se ele possuir é diferente do prazo das vagas? 

Quando a vaga não é preenchida, vocês reabrem a mesma vaga ou criam uma vaga nova? Se precisar criar, seria o processo seletivo ao todo ou só a vaga? 

Durante o processo seletivo como a plataforma irá colaborar? Ela vai ajudar somente no acompanhamento dos processos seletivos ou também irá colaborar da contratação? 

<br>

## Repostas do cliente enviadas no dia 05/09/24 08h03 

Sim, podemos ter um processo seletivo com N vagas dentro dele e inclusive de níveis diferentes, exemplo: "Processo seletivo para construção do projeto FATEC: Vamos precisar de contratar um PO, três devs onde será um senior e dois junior." 

Sim, é importante colocar prazo para encerrar, mas o prazo deve estar no processo seletivo; 

Se a vaga não for preenchida, normalmente abrimos posteriormente outro processo seletivo; 

Pela complexidade do projeto aqui faremos apenas o acompanhamento, mas o ideal seria que ele fosse uma ferramenta de Recrutamento e Seleção completa, mas não é o caso aqui agora. 

Mais informações fornecidas pelo cliente neste dia: 

Bom dia, por hora consegui recuperar por aqui os campos que existirão nessa base de dados que vamos gerar, infelizmente ainda não consegui gerar os registros de teste, entretanto vocês podem gerar por aí. É importante ressaltar que vocês tem liberdade para adicionar tabelas adicionais para vocês trabalharem os dados e gerarem o que for necessário para a apresentação dos dados. Acredito que somente essas tabelas sejam suficientes para o que precisamos fazer, caso precise inserir mais alguma informação do nosso lado aviso para vocês. 

##


### Tabela: Processos Seletivos 

Armazena informações gerais sobre cada processo seletivo. 


- ID Processo Seletivo: Identificador únicentrevio do processo seletivo. 

- Nome do Processo Seletivo: Nome ou título do processo seletivo. 

- Data de Início: Data e hora de início do processo seletivo. 

- Data de Término Prevista: Data e hora prevista para o término do processo seletivo. 

- Status do Processo: Status atual (e.g., Aberto, Em Andamento, Fechado). 

- Criado Por: Identificador ou nome da pessoa do RH que criou o processo seletivo. 

- Descrição do Processo: Descrição geral do processo seletivo. 

## 
 

### 1. Tabela: Vagas 

Detalha as vagas específicas dentro de um processo seletivo. 


- ID Vaga: Identificador único da vaga. 

- ID Processo Seletivo: Identificador do processo seletivo ao qual a vaga está associada. 

- Título da Vaga: Título ou nome da vaga (e.g., Gerente, Atendente, Suporte). 

- Número de Posições: Número de posições abertas para a vaga. 

- Requisitos da Vaga: Lista de requisitos ou qualificações necessárias para a vaga. 

- Status da Vaga: Status atual da vaga (e.g., Aberta, Fechada, Em Análise). 

- Localização da Vaga: Local onde a vaga será preenchida (e.g., Cidade, Estado). 

- Responsável pela Vaga: Identificador ou nome da pessoa do RH responsável por gerenciar essa vaga. 

- Data de Abertura da Vaga: Data e hora em que a vaga foi aberta. 

- Data de Fechamento da Vaga: Data e hora previstas ou reais em que a vaga foi fechada. 

##


### 3. Tabela: Candidatos 

Armazena informações sobre os candidatos que se inscreveram para as vagas. 


- ID Candidato: Identificador único do candidato. 

- Nome do Candidato: Nome completo do candidato. 

- ID Vaga: Identificador da vaga para a qual o candidato se inscreveu. 

- Email do Candidato: Email de contato do candidato. 

- Telefone do Candidato: Telefone de contato do candidato. 

- Data da Inscrição: Data e hora em que o candidato se inscreveu para a vaga. 

- Status do Candidato: Status atual no processo seletivo (e.g., Em Análise, Entrevista, Contratado, Rejeitado). 

- Pontuação do Candidato: Pontuação do candidato baseada em critérios de avaliação. 

- Data de Atualização do Status: Data e hora da última atualização de status do candidato. 

##


### 4. Tabela: Entrevistas 

Gerencia as entrevistas agendadas e seus detalhes. 

- ID Entrevista: Identificador único da entrevista. 

- ID Candidato: Identificador do candidato que será entrevistado. 

- ID Vaga: Identificador da vaga relacionada à entrevista. 

- Data da Entrevista: Data e hora da entrevista. 

- Entrevistador: Identificador ou nome do entrevistador ou dos entrevistadores. 

- Resultado da Entrevista: Resultado ou feedback da entrevista. 

- Observações da Entrevista: Notas adicionais ou observações feitas durante a entrevista. 

- Data de Agendamento: Data e hora em que a entrevista foi agendada. 

- Data de Conclusão da Entrevista: Data e hora em que a entrevista foi concluída. 

## 

### 5. Tabela: Contratações 

- Armazena informações sobre candidatos que foram contratados. 

- ID Contratação: Identificador único da contratação. 

- ID Candidato: Identificador do candidato contratado. 

- ID Vaga: Identificador da vaga para a qual o candidato foi contratado. 

- Data de Contratação: Data de início do contrato. 

- Salário Inicial: Salário inicial acordado para o contratado. 

- Tipo de Contrato: Tipo de contrato (e.g., CLT, Temporário, Estágio). 

- Data de Aceitação da Oferta: Data e hora em que o candidato aceitou a oferta de emprego. 

##

### 6. Tabela: Avaliações de Candidatos 

Permite o registro das avaliações dos candidatos ao longo do processo seletivo. 

- ID Avaliação: Identificador único da avaliação. 

- ID Candidato: Identificador do candidato avaliado. 

- ID Processo Seletivo: Identificador do processo seletivo relacionado. 

- Critérios de Avaliação: Critérios usados para avaliar o candidato. 

- Pontuação: Pontuação atribuída ao candidato com base nos critérios. 

- Data da Avaliação: Data e hora em que a avaliação foi realizada. 

- Avaliador: Identificador ou nome da pessoa que realizou a avaliação. 

##

### 7. Tabela: Feedbacks 

- Registra feedbacks dados aos candidatos ao longo do processo. 

- ID Feedback: Identificador único do feedback. 

- ID Candidato: Identificador do candidato que recebeu o feedback. 

- ID Vaga: Identificador da vaga para a qual o feedback é relevante. 

- Data do Feedback: Data e hora em que o feedback foi dado. 

- Tipo de Feedback: Tipo de feedback (e.g., Positivo, Negativo, Neutro). 

- Conteúdo do Feedback: Texto com o feedback detalhado para o candidato. 

- Responsável pelo Feedback: Identificador ou nome da pessoa do RH que forneceu o feedback. 

##

### 8. Tabela: Participantes do RH 

- Armazena informações sobre os membros da equipe de RH envolvidos no processo. 

- ID Participante RH: Identificador único do participante do RH. 

- Nome do Participante RH: Nome completo do membro da equipe de RH. 

- Cargo: Cargo do participante na equipe de RH (e.g., Recrutador, Gerente de RH). 

- Processos Seletivos Envolvidos: Lista de processos seletivos em que o participante está envolvido. 

- Feedbacks Dados: Número de feedbacks fornecidos pelo participante. 

##

### 9. Tabela: Ações de Processo 

- Armazena informações sobre todas as ações realizadas dentro do processo seletivo para medir SLA.

- ID Ação: Identificador único da ação. 

- Tipo de Ação: Tipo de ação realizada (e.g., Criação do Processo, Agendamento de Entrevista, Feedback Fornecido). 

- ID Processo Seletivo: Identificador do processo seletivo relacionado à ação. 

- ID Participante RH: Identificador do membro da equipe de RH que realizou a ação. 

- Data e Hora da Ação: Data e hora em que a ação foi realizada.



## Pergunta enviada no dia 06/09/24 12h22 
 
1- Boa tarde Rafael, tudo bem? Tenho mais uma pergunta para você. Como é o ambiente de produção na empresa de vocês? Vocês utilizam VM, nuvem ou docker? Gostaríamos de saber para fins de ciclo de devops 

Backlog do produto, esboço e entregas da sprint 1 enviadas em 08/09/24 

## Pergunta enviada no dia 10/09/24  
 
Boa noite Rafael, tudo bem?Nosso grupo discutiu sobre algumas métricas que poderiam ser importantes para os dashboards, gostaríamos de saber sua opinião sobre elas. Caso alguma seja indispensável gostaríamos de saber. Aqui estão: 
Processos seletivo - Métricas:- Total de vagas 
- localização da vaga (estado) 
- Tempo médio de contratação 
- Taxa de contratação (Candidatos contratados/Total de candidatos) 
- Taxa de retenção 
- Salario médio 
- Número de entrevistas 
- Total de feedbacks 
- Rentabilidade do processo (inversamente proporcional ao tempo em que o processo esta aberto, diretamente proporcional a taxa de ocupação de vagas; fazer isso para todos os processos e normalizar) 
- n° de ocupação de vagas/mês do ano 
- vagas com menores pontuações do candidato - vagas que tem um déficit de candidatos bonsFiltros: 
- Processo seletivo 
- Vagas 
- Estado 
- Usuário do time de recrutamento 
- Data de inicio 
- Data de conclusão 
- Status do processo seletivo 
- Status da vaga 
- Tipo de feedback 
- Taxa de ocupação das vagas (posições preenchidas/posições abertas no período) 

## Pergunta enviada no dia 13/09/24  

Boa noite Rafael, tudo bem? Para essa primeira sprint nós montamos um protótipo do dashboard

Nós temos planos de colocar mais métricas nele nas próximas sprints, mas de início é o que vamos entregar nesta. O Protótipo foi apresentado para a professora Juliana, que concordou com a proposta. Caso tenha alguma dúvida ou sugestão por favor não hesite em mandar. Obrigada 

 
## Repostas do cliente enviadas no dia 05/09/24 
 
Olá @Nicole Souza , bom dia, desculpe pela demora na resposta. Normalmente utilizamos nossas aplicações hospedadas em serviços de aplicativo no Azure.  

Quanto ao Backlog, tudo OK;  

Quanto ao protótipo senti só falta de um filtro mais geral por tempo, acho que seria legal eu conseguir selecionar o período que eu vou analisar, seja o geral ou por exemplo o primeiro semestre do ano; 

Quanto as métricas:  

Localização da vaga;  

Para nós esse ponto não é tão necessário, mas deixaria no escopo por ser uma adição interessante ao produto;  

E finalizando, tudo OK com o protótipo, acho que se adequa bem ao que falamos, percebi até a adiçõ ali dos filtros, boa. 
 

## Brainstorm 


Em um processo seletivo, tem vagas diferentes em questão de cargos e níveis, ou são as mesmas vagas em todos os quesitos?  

As vagas possuem prazo para serem encerradas. O processo seletivo também possui um prazo? Se ele possuir é diferente do prazo das vagas? 

Quais tipos de filtros são mais necessários para os gestores na análise dos dados?  Setor, período, status,  skills, perfil do candidato (gênero, orientação sexual, etnia) 

Vocês precisam de uma métrica mostrando quantas vezes a vaga já foi aberta? 

Quando a vaga não é preenchida, vocês reabrem a mesma vaga ou criam uma vaga nova? Se precisar criar, seria o processo seletivo ao todo ou só a vaga?  

No banco de dados que vocês irão fornecer teremos as qualificações dos candidatos? 

Durante o processo seletivo como a plataforma irá colaborar? Ela vai ajudar somente no acompanhamento dos processos seletivos ou também irá colaborar da contratação?  

 

Confirmar métricas: Vagas, Processo seletivo, Candidatos, aprovados, reprovados, duração do processo, taxa de sucesso (aprovação), 

 

Para criar uma aplicação coerente e funcional, gostaríamos de entender a hierarquia das informações: 

A equipe pro4tech abre um processo seletivo, esse processo pode possuir uma ou mais vagas. Está correto esse entendimento? As vagas dentro de um processo seletivo são todas iguais? o que há de comum entre elas? 

 Nesse primeiro momento, consideramos que a aplicação irá acompanhar 2 informações com as seguintes metricas que serão analisadas: 

Processos seletivos: Total de candidatos, Candidatos aprovados e reprovados, tempo médio de duração, status (Em aberto e finalizado), investimento no processo. 

Vagas: Total de candidatos, Candidato aprovado e reprovados, tempo médio de duração, status (Vaga regular (Dentro do prazo), vaga com prazo expirado, vaga finalizada dentro do prazo, vaga finalizada com atraso), investimento no processo. 

Funcionalidade:  

Dashboard de Processos seletivos - Os usuários terão acesso a um visual com as principais métricas e KPIs acerca dos processos seletivos podendo utilizar filtros para melhor navegação 
 

Dasboard de vagas - Os usuarios terão acesso a um visual com as principais metricas e KPIs acerca das vagas podendo filtrar para melhor navegação 

 

Cadastro de usuário - O gestor RH terá a funcionalidade para cadastrar novos usuarios. Quais as infomações necessarias para o cadastro? 

 

Parametrização dos perfis - Nossa proposta seria a seguinte, o gestor de RH(Admin) tera a possibilidade de criar usuario e criar grupo, ao criar um grupo ele pode adicionar setores e permissões e posteriomente adicionar usuarios a esses grupos e assim permitir que esse usuario tenha acesso a tudo descrito no grupo.  

 

Notificações - Quais serão os gatilhos para as notificações? 

 

Será possível um candidato se candidatar a máis de uma vaga em um mesmo, ou em diferentes processos seletivos?v 

 

Dentro do modelo de tabelas que foi passado, que critério de avaliação serão usados para gerar a pontuação do candidato? 