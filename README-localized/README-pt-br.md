---
page_type: sample
products:
- ms-graph
languages:
- csharp
description: "Os dados de segurança acessíveis por meio da API de Segurança do Microsoft Graph são totalmente confidenciais e, portanto, protegidos por permissões e funções do Azure AD."
extensions:
  contentType: samples
  technologies:
  - Mcirosoft Graph
  - Microsoft Graph
  services:
  - Security 
  createdDate: 4/19/2018 10:35:33 AM
---
# Aplicativo de exemplo de Autenticação do Microsoft Graph em C#

## Introdução

Os dados de segurança acessíveis por meio da API de Segurança do Microsoft Graph são totalmente confidenciais e, portanto, protegidos por permissões (também conhecidas como escopos) e funções do AAD (Azure AD). A API de Segurança do Microsoft Graph impõe autenticação e autorização (AuthNZ) para proteger os dados confidenciais que ela torna acessíveis.
Isso é documentado em mais detalhes em [Entender a autorização ao chamar a API de Segurança do Microsoft Graph](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2) na Tech Community da API de Segurança do Microsoft Graph 

## Autenticação e autorização no Microsoft Graph

A API de Segurança do Microsoft Graph dá suporte a dois tipos de autorização e autenticação de aplicativos (também conhecidas como AuthNZ):
* **Autorização somente para o aplicativo**, em que não há nenhum usuário conectado (por exemplo, um SIEM padrão ou um cenário de automação).
Aqui, as permissões/os escopos concedidos ao aplicativo determinam a autorização
* **Autorização delegada ao usuário**, em que um usuário que é membro do locatário do AAD está conectado.

Para chamar a API de Segurança do Microsoft Graph, o usuário deve pertencer à função de Administrador limitado do Leitor de segurança do AAD, as permissões necessárias (também conhecidas como escopos) devem ser definidas no [**registro do aplicativo**](https://go.microsoft.com/fwlink/?linkid=2083908), e o aplicativo deve receber as permissões necessárias pelo administrador de locatários do Azure AD. Esse processo também é descrito no [Exemplo de API de Segurança do Microsoft Graph para ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample)

Esse exemplo de aplicativo de Autenticação do Graph oferece mais visibilidade quanto aos dois tipos de AuthNZ ao chamar a API de Segurança do Microsoft Graph, exibindo o conteúdo do token de autenticação, bem como o conteúdo da resposta e os cabeçalhos.
O aplicativo tem uma guia para Autenticação delegada ao usuário e outra para Autenticação somente para o aplicativo.
Ele também possui uma guia **Ajuda**, com alguns erros e correções comuns.
O aplicativo também permite que você insira a consulta REST de sua escolha para poder ver a resposta. 

## Informações necessárias para executar o aplicativo

Informações necessárias para executar o aplicativo de Autenticação do Graph:
![Para os dois tipos de autenticação]:
* **ID do aplicativo** – do registro do aplicativo (tudo o que você precisa para a Autenticação delegada ao usuário)
![Para autenticação somente para o aplicativo] (além da ID do aplicativo)
* **Chave do aplicativo** (também conhecida como Segredo do aplicativo) – também do registro do aplicativo
* **ID do locatário** (ID do seu locatário do Azure AD) – essa é uma propriedade obrigatória de qualquer entidade da API de Segurança do Microsoft Graph (resposta)

## Introdução ao aplicativo de exemplo de Autenticação do Graph

 1. Baixe ou clone o aplicativo de exemplo de Autenticação do Microsoft Graph.

 2. Se você não registrou um aplicativo, não definiu as permissões necessárias nem concedeu explicitamente essas permissões, siga as instruções no [Exemplo de API de Segurança do Microsoft Graph para ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample) para fazer isso. (Não se esqueça de salvar a Chave do aplicativo (também conhecida como Segredo do aplicativo) ao registrar o exemplo).

 3. Adicione o **aplicativo nativo** na página de registro do aplicativo se você estiver executando o exemplo do ASP.NET. Isso é necessário para o aplicativo de exemplo de Autenticação de Segurança do Microsoft Graph.
 
 ## Configurar e executar o aplicativo de exemplo
 1. Abra o projeto Graph\_Security\_API\_Auth\_Sample.
 
 2. Pressione F5 para criar e executar o exemplo. Isso restaurará dependências do pacote NuGet e abrirá o aplicativo.

   >Caso receba mensagens de erro durante a instalação de pacotes, verifique se o caminho para o local onde você colocou a solução não é muito longo ou extenso. Você resolverá esse problema colocando a solução junto à raiz da unidade.

## Usar o aplicativo de exemplo de Autenticação do Microsoft Graph

1. Iniciar o aplicativo de exemplo exibirá a interface do usuário dele

![Interface do usuário do aplicativo de exemplo de Autenticação do Graph](readme-images/Default_screen.png)

2. Informe a ID do aplicativo na caixa de texto na parte superior da página

## Testar a Autorização delegada ao usuário

1. Para executar o fluxo da Autenticação delegada ao usuário, clique no botão **Enviar solicitação**. A caixa de diálogo de autenticação da Microsoft será aberta.

2. Entre com sua conta corporativa ou de estudante.

3. A interface do usuário do aplicativo de exemplo exibirá o token de autenticação no painel esquerdo, como vemos abaixo 

![Exemplo de Autenticação do Graph – Autorização delegada ao usuário](readme-images/User_delegated_auth.png)

* A propriedade **scp** (destacada) mostra os escopos ou permissões concedidos ao usuário
* A propriedade **wids** mostra os GUIDs dos grupos de usuários aos quais o usuário conectado pertence

4. A resposta à consulta REST que aparece na caixa de texto URL do Graph (seu valor padrão retorna o alerta superior, ou seja, o mais recente). Essa é a resposta JSON completa recebida da API de Segurança do Microsoft Graph. Clicar na guia **Cabeçalho** da resposta exibe os cabeçalhos HTTP da resposta.

* Observação: você pode alterar a consulta REST enviada à API de Segurança do Microsoft Graph editando o URL na caixa de texto **URL do Graph**

## Testar a Autorização somente para o aplicativo (nenhum usuário conectado)

1. Para executar o fluxo da Autenticação somente para o aplicativo, você precisa:

* Informar a Chave do aplicativo (ou Segredo do aplicativo) gerada quando você registrou seu aplicativo.
* Informar a ID do locatário do AAD (você pode obtê-la na propriedade "azureTenantId" na resposta do fluxo de Autenticação delegada ao usuário acima)
* Clique no botão **Enviar solicitação**. 

2. A interface do usuário do aplicativo de exemplo exibirá o token da Autenticação somente para o aplicativo no painel esquerdo, como vemos abaixo 

![Aplicativo de exemplo de Autenticação do Graph – Autorização somente para o aplicativo](readme-images/App_only_auth.png)

* Aqui, a propriedade **roles** (destacada) mostra os escopos ou permissões concedidos ao aplicativo
* A resposta JSON à consulta REST é a mesma que no exemplo anterior

## A guia Ajuda

A guia **Ajuda** contém alguns erros comuns, o motivo pelo qual eles ocorrem e maneiras de resolvê-los (corrigi-los) 

![Exemplo de Autenticação do Graph – guia Ajuda](readme-images/Help_tab.png)

## Recursos

Documentação:
* [Entender a autorização ao chamar a API de Segurança do Microsoft Graph](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2)
* [Referência de permissões do Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference)

Outros exemplos:
* [Exemplo de API de Segurança do Microsoft Graph para ASP.NET 4.6 (REST)](https://github.com/microsoftgraph/aspnet-security-api-sample)
