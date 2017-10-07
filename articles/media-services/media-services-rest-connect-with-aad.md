---
title: "Azure AD 驗證 tooaccess Azure 媒體服務 API 與其餘 aaaUse |Microsoft 文件"
description: "了解與使用 Azure Active Directory 驗證 tooaccess Azure Media Services API REST 的方式。"
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>使用 Azure AD 驗證 tooaccess hello 與其餘的 Azure 媒體服務 API

hello Azure 媒體服務團隊發行了 Azure Media Services 存取的 Azure Active Directory (Azure AD) 驗證支援。 它也宣佈 Media Services 存取的計劃 toodeprecate Azure 存取控制服務驗證。 因為每個 Azure 訂用帳戶，且每個 Media Services 帳戶，已附加的 tooan Azure AD 租用戶，Azure AD 驗證的支援會帶來許多的安全性優點。 如需此變更和移轉 （如果您使用 Media Services.NET SDK hello 應用程式），詳細資料，請參閱 hello 下列部落格文章和文章：

- [Azure 媒體服務宣佈支援 Azure AD 驗證，取代存取控制驗證](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation) \(英文\)
- [使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)
- [使用 Microsoft.NET 中使用 Azure AD 驗證 tooaccess Azure 媒體服務 API](media-services-dotnet-get-started-with-aad.md)
- [開始使用 Azure AD 驗證使用 hello Azure 入口網站](media-services-portal-get-started-with-aad.md)

某些客戶需要 toodevelop hello 遵循條件約束下的其媒體服務方案：

*   使用不是 Microsoft.NET 或 C# 的程式設計語言或 hello 執行階段環境不是 Windows。
*   Azure AD 程式庫，例如 Active Directory 驗證程式庫沒有可用的 hello 程式設計語言，或無法使用其執行階段環境。

某些客戶已使用 REST API 開發可執行存取控制驗證和存取 Azure 媒體服務的應用程式。 對於這些客戶，您需要的 Azure AD 驗證的方式 toouse 只有 hello REST API 和後續的 Azure 媒體服務存取。 您需要 toonot 依賴任何 hello Azure AD 文件庫或 hello Media Services.NET SDK 上。 在本文中，我們描述一種解決方案，並提供此案例的範例程式碼。 因為所有的 REST API 呼叫，不會相依於任何 Azure AD 與 hello 的程式碼或 Azure Media Services 程式庫，hello 程式碼很容易就能轉譯的 tooany 其他程式語言。

> [!IMPORTANT]
> 目前，Media Services 支援 hello Azure 存取控制服務驗證模型。 不過，存取控制驗證將在 2018 年 6 月 1 日被取代。 我們建議您儘速移轉 toohello Azure AD 驗證模型。


## <a name="design"></a>設計

在本文中，我們會使用 hello 遵循驗證和授權的設計：

*  授權通訊協定：OAuth 2.0。 OAuth 2.0 是一種涵蓋驗證和授權的 Web 安全性標準。 OAuth 2.0 受 Google、Microsoft、Facebook 和 PayPal 支援。 它於 2012 年 10 月獲得認可。 Microsoft 穩固地支援 OAuth 2.0 和 OpenID Connect。 有多種服務和用戶端程式庫均支援這些標準，包括 Azure Active Directory、Open Web Interface for .NET (OWIN) 及 Azure AD 程式庫。
*  授與類型：用戶端認證授與類型。 用戶端認證是在 OAuth 2.0 中的 hello 四個授與類型之一。 它通常用於 Azure AD Microsoft Graph API 存取。
*  驗證模型：服務主體。 hello 其他驗證模式為使用者或互動式驗證。

使用 Media Services 的 hello Azure AD 驗證和授權流程涉及總共四個應用程式或服務。 hello 應用程式和服務，以及 hello 流程 hello 下表所述：

|應用程式類型 |應用程式 |Flow|
|---|---|---|
|用戶端 | 客戶應用程式或解決方案 | 中的 hello Azure 訂用帳戶與 hello 媒體服務帳戶位於 hello Azure AD 租用戶中註冊此應用程式 (實際上其 proxy)。 hello hello 註冊應用程式的服務主體是然後授與在 hello 存取控制 (IAM) hello 媒體服務帳戶的擁有者或參與者角色。 hello 應用程式用戶端識別碼和用戶端密碼會以 hello 服務主體。 |
|身分識別提供者 (IDP) | 作為 IDP 的 Azure AD | hello 的已註冊的應用程式服務主體 （用戶端識別碼和用戶端密碼） 會由 Azure AD hello IDP 身分進行驗證。 此驗證是在內部以隱含方式執行。 用戶端認證流程，如同 hello 用戶端會代替 hello 使用者進行驗證。 |
|安全性權杖服務 (STS)/OAuth 伺服器 | 作為 STS 的 Azure AD | 驗證之後 hello IDP （或 OAuth 2.0 中的 OAuth 伺服器），存取權杖或 JSON Web Token (JWT) 做為 STS/OAuth 伺服器存取 toohello 中介層資源的 Azure AD 所簽發： 在此案例中的 hello 媒體服務 REST API 端點。 |
|資源 | 媒體服務 REST API | 存取權杖是由 Azure AD 所簽發為 STS 或 hello OAuth 伺服器已獲得授權的每個媒體服務 REST API 呼叫。 |

如果您執行 hello 範例程式碼，並擷取 JWT 存取權杖，hello JWT 具有下列屬性的 hello:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

以下是 hello JWT 和 hello 四個應用程式中的 hello 屬性或 hello 上述資料表中的服務之間的 hello 對應：

