# sync-veracode-team-users.ps1

## Descrição
Script PowerShell utilizado para adicionar usuários a times na Veracode utilizando a API de Identity.  
A atualização é feita de forma incremental, garantindo que novos usuários sejam adicionados ao time sem remover os membros já existentes.

## Funcionamento
O script executa as seguintes etapas:
1. Consulta todos os usuários da organização.
2. Consulta todos os times disponíveis.
3. Identifica o ID do time a partir do nome informado.
4. Atualiza o time adicionando o usuário especificado.

## Parâmetros de entrada
No script devem ser definidos dois valores:
- **userEmail** – email do usuário que será adicionado ao time  
- **teamName** – nome do time na Veracode  

Exemplo:
`$userEmail = "usuario@empresa.com"`  
`$teamName = "DEMOs"`

## Atualização do time
A associação do usuário é realizada utilizando o endpoint:
`PUT /api/authn/v2/teams/{teamID}`
A chamada utiliza os parâmetros:
- `partial=true`
- `incremental=true`
Esses parâmetros permitem atualizar apenas parte da configuração do time e adicionar usuários sem substituir a lista atual de membros.

## Resultado esperado
Quando executado com sucesso, o script exibirá:
`SUCESSO: Usuário usuario@empresa.com associado ao time DEMOs`
Caso a associação não seja confirmada pela API, o script retornará uma mensagem indicando erro.

## Requisitos
- PowerShell  
- HTTPie (`http`)  
- Credenciais configuradas para autenticação Veracode HMAC  
- Permissão de acesso à API da organização