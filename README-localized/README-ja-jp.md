---
page_type: sample
products:
- ms-graph
languages:
- csharp
description: "Microsoft Graph Security API を介してアクセス可能なセキュリティ データは非常に機密性が高いため、アクセス許可と Azure AD ロールによって保護されています。"
extensions:
  contentType: samples
  technologies:
  - Mcirosoft Graph
  - Microsoft Graph
  services:
  - Security 
  createdDate: 4/19/2018 10:35:33 AM
---
# C# Microsoft Graph 認証のサンプル アプリケーション

## 概要

Microsoft Graph Security API を介してアクセス可能なセキュリティ データは非常に機密性が高いため、アクセス許可 (スコープとも呼ばれる) と Azure AD (ADD) ロールによって保護されています。Microsoft Graph Security API は、認証と承認 (AuthNZ) を実施して、アクセス可能にする機密データを保護します。これについては、Microsoft Graph Security API Tech Community
の「[Understanding authorization when calling the Microsoft Graph Security API (Microsoft Graph Security API を呼び出すときの承認について)](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2)」で詳しく説明しています。 

## Microsoft Graph での認証と承認

Microsoft Graph Security API は、2 種類のアプリケーション認証と承認 (AuthNZ とも呼ばれる) をサポートしています:
* サインインしているユーザーがいない場合の**アプリケーションのみの承認**
(たとえば、標準の SIEM や自動化シナリオです)。ここで、アプリケーションに付与されたアクセス許可/スコープによって、承認が決定されます
* AAD テナントのメンバーであるユーザーがサインインする場合の**ユーザー委任承認**。

