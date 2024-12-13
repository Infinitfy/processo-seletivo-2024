
![prova tecnica](https://private-user-images.githubusercontent.com/122098536/289663385-d1a07217-0131-4687-891b-e5e0327d798c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzQxMDIyOTQsIm5iZiI6MTczNDEwMTk5NCwicGF0aCI6Ii8xMjIwOTg1MzYvMjg5NjYzMzg1LWQxYTA3MjE3LTAxMzEtNDY4Ny04OTFiLWU1ZTAzMjdkNzk4Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMjEzJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTIxM1QxNDU5NTRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xMzQyMGU4MzY1OTBkMGM5M2E3OWU2NWYwMGU3NWUyODI5OTIxMGU4YzRmMTRkOTViNDcwOTBlZDQyMGExM2VhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.CL6rBJNtEn1exeEKqfI4iGTptgcww90eS_WDwm4KRZQ)

# Prova Técnica: Desenvolvimento de Sistema de Gestão Aérea com SAP CAP

## Introdução

Esta prova técnica tem como objetivo avaliar sua habilidade na modelagem de dados, implementação de regras de negócio e desenvolvimento de serviços utilizando o SAP CAP _(Cloud Application Programming)._

Você será responsável por construir um sistema de gestão aérea que inclua funcionalidades para gerenciar **passageiros, voos, reservas e aeronaves**. Para isso, será necessário criar um **schema.cds** detalhado, descrevendo as entidades principais e suas relações.

Além de implementar as entidades e regras de negócio descritas, o candidato deve:

- **Carregar dados iniciais** através de arquivos \`.csv\`.

- **Implementar serviços REST** que atendam às validações e regras de negócio especificadas.

## Instruções Gerais

Utilize **SAP CAP** para implementar o projeto.

Respeite as regras de negócio e as validações descritas.

Marque corretamente as entidades como _"somente leitura"_ quando necessário.

Carregue os dados a partir de arquivos **.csv.**

Desenvolva serviços REST para manipulação e consulta de dados, de acordo com os requisitos.

Modele as entidades no arquivo **\`schema.cds\`**, respeitando as associações, chaves únicas e validações.

Será fornecidos arquivos \`.csv\` com dados para as entidades **Companhia, Aeronave, Aeroporto, HorarioVoo, PropriedadeAeronave e Conexao.**

Passageiro e ReservaPassageiro terá apenas o cabeçalho no .csv.

Adicione lógica de validação no backend para todas as regras de negócio descritas.

Crie exemplos de execução utilizando **Postman** ou similar para testar os serviços.

## **Criação de Serviços:**

Implemente os serviços REST para:

Gerenciar passageiros (CRUD com validações de regras de negócio).

Gerenciar reservas (CRUD com validações de regras de negócio).

Cadastrar voos, Atualizar voos, Consultar voos.

## Modelagem de Dados

O sistema deve implementar as seguintes entidades e características:

## **Entidades e Regras:**

### 1.  **Companhia (somente leitura):**

**\-** Função para Cadastrar Companhia Aérea

\- Representa as companhias aéreas registradas no sistema.

\- Deve conter informações como **ICAO, razão social, CNPJ, telefone e e-mail.**

\- **Chave única** para ICAO, razão social, CNPJ, telefone e e-mail.


### 2. **Aeronave (somente leitura):**

**\-** Função para Cadastrar Aeronave

\- Contém informações detalhadas sobre cada aeronave, incluindo marca, modelo, capacidade e tipo de motor.

\- **Chave única** composta por **marca, modelo e número de série.**


 ### 3 **PropriedadeAeronave (somente leitura):**

\- Define a associação entre uma aeronave e sua companhia proprietária.

\- Inclui informações sobre matrícula e validade de certificados.

\- **Chave única** composta por ID da aeronave e ID da companhia.


 ### **4\. Aeroporto (somente leitura):**

\- Cadastro dos aeroportos, incluindo **ICAO, cidade, estado e país.**

\- Chave única para ICAO.


### **5\. Conexão (somente leitura):**

\- Representa uma rota entre dois aeroportos (origem e destino).

\- Chave única composta pelos IDs de aeroporto de origem e destino.


### **6\. Passageiro:**

\- Cadastro dos passageiros com informações como **CPF, nome, telefone, e-mail e data de nascimento**

\- CPF, telefone e e-mail devem ser **únicos**.

\- **Validação de CPF obrigatório**.

\- Idade mínima de 3 anos para cadastro.

\- Telefone e e-mail devem ser válidos.

### **7\. ReservaPassagem:**

\- Gerencia as reservas feitas pelos passageiros, incluindo informações sobre assento, classe e preço

\- Um assento não pode ser reservado mais de uma vez no mesmo voo.

\- O preço mínimo por classe deve ser respeitado.

\- Apenas passageiros e voos cadastrados podem ser referenciados.

### **8\. HorarioVoo:**

\- Define os horários programados para voos, incluindo associações com companhia, conexão e aeronave.

\- Criar uma entidade para definir os status do voo. (seguindo regra 6 de tarefas práticas logo abaixo)

\- Horário de chegada deve ser **posterior** ao horário de partida.

\- O número total de reservas não pode exceder a capacidade máxima da aeronave.

## Regras de Negócio

## **Passageiro**

**1\. Cadastro único:**

\- O CPF, e-mail e telefone do passageiro devem ser únicos.

\- **Erro:** Retorne um erro caso haja duplicidade ao cadastrar ou atualizar um passageiro.

**2\. Validação de CPF:**

\- O CPF deve ser validado com base no algoritmo oficial de dígitos verificadores.

**Referência para validação:** [**https://homepages.dcc.ufmg.br/~rodolfo/aedsi-2-10/regrasDigitosVerificadoresCPF.html**](https://homepages.dcc.ufmg.br/~rodolfo/aedsi-2-10/regrasDigitosVerificadoresCPF.html)

\- **Erro:** Retorne um erro caso o CPF seja inválido.

**3\. Idade mínima:**

\- Passageiros devem ter ao menos 3 anos no momento do cadastro.

\- **Erro:** Retorne um erro caso a idade mínima não seja atendida.

ReservaPassagem

**4\. Assento único por voo:**

\- Um assento específico não pode ser reservado por mais de um passageiro no mesmo voo.

\- **Erro:** Retorne um erro caso o assento já esteja ocupado.

**5\. Voo deve existir:**

\- Reservas só podem ser feitas para horários de voo previamente cadastrados.

**\- Erro:** Retorne um erro caso o ID do horário de voo não exista.

**6\. Passageiro deve estar cadastrado:**

\- Reservas só podem ser feitas por passageiros previamente cadastrados.

**\- Erro:** Retorne um erro caso o ID do passageiro não exista.

**7\. Preço mínimo por classe:**

\- O preço da reserva deve ser maior ou igual ao mínimo permitido para a classe.

\- Econômica: R$ 200.

\- Executiva: R$ 500.

**\- Erro:** Retorne um erro caso o preço seja inválido.

**8\. Cancelamento de reservas:**

\- Reservas só podem ser canceladas se o voo não estiver em curso ou concluído.

**\- Erro:** Retorne um erro caso a condição não seja atendida.

## Criação de Voos

Ao criar um novo voo:

**Não é permitido definir os seguintes campos:**

\- Horário de partida real.

\- Horário de chegada real.

\- Status diferente de **'AGUARDANDO'**.

**Motivo:** Quando um voo é criado, ele ainda não ocorreu, logo não pode ter horários reais ou status que indiquem progresso.

**Atualização de Voos**

Ao atualizar um voo:

\- Apenas os seguintes campos podem ser alterados diretamente:

\- Horário de partida previsto.

\- Horário de chegada previsto.

\- Aeronave.

**Motivo:** Essas são atualizações básicas de informações previstas.

Para modificar o status de um voo, deve ser usada uma função separada, conforme descrito abaixo.

**Atualização do Status do Voo**

A atualização do status de um voo deve ser realizada por uma função específica chamada, por exemplo, **'atualizarStatus'.** Essa função seguirá as seguintes regras:

**Transição de Status Permitidas**

De **'AGUARDANDO':**

**Pode ser alterado para:**

\- **'EM CURSO':** Indica que o voo decolou.

\- Deve ser informado o horário real de partida.

\- Deve ser informado a situação real da partida.

\- '**CANCELADO'**: Indica que o voo foi cancelado.

\- Não pode ter horários reais definidos para partida ou chegada.

\- Não pode ser alterado para outros status diretamente.

De **'EM CURSO':**

**Pode ser alterado para:**

\- **'CONCLUÍDO':** Indica que o voo foi finalizado.

\- Deve ser informado o horário real de chegada.

\- Deve ser informado a situação real da chegada.

\- Não pode ser alterado para **'CANCELADO'** ou qualquer outro status.

**Restrições e Motivações**

\- A transição de **'EM CURSO'** para **'CANCELADO'** não faz sentido e é proibida.

\- Outros status fora do fluxo descrito só podem ocorrer em situações excepcionais (como acidentes), que devem ser tratadas separadamente.

## Critérios de Avaliação

**1\. Qualidade do código:**

\- Organização, clareza e legibilidade.

**2\. Cumprimento das regras de negócio:**

\- Implementação correta de todas as validações.

**3\. Conformidade com o SAP CAP:**

\- Uso adequado do framework e seus padrões.

Boa sorte!
