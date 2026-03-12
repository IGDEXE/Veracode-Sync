# sync-veracode-app-teams.ps1

## Descrição
Script PowerShell utilizado para associar times a aplicações na Veracode utilizando a API AppSec.
O script permite automatizar a organização de **Application Profiles**, garantindo que uma aplicação esteja vinculada ao time responsável.

## Funcionamento
O script executa as seguintes etapas:
1. Consulta todos os Application Profiles da organização.
2. Consulta todos os times disponíveis.
3. Identifica o GUID da aplicação a partir do nome informado.
4. Identifica o GUID do time a partir do nome informado.
5. Atualiza a aplicação adicionando o time correspondente.

## Parâmetros de entrada
No script devem ser definidos dois valores:
- **appName** – nome da aplicação na Veracode  
- **teamName** – nome do time que será associado  

Exemplo:
`$appName = "NodeGoat-JS-MB"`  
`$teamName = "DEMOs"`

## Atualização da aplicação
A associação do time é realizada utilizando o endpoint:
`PATCH /appsec/v1/applications/{appGUID}`
A chamada envia o campo `add_teams`, que inclui o GUID do time na lista de times associados à aplicação.

## Resultado esperado
Quando executado com sucesso, o script exibirá:
`SUCESSO: Time DEMOs associado à aplicação NodeGoat-JS-MB`
Caso a associação não seja confirmada pela API, o script retornará uma mensagem indicando erro.

## Requisitos
- PowerShell  
- HTTPie (`http`)  
- Credenciais configuradas para autenticação Veracode HMAC  
- Permissão de acesso à API da organização