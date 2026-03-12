# Automação de Sincronização de Times e Usuários – Veracode

## Visão Geral
Este projeto contém um conjunto de scripts PowerShell utilizados para automatizar a organização de **times, aplicações e usuários** dentro da plataforma Veracode por meio de sua API.
O objetivo é permitir que essas associações sejam mantidas de forma consistente e repetível, reduzindo atividades manuais na interface da plataforma e facilitando processos de governança e administração.
O projeto é composto por **dois scripts principais**, cada um responsável por um tipo específico de sincronização.

---

# Estrutura do Projeto
Os scripts trabalham de forma complementar e utilizam a **API de Identity e AppSec da Veracode**, com autenticação HMAC.

## 1. Sincronização de Times em Aplicações
Este script é responsável por associar **times a aplicações** dentro da Veracode.
Ele executa as seguintes etapas:
1. Recupera a lista completa de **Application Profiles** da organização.
2. Recupera a lista de **times** existentes.
3. Identifica os IDs internos necessários (GUID da aplicação e GUID do time).
4. Atualiza a aplicação para associá-la ao time correspondente.
Essa associação é importante para:
- controle de acesso
- organização de responsabilidades
- governança das análises de segurança

---
## 2. Sincronização de Usuários em Times

O segundo script é responsável por adicionar **usuários a times existentes**.
O fluxo executado é:
1. Recuperar todos os **usuários** da organização.
2. Recuperar todos os **times disponíveis**.
3. Identificar o **ID do time** desejado.
4. Atualizar o time adicionando o usuário informado.
A atualização utiliza os parâmetros:
- `partial=true`
- `incremental=true`
Isso garante que novos usuários sejam adicionados ao time **sem remover os membros já existentes**.

---

# Funcionamento Geral

Ambos os scripts seguem o mesmo padrão de implementação:
1. **Consulta à API com paginação**  
   Para garantir que todos os registros da organização sejam recuperados.
2. **Resolução de identificadores internos**  
   Conversão de nomes (times, aplicações ou usuários) para os IDs utilizados pela API.
3. **Atualização via API**  
   Execução das chamadas necessárias para realizar as associações desejadas.
4. **Validação da resposta**  
   Verificação da resposta retornada pela API para confirmar se a operação foi concluída corretamente.

---

# Benefícios da Automação
A utilização desses scripts permite:
- padronizar a gestão de times e usuários
- reduzir operações manuais na interface da plataforma
- facilitar integrações com processos internos de governança
- possibilitar automações maiores envolvendo CI/CD ou gestão de identidades

---

# Requisitos

Para executar os scripts é necessário:
- PowerShell
- ferramenta `http` (HTTPie)
- credenciais configuradas para autenticação **Veracode HMAC**
- acesso à API da organização na Veracode

---

# Considerações
Esses scripts foram projetados para serem simples de adaptar e podem ser utilizados como base para automações maiores envolvendo:
- provisionamento de usuários
- organização de times
- integração com processos internos de gestão de aplicações