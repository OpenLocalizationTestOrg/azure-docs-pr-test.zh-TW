---
title: "所做的 aaaChanges tooa MVC 專案，當您連接 tooAzure AD |Microsoft 文件"
description: "描述使用 Visual Studio 連接的服務連線 tooAzure AD 時所採取的 tooyour MVC 專案"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>哪些情形的 toomy MVC 專案 （Visual Studio Azure Active Directory 已連線服務）？
> [!div class="op_single_selector"]
> * [開始使用](vs-active-directory-dotnet-getting-started.md)
> * [發生什麼情形](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>已加入參考
### <a name="nuget-package-references"></a>NuGet 封裝參考
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>.NET 參考
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>已加入程式碼
### <a name="code-files-were-added-tooyour-project"></a>程式碼檔案加入 tooyour 專案
驗證啟動類別**App_Start/Startup.Auth.cs**已加入 tooyour 專案包含 Azure AD 驗證的啟動邏輯。 另外也已加入控制器類別 Controllers/AccountController.cs，內含 **SignIn()** 和 **SignOut()** 方法。 最後，已加入部分檢視 **Views/Shared/_LoginPartial.cshtml**，內含 SignIn/SignOut 的動作連結。

### <a name="startup-code-was-added-tooyour-project"></a>啟始程式碼已加入 tooyour 專案
如果您已經在專案中啟動類別，hello**組態**方法太更新的 tooinclude 呼叫**ConfigureAuth(app)**。 否則，請啟動類別已加入 tooyour 專案。

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>app.config 或 web.config 有新的組態值
已加入下列組態項目 hello。

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>建立 Azure Active Directory (AD) 應用程式
Azure AD 應用程式已建立您 hello 精靈中選取的 hello 目錄中。

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>如果在簽*停用個別使用者帳戶驗證*，toomy 專案所做其他變更？
NuGet 封裝參考會被移除，檔案也會移除並加以備份。 根據您的專案 hello 狀態，您可能必須 toomanually 移除其他參考或檔案，或修改為適當的程式碼。

### <a name="nuget-package-references-removed-for-those-present"></a>移除的 NuGet 封裝參考 (如果存在)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>備份和移除的程式碼檔案 (如果存在)
每個下列檔案已備份，並且從 hello 專案中移除。 備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>備份的程式碼檔案 (如果存在)
下列每個檔案會在取代之前備份。 備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>如果在簽*讀取目錄資料*，toomy 專案所做其他變更？
已加入其他參考。

### <a name="additional-nuget-package-references"></a>其他 NuGet 封裝參考
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>其他 .NET 參考
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>其他的程式碼檔案加入 tooyour 專案
已加入兩個檔案 toosupport 權杖快取： **Models\ADALTokenCache.cs**和**Models\ApplicationDbContext.cs**。  其他控制器和檢視已加入 tooillustrate 存取使用 Azure graph Api 的使用者設定檔資訊。  這些檔案是 **Controllers\UserProfileController.cs** 和 **Views\UserProfile\Index.cshtml**。

### <a name="additional-startup-code-was-added-tooyour-project"></a>已新增其他的啟動程式碼 tooyour 專案
在 hello **startup.auth.cs**檔案，新**OpenIdConnectAuthenticationNotifications**物件已加入 toohello**通知**hello 的成員**OpenIdConnectAuthenticationOptions**。  這是 tooenable 接收 hello OAuth 的程式碼和交換存取權杖。

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Tooyour app.config 或 web.config 進行其他變更
hello 下列額外的設定項目已加入。

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

hello 下列組態區段和連接字串已加入。

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a>Azure Active Directory 應用程式已更新
您 Azure Active Directory 應用程式已更新的 tooinclude hello*讀取目錄資料*權限，以及其他機碼已建立的已當做 hello *ida: ClientSecret*在 hello **web.config**檔案。

## <a name="next-steps"></a>後續步驟
- [深入了解 Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

