---
page_type: sample
products:
- ms-graph
languages:
- csharp
description: "可通过 Microsoft Graph 安全性 API 访问的安全性数据是非常敏感的，因此受到权限和 Azure AD 角色的保护。"
extensions:
  contentType: samples
  technologies:
  - Mcirosoft Graph
  - Microsoft Graph
  services:
  - Security 
  createdDate: 4/19/2018 10:35:33 AM
---
# C# Microsoft Graph 身份验证示例应用程序

## 简介

可通过 Microsoft Graph 安全性 API 访问的安全性数据是非常敏感的，因此受到权限（也称为作用域）和 Azure AD (AAD) 角色的保护。
Microsoft Graph 安全性 API 强制执行身份验证和授权 (AuthNZ)，以保护其可访问的敏感数据。在 Microsoft Graph 安全性 API 技术社区中，[了解调用 Microsoft Graph 安全性 API 时的身份验证](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2)一文更详细地介绍了这一点 

## Microsoft Graph 中的身份验证和授权

Microsoft Graph 安全性 API 支持两种类型的应用程序身份验证和授权（也称为 AuthNZ）：
* **仅限应用程序的授权**，其中没有已登录的用户（如标准 SIEM 或自动化方案）。
在这里，授予应用程序的权限/作用域将确定授权
* **用户委派的授权**，其中有一个属于 AAD 租户成员的用户已登录。

若要调用 Microsoft Graph 安全性 API，该用户必须属于 AAD 安全读取者受限管理员角色，所需的权限（也称为作用域）必须已在[**应用程序注册**](https://go.microsoft.com/fwlink/?linkid=2083908)中定义，并且应用程序必须由 Azure AD 租户管理员授予所需的权限。[针对 ASP.NET 4.6 (REST) 的 Microsoft Graph 安全性 API](https://github.com/microsoftgraph/aspnet-security-api-sample) 中也介绍了此过程

此示例 Graph 身份验证应用程序通过显示身份验证令牌的内容以及响应内容和标头，在调用 Microsoft Graph 安全性 API 时，提供了对这两种 AuthNZ 类型的更多可见性。
该应用程序有一个选项卡用于用户委派的身份验证，另一个则用于仅限应用程序的身份验证。
它还有一个“**帮助**”选项卡，其中包含一些常见的错误和修补程序。
通过该应用，你还可以输入自己选择的 REST 查询，以便能够查看相应响应。 

## 运行应用程序所需的信息

运行 Graph 身份验证应用所需的信息：
![对于两种类型的身份验证]：
* **应用 ID** - 来自应用程序注册（用户委派的身份验证只需要该信息）
![对于仅限应用程序的身份验证]（除了应用 ID，还需要其他信息）
* **应用秘钥**（也称为应用密码） - 同样来自应用程序注册
* **租户 ID**（Azure AD 租户的 ID）- 这是所有 Microsoft Graph 安全性 API 实体的强制属性（响应）

## Graph 身份验证示例应用入门

 1. 下载或克隆 Microsoft Graph 身份验证示例。

 2. 如果尚未注册应用程序、定义所需权限并显式授予这些权限，请按照[针对 ASP.NET 4.6 (REST) 的 Microsoft Graph 安全性 API](https://github.com/microsoftgraph/aspnet-security-api-sample) 中的说明进行操作。（请务必在注册示例应用程序时保存应用密钥 \[也称为应用密码]）。

 3. 如果正在运行 ASP.NET 示例，请务必在应用程序注册页上添加**本机应用程序**。这是 Microsoft Graph 安全性身份验证示例应用所必需的。
 
 ## 配置并运行示例应用
 1。打开 Graph\_Security\_API\_Auth\_Sample 项目。
 
 2. 按 F5 生成并运行此示例。这将还原 NuGet 包依赖项，并打开该应用程序。

   >如果在安装包时出现任何错误，请确保你放置该解决方案的本地路径并未太长/太深。将解决方案移动到更接近驱动器根目录的位置将会解决此问题。

## 使用 Microsoft Graph 身份验证示例应用

1. 启动示例应用将显示示例应用的 UI

![Graph 身份验证示例应用 UI](readme-images/Default_screen.png)

2. 在页面顶部的文本框中输入应用 ID

## 测试用户委派的授权

1. 若要运行用户委派的身份验证流，请单击“**发送请求**”按钮。系统将打开 Microsoft 身份验证对话框。

2. 使用你的工作或学校帐户登录。

3. 示例应用 UI 将在左侧窗格中显示身份验证令牌，如下所示 

![Graph 身份验证示例 - 用户委派的授权](readme-images/User_delegated_auth.png)

* **scp** 属性（突出显示）显示授予用户的作用域或权限
* **wids** 属性显示已登录用户所属的用户组的 GUID

4. 对 Graph URL 文本框中显示的 REST 查询的响应（默认值返回最前面 \[即最新] 的警报）。这是从 Microsoft Graph 安全性 API 接收到的完整 JSON 响应。单击响应部分的“**标头**”选项卡将显示响应的 HTTP 标头。

* 注意：可通过修改“**Graph URL**”文本框中的 URL 来更改提交到 Microsoft Graph 安全性 API 的 REST 查询

## 测试仅限应用程序的授权（无登录用户）

1. 若要运行仅限应用程序的身份验证流，需要执行以下操作：

* 输入注册应用时生成的应用密钥（或应用密码）。
* 输入 AAD 租户 ID（可从上方用户委派的身份验证流的响应中的“azureTenantId”属性中获取此 ID）
* 单击“**发送请求**”按钮。 

2. 示例应用 UI 将在左侧窗格中显示仅限应用程序的身份验证令牌，如下所示 

![Graph 身份验证示例 - 仅限应用程序的授权](readme-images/App_only_auth.png)

* 此处的 **roles** 属性（突出显示）显示授予应用程序的作用域或权限
* 对 REST 查询的 JSON 响应与前面的示例相同

## “帮助”选项卡

“**帮助**”选项卡中包含一些常见错误及其发生的原因和解决（修复）方法 

![Graph 身份验证示例 -“帮助”选项卡](readme-images/Help_tab.png)

## 资源

文档：
* [了解调用 Microsoft Graph 安全性 API 时的身份验证](https://techcommunity.microsoft.com/t5/Using-Microsoft-Graph-Security/Authorization-and-Microsoft-Graph-Security-API/m-p/184376#M2)
* [Microsoft Graph 权限引用](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference)

其他示例：
* [针对 ASP.NET 4.6 (REST) 的 Microsoft Graph 安全性 API](https://github.com/microsoftgraph/aspnet-security-api-sample)