|應用程式類型 |應用程式 |JWT 屬性 |
|---|---|---|
|用戶端 |客戶應用程式或解決方案 |appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6"。 hello 用戶端識別碼的應用程式會登錄 tooAzure AD hello 下一節。 |
|身分識別提供者 (IDP) | 作為 IDP 的 Azure AD |idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/"。  hello GUID 是 hello 的 Microsoft ID 租用戶 (microsoft.onmicrosoft.com)。 每個租用戶都有專屬的唯一識別碼。 |
|安全性權杖服務 (STS)/OAuth 伺服器 |作為 STS 的 Azure AD | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/"。 hello GUID 是 hello 的 Microsoft ID 租用戶 (microsoft.onmicrosoft.com)。 |
|資源 | 媒體服務 REST API |aud: "https://rest.media.azure.net"。 hello 收件者或 hello 存取權杖對象。 |

## <a name="steps-for-setup"></a>設定的步驟

tooregister 及設定 Azure AD 驗證和存取權杖來呼叫 hello Azure 媒體服務 REST API 端點，完成下列步驟的 hello tooobtain Azure AD 應用程式：

1.  在 [hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，註冊 Azure AD 應用程式 (例如，wzmediaservice) toohello Azure AD 租用戶 (例如，microsoft.onmicrosoft.com)。 註冊為 Web 應用程式或原生應用程式都可以。 此外，您可以選擇任何登入 URL 和回覆 URL (例如，http://wzmediaservice.com)。
2. 在 [hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，go toohello**設定**應用程式] 索引標籤。 請注意 hello**用戶端識別碼**。 然後，在 [金鑰]之 下，產生一個 [用戶端金鑰] (用戶端祕密)。 

    > [!NOTE] 
    > 記下 hello 用戶端密碼。 它將不會再次顯示。
    
3.  在 [hello [Azure 入口網站](http://ms.portal.azure.com)，go toohello Media Services 帳戶。 選取 hello**存取控制**(IAM) 窗格。 加入新的成員具有 hello 擁有者或 hello 參與者角色。 Hello 主體搜尋 hello 註冊，讓您在步驟 1 中 （在此範例中，wzmediaservice） 的應用程式名稱。

## <a name="info-toocollect"></a>資訊 toocollect

tooprepare REST 撰寫程式碼，請收集下列資料點 tooinclude hello 程式碼中的 hello:

*   作為 STS 端點的 Azure AD： https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token。 JWT 存取權杖是從這個端點要求。 此外 tooserving IDP 身分，Azure AD 也可做為 STS。 Azure AD 會核發存取資源所需的 JWT (存取權杖)。 JWT 權杖含有各種宣告。
*   作為資源或對象的 Azure 媒體服務 REST API：https://rest.media.azure.net。
*   用戶端識別碼：請參閱[設定步驟](#steps-for-setup)中的步驟 2。
*   用戶端祕密：請參閱[設定步驟](#steps-for-setup)中的步驟 2。
*   Media Services 帳戶 hello 遵循格式中的 REST API 端點：

    https://[media_service_account_name].restv2.[data_center].media.azure.net/API 

    這是針對所有媒體服務 REST API 進行呼叫應用程式中的 hello 端點。 例如，https://willzhanmswjapan.restv2.japanwest.media.azure.net/API。

您接著可以在 web.config 或 app.config 檔案中，您的程式碼中的 toouse 放置這些五個參數。

## <a name="sample-code"></a>範例程式碼

您可以找到 hello 中的範例程式碼[以 Azure Media Services 存取的 Azure AD 驗證： 透過 REST API 兩者](https://github.com/willzhan/WAMSRESTSoln)。

hello 範例程式碼有兩個部分：

*   Azure AD 驗證與授權的所有 hello REST API 程式碼的 DLL 程式庫專案。 它也有一種方法進行 REST API 呼叫 toohello 媒體服務 REST API 端點展開，以 hello 存取權杖。
*   主控台測試用戶端，會起始 Azure AD 驗證，並呼叫不同的媒體服務 REST API。

hello 範例專案具有三個功能：

*   Azure AD 驗證，透過 hello 用戶端認證授與使用 hello REST API。
*   使用 hello REST API 的 azure 媒體服務存取。
*   使用 azure 儲存體存取權僅 hello REST 應用程式開發介面 （做為使用 toocreate Media Services 帳戶，使用 REST API)。


## <a name="where-is-hello-refresh-token"></a>其中是 hello 重新整理權杖？

某些讀取器可能會要求： 所在 hello 重新整理權杖？ 為何不在此使用重新整理權杖？

重新整理權杖的 hello 目的不是 toorefresh 存取權杖。 相反地，它是設計的 toobypass 使用者驗證或使用者的介入，，當先前的權杖到期時仍可以獲得的有效存取權杖。 比重新整理權杖更適合的名稱可能是像「略過使用者重新登入權杖」的名稱。

如果您使用 hello OAuth 2.0 授權授與流程 （使用者名稱和密碼，可代表使用者），重新整理權杖可協助您不需要求使用者介入的情況下，取得更新的存取權杖。 不過，hello OAuth 2.0 用戶端認證授與我們在本文中說明的流程，hello 用戶端的作用代替它自己。 您不需要使用者介入，而且在 hello 授權伺服器不太需要 （及將不會） 提供重新整理權杖。 如果您偵錯 hello **GetUrlEncodedJWT**方法，您會注意到 hello 回應 hello 權杖端點的存取權杖，但不是重新整理權杖。

## <a name="next-steps"></a>後續步驟

開始使用[上傳檔案 tooyour 帳戶](media-services-dotnet-upload-files.md)。
