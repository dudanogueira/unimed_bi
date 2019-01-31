# Unimed BI
Sistema de BI para Unimeds que usam Cardio e opcionalmente UERP


## Instruções de Uso

1 - Instale os seguintes Softwares:
Spoon: https://sourceforge.net/projects/pentaho/files/latest/download?aliId=137249511
Mondrian Schema WorkBench: https://sourceforge.net/projects/mondrian/files/schema%20workbench/3.14.0/
Docker:  https://docs.docker.com/get-started/
Docker Compose: https://docs.docker.com/compose/install/

2 - Execute o container, dentro da pasta:
- docker-compose up
Isso irá executa dois containers. Um na porta 8085, com o Pentaho Business Analytics, e outro com o Postgres, na porta 5432, 
que será usado como nosso DatawareHouse

3 - Abra o Spoon (PENTAHO DATA INTEGRATOR - PDI), e configura como repositório a pasta "spoon" deste repositório

4 - Abra o JOB PROCESSA CARDIO CARDIO

5 - Acesse a aba "VIEW" > "CONEXÕES" e edite cada uma das conexões, usando as configurações do seu ambiente. Crie o banco do BI, caso necessário.

6 - Clique no botão "Generate the SQL needed to run this job", para criar todas as tabelas que receberão as dimensões e fatos do Cardio

7 - Execute o JOB (botão "play")

8 - Aguarde...

9 - Execute o programa Mondrian Schema Workbench

10 - Abra o xml (File / Open...) do cubo do Cardio (mondrian/CARDIO.mondrian.xml)

11 - Configure as conexões do cubo (Options / Connections) com as informações do seu ambiente

12 - Publique o seu cubo no servidor do Pentaho BA (File / Publish...)

13 - Acesse o servidor do Pentaho BA, e crie visualizações e paineis.

## CUBOS PARA CARDIO
- Custos Assistenciais
  - Fato: Cada Item Evento
  - Medidas: Valor Pago (ao prestador), Valor Cobrado (do beneficiário), Quantidade
  - Dimensão Tempo (Ano, Trimestre, Mês)
  - Unimed de Atendimento (UF, Cidade, Nome)
  - Unimed de Cobrança (UF, Cidade, Nome)
  - Procedimento (Nome, Grupo, Classe, Codigo)
  - Natureza da Admissão
  - Beneficiário (Sexo, Idade, Faixa ANS), 
  - Contrato (Grupo, Classe)
  - Solicitante (Nome, Classe, UF, Cidade)
- Receitas (em breve)

## CUBOS PARA UERP
- Protocolos de Atendimento
  - Fato: Cada protocolo gerado por atendimento
  - Medidas: Quantidade
  - Dimensão Tempo (Ano, Trimestre, Mês)
  - Dimensão Tipo
  - Dimensão Categoria
  - Dimensão Natureza (beneficiário local em intercambio, beneficiário local em local, beneficiario intercambio em local)
  - Dimensão Canal de Atendimento