Microsoft Graph Security API を呼び出すには、ユーザーは AAD セキュリティ閲覧者制限付き管理者ロールに属し、必要なアクセス許可 (スコープとも呼ばれる) が[**アプリケーションの登録**](https://go.microsoft.com/fwlink/?linkid=2083908)で定義され、Azure AD テナント管理者がアプリケーションに必要なアクセス許可を付与する必要があります。このプロセスは、「[Microsoft Graph Security API Sample for ASP.NET 4.6 (REST) (ASP.NET 4.6 (REST) 用 Microsoft Graph Security API のサンプル)](https://github.com/microsoftgraph/aspnet-security-api-sample)」でも説明されています。

このサンプルの Graph 認証アプリケーションは、Microsoft Graph Security API を呼び出すときに、認証トークンのコンテンツ、応答のコンテンツおよびヘッダーを表示することで、両方のタイプの AuthNZ の可視性を向上させます。
アプリケーションには、ユーザー委任認証用のタブとアプリケーションのみの認証用のタブがあります。
また、いくつかの一般的なエラーと修正プログラムを含む
[**ヘルプ**] タブもあります。このアプリでは、選択した REST クエリを入力して、応答を表示することもできます。 

## アプリケーションを実行するために必要な情報

Graph 認証アプリを実行するために必要な情報:
！[両方のタイプの認証]:
* **アプリ ID** - アプリケーションの登録から (ユーザー委任認証に必要なすべて)
![アプリケーションのみの認証] (アプリ ID に加えて)
* **アプリ キー** (アプリ シークレットとも呼ばれる) - こちらもアプリケーションの登録から
* **テナント ID** (Azure AD テナントの ID) - これはすべての Microsoft Graph Security API エンティティにおける必須プロパティです (応答)

## Graph 認証のサンプル アプリの使用を開始する

 1. Microsoft Graph 認証のサンプルをダウンロードするか、クローンを作成します。

 2. アプリケーションを登録していない、必要なアクセス許可を定義していない、これらのアクセス許可を明示的に付与していない場合は、「[Microsoft Graph Security API Sample for ASP.NET 4.6 (REST) (ASP.NET 4.6 (REST) 用 Microsoft Graph Security API のサンプル)](https://github.com/microsoftgraph/aspnet-security-api-sample)」の指示に従ってください。(サンプル アプリケーションを登録するときは、必ず アプリ キー (アプリ シークレットとも呼ばれる) を保存してください)。

 3. ASP.NET サンプルを実行している場合は、アプリケーションの登録ページに必ず**ネイティブ アプリケーション**を追加してください。これは、Microsoft Graph セキュリティ認証のサンプル アプリに必要です。
 
 ## サンプル アプリ
 1 を構成して実行します。Graph\_Security\_API\_Auth\_Sample プロジェクトを開きます。
 
 2. F5 キーを押して、サンプルをビルドして実行します。これにより、NuGet パッケージの依存関係が復元され、アプリケーションが開きます。

   >パッケージのインストール中にエラーが発生した場合は、ソリューションを保存したローカル パスが長すぎたり深すぎたりしていないかご確認ください。この問題は、ソリューションをドライブのルート近くに移動すると解決します。

## Microsoft Graph 認証のサンプル アプリの使用

1. サンプル アプリを起動すると、サンプル アプリの UI が表示されます

![Graph 認証のサンプル アプリの UI](readme-images/Default_screen.png)

2. ページ上部のテキスト ボックスにアプリ ID を入力します

## ユーザー委任承認のテスト

1. ユーザー委任認証フローを実行するには、[**リクエストの送信**] ボタンをクリックします。Microsoft 認証ダイアログが開きます。

2. 職場または学校のアカウントを使用してサインインします。

3. サンプル アプリの UI では、以下に示すように、左側のウィンドウに認証トークンが表示されます 

![Graph 認証のサンプル - ユーザー委任承認](readme-images/User_delegated_auth.png)

* **scp** プロパティ (強調表示) は、ユーザーに付与されたスコープまたはアクセス許可を示します
* **wids** プロパティには、サインインしているユーザーが属するユーザー グループの GUID が表示されます

4. [Graph URL] テキスト ボックスに表示される REST クエリへの応答 (既定値は最上位、つまり最新のアラートを返します)。これは、Microsoft Graph Security API から受信した完全な JSON 応答です。応答の [**ヘッダー**] タブをクリックすると、応答の HTTP ヘッダーが表示されます。

* 注:[**Graph URL**] テキスト ボックスの URL を編集して、Microsoft Graph Security API に送信された REST クエリを変更できます

## アプリケーションのみの承認のテスト (サインイン ユーザーなし)

1. アプリケーションのみの認証フローを実行するには、次の操作を行う必要があります。

* アプリの登録時に生成されたアプリ キー (またはアプリ シークレット) を入力します。
* AAD テナント ID を入力します (上記のユーザー委任認証フローの応答で "azureTenantId" プロパティから取得できます)
* [**リクエストの送信**] ボタンをクリックします。 

2. サンプル アプリの UI では、以下に示すように、左側のウィンドウにアプリケーションのみの認証トークンが表示されます 

![Graph 認証のサンプル - アプリケーションのみの承認](readme-images/App_only_auth.png)

* ここで、**roles** プロパティ (強調表示) は、アプリケーションに付与されたスコープまたはアクセス許可を示します
* REST クエリに対する JSON 応答は、前の例と同じです

## [ヘルプ] タブ

[**ヘルプ**] タブには、いくつかの一般的なエラー、発生する理由、および解決 (修正) する方法が含まれています 

![Graph 認証のサンプル - [ヘルプ] タブ](readme-images/Help_tab.png)

## リソース

ドキュメント:
* [Understanding authorization when calling the Microsoft Graph Security API (Microsoft Graph Security API を呼び出すときの承認について)](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2) * [Microsoft Graph のアクセス許可のリファレンス](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference)

その他のサンプル: 
* 「[Microsoft Graph Security API Sample for ASP.NET 4.6 (REST) (ASP.NET 4.6 (REST) 用 Microsoft Graph Security API のサンプル)](https://github.com/microsoftgraph/aspnet-security-api-sample)」
