---
title: "aaaAuthenticate 與 Mobile Engagement REST Api"
description: "描述如何使用 Azure Mobile Engagement REST Api tooauthenticate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>使用 Mobile Engagement REST API 進行驗證
## <a name="overview"></a>概觀
本文件說明如何 tooget 有效的 AAD Oauth 語彙基元 tooauthenticate 以 hello Mobile Engagement REST Api。 

已假設您具備有效的 Azure 訂用帳戶，也已使用其中一個 [開發人員教學課程](mobile-engagement-windows-store-dotnet-get-started.md)建立 Mobile Engagement 應用程式。

## <a name="authentication"></a>驗證
使用 Microsoft Azure Active Directory 型的 OAuth 權杖進行驗證。 

在訂單 tooauthentication API 要求中，授權標頭必須加入屬於下列表單的 hello tooevery 要求：

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Azure Active Directory 權杖會在 1 小時內過期。
> 
> 

有數種方式 tooget 語彙基元。 Hello Api 通常稱為從雲端服務，因為您想 toouse API 金鑰。 在 Azure 術語中，API 金鑰稱為「服務主體密碼」。 hello 下列程序說明其中一種方式 toosetting 它以手動方式啟動。

### <a name="one-time-setup-using-script"></a>單次設定 (使用指令碼)
您應該遵循 hello 組 tooperform hello 安裝程式需要 hello 安裝程式的最小時間，但是會使用 hello 最所允許的預設值的 PowerShell 指令碼中使用下列指示。 （選擇性） 您也可以遵循 hello 中的 hello 指示[手動安裝](mobile-engagement-api-authentication-manual.md)hello Azure 入口網站直接與不要進行更細微的組態執行此作業。 

1. 取得 hello 最新版本的 Azure PowerShell，從[這裡](http://aka.ms/webpi-azps)。 如需有關 hello 下載指示的詳細資訊，您可以看到這[連結](/powershell/azure/overview)。  
2. 使用 hello 下列 Azure PowerShell 安裝之後，命令 tooensure 您擁有 hello **Azure 模組**安裝：
   
    a. 確定在 hello 可用的模組清單中的 hello Azure PowerShell 模組可用。 
   
        Get-Module –ListAvailable 
   
    ![可用的 Azure 模組][1]
   
    b. 如果您找不到 hello Azure PowerShell 模組清單上方的 hello 中您會需要 toorun hello 下列：
   
        Import-Module Azure 
3. 登入 toohello 從 PowerShell 的 Azure 資源管理員執行 hello 下列命令，並提供您的 Azure 帳戶使用者名稱和密碼： 
   
        Login-AzureRmAccount
4. 如果您有多個訂閱，您應該執行 hello 下列：
   
    a. Toouse 取得您所有的訂閱和複製 hello hello 您想要的訂用帳戶的訂用帳戶 Id 的清單。 請確定此訂用帳戶是具有相同 hello 您 Mobile Engagement 應用程式的 hello 與使用 toointeract hello 應用程式開發介面。 
   
        Get-AzureRmSubscription
   
    b. Hello 執行的下列命令提供 hello SubscriptionId tooconfigure hello 訂用帳戶 toobe 使用。
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. 複製 hello 的 hello 文字[新增 AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1)指令碼 tooyour 本機電腦，然後將它儲存為 PowerShell 指令程式 (例如`APIAuth.ps1`) 並執行它`.\APIAuth.ps1`。 
6. hello 指令碼會要求您輸入的 tooprovide **principalName**。 您想 toouse toocreate Active Directory 應用程式 (例如 APIAuth) 提供一個適合的名稱。 
7. Hello 指令碼完成後，它會顯示 hello 下列四個值，您必須以程式設計方式使用 AD tooauthenticate，所以請確定 toocopy 它們。 
   
    **TenantId**、**SubscriptionId**、**ApplicationId** 及 **Secret**。
   
    您將使用 TenantId 做為 `{TENANT_ID}`、使用 ApplicationId 做為 `{CLIENT_ID}`，並使用 Secret 做為 `{CLIENT_SECRET}`。
   
   > [!NOTE]
   > 預設的安全性原則可能會阻止您執行 PowerShell 指令碼。 如果是這樣，您會暫時設定您執行 tooallow 指令碼執行原則使用下列命令的 hello:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. 以下是 hello 組 PS 指令程式會如下。 
   
    ![][3]
9. 請檢查 hello Azure 管理入口網站中，新的 AD 應用程式建立 hello 名稱您提供 toohello 指令碼呼叫**principalName**下**顯示我公司所擁有的應用程式**。
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>步驟 tooget 有效的語彙基元
1. 以下列參數的 hello 呼叫 hello 應用程式開發介面，並請確定 tooreplace hello 租用戶\_識別碼、 用戶端\_識別碼和用戶端\_密碼：
   
   * **要求 URL** 為 https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token
   * **HTTP Content-Type 標頭** 為 *application/x-www-form-urlencoded*
   * **HTTP 要求主體**為 grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     hello 下面是範例要求：
     
       POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     以下是範例回應：
     
       HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     這個範例包含 URL 編碼的 hello POST 參數，`resource`值實際上是`https://management.core.windows.net/`。 請小心 tooalso URL 編碼`{CLIENT_SECRET}`因為它可能包含特殊字元。
     
     > [!NOTE]
     > 如需測試，您可以使用像是 [Fiddler](http://www.telerik.com/fiddler) 或 [Chrome Postman 擴充](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)的 HTTP 用戶端工具 
     > 
     > 
2. 現在每個應用程式開發介面呼叫，包括 hello 授權要求標頭：
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    如果您收到 401 狀態碼傳回，核取 hello 回應主體中，它可能在 hello 權杖到期時告訴您。 在此情況下，請取得新的權杖。

## <a name="using-hello-apis"></a>使用 hello 應用程式開發介面
現在您有有效的語彙基元時，您就準備 toomake hello API 呼叫。

1. 在每個 API 要求中，您必須使用 toopass 有效且未到期的語彙基元 hello 前一節中取得。
2. 您將需要某些參數 tooplug 入 hello 要求 URI 可用來識別您的應用程式。 hello 要求 URI 看起來像下列 hello
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    tooget hello 參數，按一下您的應用程式名稱，然後按一下 儀表板，您會看到一個頁面，像是 hello 下列所有 hello 3 個參數。
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4**您的資源群組名稱即將 toobe **MobileEngagement**除非您建立一個新。 
     
     ![Mobile Engagement API URI 參數][2]

> [!NOTE]
> <br/>
> 
> 1. 忽略 hello API 根位址，因為這是 hello 先前的應用程式開發介面。<br/>
> 2. 如果您建立使用 Azure 傳統入口網站的 hello 應用程式則需要 toouse hello 應用程式資源名稱有別於 hello 應用程式名稱本身。 如果您建立 hello Azure 入口網站中的 hello 應用程式，您應該使用 hello 本身 （沒有應用程式資源名稱與 hello 新入口網站中建立的應用程式的應用程式名稱之間沒有差異） 的應用程式名稱。  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



