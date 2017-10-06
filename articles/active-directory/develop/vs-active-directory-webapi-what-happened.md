---
title: "連接 tooAzure AD 時所做的 aaaChanges tooa WebApi 專案 |Microsoft 文件"
description: "描述使用 Visual Studio 連接 tooAzure AD 時所採取的 tooyour WebApi 專案"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>哪些情形的 toomy WebApi 專案 （Visual Studio Azure Active Directory 已連線服務）
> [!div class="op_single_selector"]
> * [開始使用](vs-active-directory-webapi-getting-started.md)
> * [發生什麼情形](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>已加入參考
### <a name="nuget-package-references"></a>NuGet 封裝參考
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>.NET 參考
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>程式碼變更
### <a name="code-files-were-added-tooyour-project"></a>程式碼檔案加入 tooyour 專案
驗證啟動類別**App_Start/Startup.Auth.cs**已加入 tooyour 專案包含 Azure AD 驗證的啟動邏輯。

### <a name="startup-code-was-added-tooyour-project"></a>啟始程式碼已加入 tooyour 專案
如果您已經在專案中啟動類別，hello**組態**方法太更新的 tooinclude 呼叫`ConfigureAuth(app)`。 否則，請啟動類別已加入 tooyour 專案。

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>app.config 或 web.config 檔案有新的組態值。
已加入下列組態項目 hello。

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>已建立 Azure AD 應用程式
Azure AD 應用程式已建立您 hello 精靈中選取的 hello 目錄中。

[深入了解 Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>如果在簽*停用個別使用者帳戶驗證*，toomy 專案所做其他變更？
NuGet 封裝參考會被移除，檔案也會移除並加以備份。 根據您的專案 hello 狀態，您可能必須 toomanually 移除其他參考或檔案，或修改為適當的程式碼。

### <a name="nuget-package-references-removed-for-those-present"></a>移除的 NuGet 封裝參考 (如果存在)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>備份和移除的程式碼檔案 (如果存在)
每個下列檔案已備份，並且從 hello 專案中移除。 備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>備份的程式碼檔案 (如果存在)
下列每個檔案會在取代之前備份。 備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>如果在簽*讀取目錄資料*，toomy 專案所做其他變更？
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Tooyour app.config 或 web.config 進行其他變更
hello 下列額外的設定項目已加入。

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Azure Active Directory 應用程式已更新
您 Azure Active Directory 應用程式已更新的 tooinclude hello*讀取目錄資料*權限，以及其他機碼已建立的已當做 hello *ida： 密碼*在 hello`web.config`檔案。

## <a name="next-steps"></a>後續步驟
- [深入了解 Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

