# desafio-cognito
Segurança em APIs com grupo de usuários do Amazon Cognito

##### Criar  a API:

No AWS API Gateway, crie uma nova API:

- Tipo: REST API;
- Nome: cognito_api_teste
- Create New API: New API
- Description: Descreva brevemente sua API. Item opcional.
- Endpoint Type: Regional
- Botão "Create API"

Após criada a API, criamos um resource para ela:

- Botão "Actions" >> Create new resource >> Dê um nome a ele (Ex: items) >> Create Resource.

O método do Resource será adicionado nas próximas fases.

##### Criar uma tabela de teste no Dynamo DB

No serviço "Dynamo DB", crie uma tabela:

- Botão "Criar Tabela" >> Dar um nome para a Partition Key (Ex: id) >> Dar um nome para a tabela >> Os outros parâmetros são padrão >> Botão "Create Table"

Deixe a tabela aí pronta para as próximas fases.

##### Criar a função Lambda (Função de Backend serverless)

No AWS Lambda, crie uma nova função. Essa função será responsável por inserir dados no Dynamo DB via API.

- Botão "Criar função" >> Opção "Criar do Zero" >> Dar um nome (Usei "teste_put_items_function") >> Verifique se o Node é o atual >> os outros parâmetros são padrão >> Botão "Create Function"

Aqui já temos a visão geral da função criada, com o mapeamento inicial e o código-fonte para teste. Logo, a partir daqui precisaremos fornecer a permissões necessárias para estabelecer a comunicação das funções lambda com o Dynamo DB, assim como qualquer tipo de comunicação entre serviços AWS. Para isso, fazemos uso dos recursos do IAM para fornecer tais permissões de acesso.

Agora vamos inserir o código da função da aplicação na área de código-fonte.

- Coloque o código da função criada na área de código-fonte >> Faça a inspeção do código e as correções necessárias de parâmetros e sintaxe>> Fazer o Deploy (Botão "Deploy")

Agora, vamos tratar das configurações de acesso da função Lambda:

- Ir na aba "Configurações" na área do código-fonte >> opção "Permissões" >> Selecionar a Role >> No subtítulo "Políticas de permissões" , botão "Adicionar políticas" >> Opção "Criar política de linha" >>
- Serviço: Dynamo DB
- Ações: Adicionar ação manualmente >> "putItem" >> Adicionar
- Resources: ARN completo
- Botão "Revisar política" >> Dar nome a política (putItem_politica) >>  Criar política

##### Integrar o API Gateway com a função Lambda para escrever no Dynamo DB

Aqui, precisamos fazer a integração dos dois serviços para que possamos fazer as requisições para escrita no Dynamo DB.

- No API Gateway, vamos criar um método: Botão "Actions" >> POST >> Botão de "Visto" >> 
- No Setup:
- Integration Type: Lambda Fubctions >> Use Lambda Proxy Integration: Selecionar >> Lambda Region: a mesma para todos os serviços que compõem a solução >> Timeout padrão: Selecionar >> Botão "Save" >> Dar permissões: OK
- O mapa de fluxo da requisição é criado.
- Configurar o "Method Request" do mapa >> Deixe como está >> Actions >> Deploy API 
- Testar no Postman >>

##### Criar o Pool de usuários no Cognito

Interface mudou bastante de 2021 até 2023. Pesquisar o entendimento das novas opções. Alguns atributos ficaram subentendidos.