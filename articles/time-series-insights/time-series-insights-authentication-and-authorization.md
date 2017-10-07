---
title: "呼叫的自訂應用程式的 aaaConfigure 驗證和授權 hello Azure 時間數列 Insights API，|Microsoft 文件"
description: "本教學課程說明如何在呼叫的自訂應用程式的 tooconfigure 驗證和授權 hello Azure 時間數列 Insights API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Azure Time Series Insights API 的驗證和授權

本文說明如何自訂的應用程式呼叫 tooconfigure hello Azure 時間數列 Insights API。

## <a name="service-principal"></a>服務主體

本節說明如何 tooconfigure 應用程式 tooaccess hello 代表 hello 應用程式的時間序列 Insights API。 hello 應用程式可以接著查詢資料或發行應用程式認證和 hello 使用者認證 hello 時間數列 Insights 環境中的參考資料。

當您需要 tooaccess 時間數列 Insights 的應用程式時，您必須在設定 Azure Active Directory 應用程式，並指派 hello 時間數列 Insights 環境中的 hello 資料存取原則。 這個方法很理想 toorunning hello 應用程式，以您自己的認證，因為：

* 您可以指派權限 toohello 應用程式識別碼不同於您自己的權限。 一般而言，這些權限會限制的 tooexactly 哪些 hello 應用程式需要 toodo。 例如，您可以允許 hello 應用程式 tooonly 讀取特定的時間序列 Insights 環境中的資料。
* 如果您的責任的變更，您不需要 toochange hello 應用程式的認證。
* 如果您執行自動執行的指令碼，您可以使用憑證或金鑰 tooautomate 驗證應用程式。

本文將說明這些逐步的 tooperform hello Azure 入口網站的方式。 它著重在 hello 應用程式所在預定的 toorun 只能有一個組織中的單一租用戶應用程式。 您通常會將單一租用戶應用程式用在組織內執行的企業營運系統應用程式。

hello 的安裝程式流程是由三個高階步驟所組成：

1. 在 Azure Active Directory 中建立應用程式。
2. 授權這個應用程式 tooaccess hello 時間數列 Insights 環境。
3. 使用 hello 應用程式識別碼和金鑰 tooacquire 語彙基元 toohello`"https://api.timeseries.azure.com/"`對象或資源。 hello 語彙基元接著可以使用的 toocall hello Insights API，時間序列。

以下是 hello 詳細的步驟：

1. 在 hello Azure 入口網站，選取  **Azure Active Directory** > **應用程式註冊** > **新應用程式註冊**。

   ![Azure Active Directory 中的新應用程式註冊](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. 提供 hello 應用程式名稱、 選取 hello 類型 toobe **Web 應用程式 / 應用程式開發介面**，選取任何有效的 URI，如**登入 URL**，然後按一下**建立**。

   ![在 Azure Active Directory 中建立 hello 應用程式](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. 選取您新建立的應用程式並複製其應用程式識別碼 tooyour 慣用的文字編輯器。

   ![複製 hello 應用程式識別碼](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. 選取**金鑰**，輸入 hello 索引鍵名稱，選取 hello 到期，然後按一下**儲存**。

   ![選取應用程式金鑰](media/authentication-and-authorization/active-directory-application-keys.png)

   ![輸入 hello 索引鍵名稱和到期日，然後按一下 [儲存]](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. 複製 hello 金鑰 tooyour 慣用的文字編輯器。

   ![複製 hello 應用程式金鑰](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Hello 時間數列 Insights 環境中，選取**資料存取原則**按一下**新增**。

   ![加入新資料的存取原則 toohello 時間數列 Insights 環境](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. 在 [hello**選取使用者**] 對話方塊中，貼上 hello 應用程式名稱 （來自步驟 2） 或應用程式識別碼 （從步驟 3）。

   ![尋找應用程式在 hello [選取使用者] 對話方塊](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. 選取 hello 角色 (**讀取器**來查詢資料，**參與者**查詢資料和變更參考資料)，按一下 **確定**。

   ![在 hello 選取角色 對話方塊中挑選讀者或參與者](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. 按一下以儲存 hello 原則**確定**。

10. 使用 hello 應用程式識別碼 （從步驟 3） 和應用程式 （從步驟 5） 索引鍵 tooacquire hello 語彙基元，代表 hello 應用程式。 hello 語彙基元可以然後傳入 hello `Authorization` hello 應用程式會呼叫 hello 時間數列 Insights API 時，標頭。

    如果您使用 C#，您可以使用下列程式碼 tooacquire hello 語彙基元，代表 hello 應用程式的 hello。 如需完整範例，請參閱[使用 C# 查詢資料](time-series-insights-query-data-csharp.md)。

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>後續步驟

應用程式中使用 hello 應用程式識別碼和金鑰。 呼叫 hello 時間數列 Insights API 的範例程式碼，請參閱[查詢資料使用 C#](time-series-insights-query-data-csharp.md)。

## <a name="see-also"></a>另請參閱

* [查詢 API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) hello 完整查詢 API 參考
* [建立服務主體在 hello Azure 入口網站](../azure-resource-manager/resource-group-create-service-principal-portal.md)
