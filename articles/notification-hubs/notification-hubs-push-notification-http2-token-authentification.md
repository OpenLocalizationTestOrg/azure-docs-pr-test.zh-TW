---
title: "aaaToken 基礎 APNS Azure 通知中心中的 (HTTP/2) 驗證 |Microsoft 文件"
description: "本主題說明如何 tooleverage hello 新適用於 APNS 的權杖驗證"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>適用於 APNS 的權杖型 (HTTP/2) 驗證
## <a name="overview"></a>概觀
這篇文章說明如何 toouse hello 新 APNS HTTP/2 的通訊協定與權杖型驗證。

使用新通訊協定 hello hello 主要優點包括：
-   語彙基元的產生是相當麻煩可用 (比較的 toocertificates)
-   不再需要顧慮到期日 – 您可以控制驗證權杖及其撤銷
-   裝載現在可以註冊 too4 KB
- 同步的意見反應
-   您在 Apple 的最新的通訊協定 – 憑證仍然使用 hello 二進位通訊協定，可標示為已被取代

在幾分鐘內透過兩個步驟完成使用此新機制的動作：
1.  從 hello Apple 開發人員帳戶入口網站取得 hello 所需的資訊
2.  使用 hello 新資訊來設定您的通知中樞

通知中樞現在是所有集合 toouse hello 新驗證系統使用 APNS。 

請注意，如果您從使用適用於 APNS 的憑證認證進行移轉：
- 您的憑證覆寫在我們的系統，hello 權杖屬性
- 但您的應用程式會順暢地繼續 tooreceive 通知。

## <a name="obtaining-authentication-information-from-apple"></a>從 Apple 取得驗證資訊
tooenable 權杖型驗證，您需要 hello Apple 開發人員帳戶中的下列屬性：
### <a name="key-identifier"></a>金鑰識別碼
您可以從 hello Apple 開發人員帳戶中的 「 金鑰 」 頁面取得 hello 金鑰識別碼

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>應用程式識別碼和應用程式名稱
透過在 hello 開發人員帳戶中的 hello 應用程式識別碼頁面可使用 hello 應用程式名稱。 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

hello 應用程式識別碼是可透過 hello 開發人員帳戶中的 hello 成員資格詳細資料頁面。
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>驗證權杖
則產生權杖，應用程式之後，您可以下載 hello 驗證權杖。 如如何 toogenerate 這權杖的詳細資訊，請參閱太[Apple 開發人員文件](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65)。

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>設定通知中樞 toouse 權杖型驗證
### <a name="configure-via-hello-azure-portal"></a>透過 hello Azure 入口網站設定
tooenable 權杖型驗證在 hello 入口網站登入 toohello Azure 入口網站，並移 tooyour 通知中樞 > Notification Services > APNS 面板。 

我們已提供新屬性 – 驗證模式。 選取語彙基元可讓您 tooupdate 您與所有相關語彙基元屬性 hello 的中樞。

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- 輸入您從 Apple 開發人員帳戶，擷取 hello 屬性 
- 選擇您的應用程式模式 (「生產」或「沙箱」) 
- 按一下 儲存 tooupdate APNS 憑證。 

### <a name="configure-via-management-api-rest"></a>透過管理 API (REST) 進行設定

您可以使用我們[管理 Api](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate 通知中樞 toouse 權杖型驗證。
根據您設定的 hello 應用程式是否 （Apple 開發人員帳戶中指定） 的沙箱或實際執行應用程式，使用其中一種 hello 對應的端點：

- 沙箱端點：[https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)
- 生產端點：[https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> 權杖型驗證所需的 API 版本：**2017-04 或更新版本**。
> 
> 

PUT 要求 tooupdate 集線器使用權杖型驗證的範例如下：


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>設定透過 hello.NET SDK
您可以設定程式中樞 toouse 權杖型的驗證，請使用我們[最新的用戶端 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8)。 

以下是程式碼範例說明 hello 正確使用方式：


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>還原 toousing 憑證式驗證
您可以使用任何上述的方法，並將 hello 憑證而非 hello 語彙基元屬性還原在任何時間 toousing 憑證式驗證。 動作會覆寫 hello 先前預存認證。
