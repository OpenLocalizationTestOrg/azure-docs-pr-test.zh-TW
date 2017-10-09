---
title: "具有多重 DRM 及存取控制的 CENC：Azure 與 Azure 媒體服務的參考設計和實作 | Microsoft Docs"
description: "深入了解如何 toolicensing hello Microsoft® Smooth Streaming Client Porting Kit。"
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>具有多重 DRM 及存取控制的 CENC：Azure 與 Azure 媒體服務的參考設計和實作
 
## <a name="introduction"></a>簡介
它是眾所周知它是複雜的工作 toodesign，並建置 OTT DRM 子系統或線上串流處理解決方案。 而且它是一般練習的運算子/線上視訊提供者 toooutsource 這個組件 toospecialized DRM 服務提供者。 這份文件 hello 目標是 toopresent 參考設計和實作端對端 DRM 子系統 OTT 或線上串流處理解決方案中。

本文件的 hello 目標讀者是工程師 DRM 子系統 OTT 或線上串流/多-screen 解決方案，或非興趣 DRM 子系統的的讀取器中使用。 hello 假設是讀者已熟悉 hello DRM 技術，例如 PlayReady、 Widevine、 FairPlay 或 Adobe Access 的 hello 市場上其中。

根據 DRM，我們也包含 CENC (Common Encryption) 與多重 DRM。 線上串流和 OTT 產業中的主要趨勢是 toouse CENC 多-native-DRM 各種用戶端的平台，使用 shift 鍵，從各種用戶端的平台針對使用單一的 DRM 與用戶端 SDK 的 hello 先前趨勢。 當使用多 native DRM CENC，PlayReady 和 Widevine 加密 hello[一般加密 (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/)規格。

使用多重 DRM CENC hello 優點如下：

1. 降低加密成本，因為對於不同平台使用其原生 DRM 進行單一加密處理；
2. 可減少由於需要加密的資產的單一複本; 因此管理加密的資產 hello 成本
3. 排除 DRM 授權成本，因為原生 DRM 用戶端 hello 通常是免費的原生平台上的用戶端。

Microsoft 已經成為 DASH 和 CENC 與其他一些主要業界播放器的積極推動者。 Microsoft Azure 媒體服務已提供 DASH 和 CENC 的支援。 如需最新的通知，請參閱 Mingfei 的部落格：[Announcing Google Widevine license delivery services in Azure Media Services (宣佈在 Azure 媒體服務中推出 Google Widevine 授權傳遞服務)](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)，和 [Azure Media Services adds Google Widevine packaging for delivering multi-DRM stream (Azure 媒體服務新增 Google Widevine 封裝來傳遞多重 DRM 串流)](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)。  

### <a name="overview-of-this-article"></a>本文概觀：
本文的 hello 目標包括 hello 下列：

1. 提供使用 CENC 與多重 DRM 的 DRM 子系統的參考設計；
2. 提供 Microsoft Azure/Azure 媒體服務平台上的參考實作；
3. 討論某些設計和實作主題。

在 hello 文章中，「 多 DRM"涵蓋 hello 下列：

1. Microsoft PlayReady (英文)
2. Google Widevine
3. Apple FairPlay 

hello 表摘要說明 hello 原生的平台/原生應用程式，以及每個 DRM 所支援的瀏覽器。

| **用戶端平台** | **原生 DRM 支援** | **瀏覽器/應用程式** | **串流格式** |
| --- | --- | --- | --- |
| **智慧型電視、運算子 STB、OTT STB** |主要為 PlayReady，及/或 Widevine，及/或其他的 DRM |Linux、Opera、WebKit 及其他瀏覽器/應用程式 |各種格式 |
| **Windows 10 裝置 (Windows 電腦、Windows 平板電腦、Windows Phone、Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |DASH (HLS 並不支援 PlayReady)<br/><br/>DASH、Smooth Streaming (HLS 並不支援 PlayReady) |
| **Android 裝置 (電話、平板電腦、電視)** |Widevine |Chrome/EME |DASH,HLS |
| **iOS (iPhone、iPad)、OS X 用戶端和 Apple 電視** |FairPlay |Safari 8+/EME |HLS |


請考慮為每個 DRM 部署的 hello 目前狀態，服務通常會想 tooimplement 2 或 3 DRMs toomake 確定解決所有的 hello 類型的端點在 hello 最佳的方式。

Hello 複雜度 hello 服務邏輯之間沒有取捨，hello 複雜性 hello 用戶端端 tooreach 特定層級的使用者體驗上 hello 各種用戶端。

toomake 選取範圍，請注意下列重點：

* PlayReady 原生實作在每種 Windows 裝置及部分 Android 裝置中，且可透過軟體 SDK 在幾乎所有平台上實作
* Widevine 原生實作在每種 Android 裝置、Chrome 及部分其他的裝置中
* FairPlay 只使用在 iOS 和 Mac OS 用戶端中，或是透過 iTunes 來提供。

因此典型的多重 DRM 會是：

* 選項 1：PlayReady 及 Widevine
* 選項 2：PlayReady、Widevine 和 FairPlay

## <a name="a-reference-design"></a>參考設計
在本節中，我們將提供參考設計也就是使用無從驗證 tootechnologies tooimplement 它。

DRM 子系統可能包含下列元件的 hello:

1. 金鑰管理
2. DRM 封裝
3. DRM 授權傳遞
4. 權利檢查
5. 驗證/授權
6. 播放器
7. 原始/CDN

hello 下列圖表說明 hello 高等級的互動 DRM 子系統中的 hello 元件之間。

![DRM 子系統與 CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Hello 設計有三個基本 」 層級 」:

1. 後台系統層級 (黑色)，不會對外部公開；
2. 包含所有面向公用; 的 hello 端點的 「 周邊網路 」 層 （藍色）
3. 公用網際網路層級 (淺藍色)，包含具有跨公用網際網路流量的 CDN 和播放器。

應該有用來控制 DRM 保護的內容管理工具，無論是靜態或動態加密。 DRM 加密的 hello 輸入應該包括：

1. MBR 視訊內容；
2. 內容金鑰；
3. 授權取得 URL。

在播放期間，hello 高的層級非固定格式為：

1. 使用者已通過驗證；
2. 授權權杖建立 hello 使用者;
3. 受 DRM 保護內容 （資訊清單） 是下載的 tooplayer;
4. 玩家送出授權擷取要求 toolicense 伺服器以及金鑰識別碼和授權權杖。

之前移動 toohello 下一個主題： hello 相關的幾個字設計的金鑰管理。

| **ContentKey–to-Asset** | **案例** |
| --- | --- |
| 1 對 1 |hello 簡單的情況。 它提供 hello 最精細的控制。 但是，這通常會導致 hello 最高的授權傳遞成本。 每個受保護的資產需要至少一個授權要求。 |
| 1 對多 |您可以使用相同的內容金鑰的多個資產的 hello。 例如，為所有的 hello 資產中的邏輯群組，例如內容類型或內容類型 （或電影 Gene） 的子集，您可以使用單一的內容金鑰。 |
| 多對 1 |每個資產需要有多個內容金鑰。 <br/><br/>例如，如果您需要具有多重 DRM tooapply 動態 CENC 保護 MPEG DASH 和 HLS 動態 aes-128 加密，您需要兩個不同內容索引鍵，每個都有它自己的 ContentKeyType。 （hello 做為動態 CENC 保護內容的金鑰，ContentKeyType.CommonEncryption 應該用於，而內容應該使用金鑰用於動態 aes-128 加密，ContentKeyType.EnvelopeEncryption hello。）<br/><br/>另一個範例中的虛線 CENC 保護內容，理論上，請使用的 tooprotect 視訊資料流和另一個內容金鑰 tooprotect 音訊資料流，可以是一個內容金鑰。 |
| 許多 – 太對多 |Hello 上述兩個案例的組合： 一組內容金鑰可用於每個 hello 的多個資產的 hello 相同資產 「 群組 」。 |

另一個重要的因素 tooconsider 是 hello 使用持續性和非持續性授權。

這些考量為何重要？

它們有直接的影響 toolicense 傳遞，若您使用公用雲端來授權傳遞成本。 讓我們考量有下列兩個不同的設計案例 tooillustrate hello:

1. 每月訂用帳戶：使用持續性授權，以及 1 對多的內容金鑰對資產對應。 例如 所有的 hello 兒童影片中，我們會使用單一內容金鑰加密。 在此案例中：

    所有兒童影片/裝置的授權數總計 = 1
2. 每月訂用帳戶：使用非持續性授權，以及內容金鑰和資產之間的 1 對 1 對應。 在此案例中：

    所有兒童影片/裝置的授權數總計 = [觀賞影片數] x [工作階段數]

您可以輕鬆地看到，hello 兩個不同的設計導致非常不同的授權要求模式，因此授權成本如果授權傳遞服務係由 Azure Media Services 例如公用雲端的傳遞。

## <a name="mapping-design-tootechnology-for-implementation"></a>對應設計 tootechnology 實作
接下來，我們將 Microsoft Azure/Azure Media Services 平台上，我們一般設計 tootechnologies 對應藉由指定的每個建置組塊的技術 toouse。

hello 下表顯示 hello 對應：

| **建置組塊** | **Technology** |
| --- | --- |
| **播放器** |[Azure Media Player](https://azure.microsoft.com/services/media-services/media-player/) |
| **身分識別提供者 (IDP)** |Azure Active Directory |
| **安全權杖服務 (STS)** |Azure Active Directory |
| **DRM 保護工作流程** |Azure 媒體服務動態保護 |
| **DRM 授權傳遞** |1.Azure 媒體服務授權傳遞 (PlayReady、Widevine、FairPlay) 或 <br/>2.Axinom 授權伺服器， <br/>3.自訂 PlayReady 授權伺服器 |
| **原始** |Azure 媒體服務串流端點 |
| **金鑰管理** |不需要參考實作 |
| **內容管理** |C# 主控台應用程式 |

換句話說，身分識別提供者 (IDP) 和安全權杖服務 (STS) 都將是 Azure AD。 對於播放器，我們將會使用 [Azure 媒體播放器 API](http://amp.azure.net/libs/amp/latest/docs/)。 Azure 媒體服務和 Azure Media Player 都支援具有多重 DRM 的 DASH 和 CENC。

下列圖表顯示 hello hello 以上述技術對應 hello 的整體結構與流程。

![AMS 上的 CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

順序 tooset 動態 CENC 加密設定，在 hello 內容管理工具將使用下列輸入 hello:

1. 開啟內容；
2. 來自金鑰產生/管理的內容金鑰；
3. 授權取得 URL；
4. Azure AD 中的資訊清單。

hello 輸出 hello 內容管理工具將會：

1. 包含如何授權傳遞驗證的 JWT 語彙基元和 DRM 授權規格; hello 規格 ContentKeyAuthorizationPolicy
2. AssetDeliveryPolicy，包含串流格式、DRM 保護和授權取得 URL 的規格。

Hello 流程是在執行階段如下：

1. 在使用者驗證時，會產生 JWT 權杖；
2. 包含 「 EntitledUserGroup"hello 群組物件識別碼的 「 群組 」 宣告的 hello 宣告 hello JWT 權杖中包含的其中一個。 這個宣告會用於傳遞「權利檢查」。
3. 播放程式下載用戶端資訊清單的 CENC 受保護的內容和 「 看見 」 hello 下列：

   1. 金鑰識別碼，
   2. hello 內容是受保護的 CENC
   3. 授權取得 URL。
4. 播放程式就會根據 hello 瀏覽器/DRM 支援授權擷取要求。 Hello 授權取得要求、 索引鍵識別碼和 hello JWT 中也會提交語彙基元。 授權傳遞服務會確認 hello JWT 權杖和 hello 宣告包含之前發出 hello 需要授權。

## <a name="implementation"></a>實作
### <a name="implementation-procedures"></a>實作程序
hello 實作會包含下列步驟的 hello:

1. 準備測試 asset(s)： 編碼/封裝測試視訊 toomulti-位元速率分散 MP4 Azure 媒體服務中的。 這項資產不受 DRM 保護。 DRM 保護稍後會由動態保護完成。
2. 建立金鑰識別碼和內容金鑰 (選擇性地從金鑰種子)。 對於我們的目的，不需要金鑰管理系統，因為我們只會針對一些測試資產處理一組金鑰識別碼和內容金鑰；
3. 使用 AMS API tooconfigure 多重 DRM 授權傳遞服務 hello 測試資產。 如果您使用自訂的授權伺服器透過您的公司或您公司的廠商，而不是在 Azure 媒體服務授權服務，您可以略過此步驟，並指定在 hello 步驟中設定授權傳遞的授權取得 Url。 AMS API 是所需的一些詳細的 toospecify 組態，例如授權原則限制，授權等不同 DRM 授權服務的回應範本。此時，hello Azure 入口網站尚未提供此設定 hello 所需 UI。 您可以在 Julia Kornich 的文件中尋找 API 層級資訊和範例程式碼： [使用 PlayReady 和/或 Widevine Dynamic Common Encryption](media-services-protect-with-drm.md)。
4. 用於 hello 測試資產 AMS API tooconfigure 資產傳遞原則。 您可以在 Julia Kornich 的文件中尋找 API 層級資訊和範例程式碼： [使用 PlayReady 和/或 Widevine Dynamic Common Encryption](media-services-protect-with-drm.md)。
5. 在 Azure 中建立和設定 Azure Active Directory 租用戶；
6. Azure Active Directory 租用戶中建立幾個使用者帳戶和群組： 您應該至少建立"EntitledUser 」 群組，並新增使用者 toothis 群組。 此群組中的使用者將會傳入取得授權的權限核取並不在此群組中的使用者將會失敗 toopass 驗證檢查，而且也不會無法 tooacquire 任何授權。 這個 「 EntitledUser 」 群組的成員，是在 hello Azure AD 所簽發的 JWT 權杖中必要的 「 群組 」 宣告。 這個宣告需求應該在設定多重 DRM 授權傳遞服務步驟中指定。
7. 建立 ASP.NET MVC 應用程式，它將會裝載視訊播放器。 此 ASP.NET 應用程式將保護的 hello Azure Active Directory 租用戶的使用者驗證。 在 hello 存取權杖取得使用者驗證之後，將會包含適當的宣告。 建議在此步驟使用 OpenID Connect API。 您需要下列 NuGet 封裝 tooinstall hello:
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. 使用 [Azure 媒體播放器 API](http://amp.azure.net/libs/amp/latest/docs/)來建立播放器。 [Azure Media Player 的 ProtectionInfo API](http://amp.azure.net/libs/amp/latest/docs/) toospecify 可讓您在不同的 DRM 平台上的 DRM 技術 toouse。
9. 測試矩陣：

| **DRM** | **[瀏覽器]** | **有權限的使用者的結果** | **無權限的使用者的結果** |
| --- | --- | --- | --- |
| **PlayReady** |MS Edge 或 Windows 10 上的 IE11 |成功 |不合格 |
| **Widevine** |Windows 10 上的 Chrome |成功 |不合格 |
| **FairPlay** |TBD | | |

Azure 媒體服務團隊的 George Trifonov 所撰寫的部落格提供針對 ASP.NET MVC 播放器應用程式來設定 Azure Active Directory 的詳細步驟： [Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims (整合 Azure 媒體服務 OWIN MVC 型應用程式與 Azure Active Directory，並根據 JWT 宣告來限制內容金鑰傳遞)](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)。

George 也撰寫了一篇相關的部落格文章： [JWT token Authentication in Azure Media Services and Dynamic Encryption (Azure 媒體服務和動態加密中的 JWT 權杖驗證)](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)。 以下是他 [整合 Azure AD 與 Azure 媒體服務金鑰傳遞的範例](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/)。

如需 Azure Active Directory 的詳細資訊：

* 您可以在 [Azure Active Directory 開發人員指南](../active-directory/active-directory-developers-guide.md)中找到開發人員的資訊。
* 您可以在 [管理 Azure AD 目錄](../active-directory/active-directory-administer.md)中找到系統管理員的資訊。

### <a name="some-gotchas-in-implementation"></a>實作中的一些錯誤
Hello 實作中有一些 「 問題 」。 但願 hello 遵循 「 問題 」 的清單可協助您疑難排解萬一您遇到問題。

1. **簽發者**的 URL 結尾應該是 **"/"**。  

    **對象**應該 hello 播放器應用程式用戶端識別碼，而且您也應該加入**"/"** hello hello 簽發者 URL 結尾處。

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    在[JWT 解碼器](http://jwt.calebb.net/)，您應該會看到**則**和**iss** hello JWT 權杖中，如下：

    ![第 1 個錯誤](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. （在 hello 應用程式設定 索引標籤），請在 AAD 中新增 toohello 應用程式的權限。 對於每個應用程式這是必要的 (本機和已部署版本)。

    ![第 2 個錯誤](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. 使用中設定動態 CENC 保護 hello 正確的簽發者：

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    hello 下列將不會運作：

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    hello GUID 是 hello AAD 租用戶識別碼。 hello GUID 可以找到端點快顯視窗中，在 Azure 入口網站中。
4. 授與群組成員資格宣告權限。 確定 AAD 應用程式資訊清單檔中，我們有下列 hello

    "groupMembershipClaims":"All"（hello 預設值是 null）
5. 建立限制需求時，設定適當的 TokenType。

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    新增支援的 JWT (AAD) 此外 tooSWT (ACS)，因為 hello 預設 TokenType 是 TokenType.JWT。 如果您使用 SWT/ACS 時，您必須設定 tooTokenType.SWT。

## <a name="additional-topics-for-implementation"></a>Additional Topics for Implementation (其他關於實作的主題)
接下來，我們將討論設計和實作中的其他主題。

### <a name="http-or-https"></a>HTTP 或 HTTPS？
hello 我們建立的 ASP.NET MVC 播放器應用程式必須支援下列 hello:

1. 透過 Azure AD 中，這需要 toobe HTTPS; 下的使用者驗證
2. JWT 權杖 exchange 用戶端與 Azure AD 中，這需要 HTTPS; 下的 toobe 之間
3. DRM 取得 hello 用戶端為必要的 toobe HTTPS 之下，如果授權傳遞由 Azure Media Services 提供的授權。 當然，PlayReady 產品套件不會針對授權傳遞來授權 HTTPS。 如果您的 PlayReady 授權伺服器位於 Azure 媒體服務以外的地方，則可以使用 HTTP 或 HTTPS。

因此，hello ASP.NET 播放器應用程式將最佳做法是使用 HTTPS。 這表示的 hello Azure Media Player 會在 HTTPS 頁面。 不過，對於資料流我們偏好 HTTP，因此我們需要 tooconsider 混合內容的問題。

1. 瀏覽器不允許混合的內容。 但是如 Silverlight 的外掛程式和適用於 Smooth 和 DASH 的 OSMF 外掛程式允許。 混合的內容的安全性問題-這是因為 toohello 威脅的 hello 能力 tooinject 而造成惡意 JS hello 客戶資料 toobe 風險。  瀏覽器封鎖了這項預設，且目前 hello 唯一方式 toowork 周圍 hello 伺服器 （來源） 端上，tooallow （不論 https 或 http） 的所有網域。 這可能也不是個好主意。
2. 我們應該避免混合的內容：都使用 HTTP 或都使用 HTTPS。 播放混合的內容時，silverlightSS 技術需要清除混合內容警告。 flashSS 技術會處理混合的內容，而沒有混合內容警告。
3. 如果您的串流端點是在 2014 年 8 月之前建立，它將不會支援 HTTPS。 在此情況下，請針對 HTTPS 建立並使用新的串流端點。

在 hello 參考實作中，受 DRM 保護內容的應用程式和資料流將會在 HTTTPS 之下。 開啟的內容，hello 播放程式不需要驗證或授權，因此您擁有 hello liberty toouse 是 HTTP 或 HTTPS。

### <a name="azure-active-directory-signing-key-rollover"></a>Azure Active Directory 簽署金鑰變換
這是重要的點 tootake 實作的考量。 如果您不會考慮此實作中，已完成的 hello 系統最後會完全位於最多 6 週停止運作。

Azure AD 會使用業界標準 tooestablish 信任其本身之間使用 Azure AD 的應用程式。 具體而言，Azure AD 使用簽署金鑰，該金鑰是由公開和私密金鑰組所組成。 當 Azure AD 會建立包含 hello 使用者的相關資訊的安全性權杖時，這個權杖是由使用其私密金鑰，然後才傳送出去後 toohello 應用程式的 Azure AD 中簽署。 hello 語彙基元的 tooverify 有效且確實來自 Azure AD，hello 應用程式必須驗證 hello 權杖之簽章使用 hello hello 租用戶同盟中繼資料文件中包含的 Azure AD 所公開的公開金鑰。 這個公用金鑰 – 和簽章的金鑰衍生出 hello – 是 hello 用於在 Azure AD 中的所有租用戶的同一個。

Azure AD 金鑰變換的詳細的資訊，請參閱 hello 文件：[重要資訊在 Azure AD 中簽署金鑰變換](../active-directory/active-directory-signing-key-rollover.md)。

Hello 之間[公開-私密金鑰組](https://login.microsoftonline.com/common/discovery/keys/)，

* 使用 hello 私密金鑰由 Azure Active Directory toogenerate JWT 權杖中。
* hello 公開金鑰用在 AMS tooverify hello JWT 權杖中; 例如 DRM 授權傳遞服務應用程式

基於安全性目的，Azure Active Directory 會定期替換此憑證 (每隔 6 週)。 發生安全性漏洞時 hello 金鑰變換可能會發生任何時間。 因此，在 AMS hello 授權傳遞服務需要 tooupdate hello 公開金鑰做為 Azure AD 會旋轉 hello 金鑰組，否則在 AMS 權杖驗證將會失敗並會發出任何授權。

設定 DRM 授權傳遞服務時，這是藉由設定 TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument 來達成。

hello JWT 權杖流程為如下：

1. Azure AD 會發出 hello JWT 權杖，hello 目前私密金鑰已驗證使用者;
2. 當播放程式看到 CENC 具有多重 DRM 保護內容時，它會先找出 hello Azure AD 所簽發的 JWT 語彙基元。
3. hello player AMS; 以傳送 hello JWT 語彙基元 toolicense 傳遞服務與授權擷取要求
4. AMS hello 授權傳遞服務會使用 hello 目前/有效公用的金鑰從 Azure AD tooverify hello JWT 權杖中，然後再發出授權。

DRM 授權傳遞服務永遠會檢查 hello 目前/有效公開金鑰從 Azure AD。 將用來驗證 Azure AD 所簽發的 JWT 語彙基元的 hello 金鑰 hello Azure AD 所呈現的公開金鑰。

如果之後 AAD 產生的 JWT 語彙基元，但玩家 tooDRM 授權傳遞服務會在 AMS 針對驗證權杖會傳送 hello JWT 之前，會發生情況 hello 金鑰變換？

因為金鑰可能會在任何時間變換，一定會一個以上有效的公開金鑰可用 hello 同盟中繼資料文件中。 Azure 媒體服務授權傳遞可使用任何 hello 指定索引鍵在 hello 文件，由於其中一個索引鍵可能會過期，所以另一個可能是一個取代，等等。

### <a name="where-is-hello-access-token"></a>其中是 hello 存取權杖？
如果您查看如何 web 應用程式呼叫 API 應用程式在[使用 OAuth 2.0 用戶端認證授與應用程式識別](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api)，hello 驗證流程為如下：

1. 使用者登入 tooAzure AD hello web 應用程式中 (請參閱 hello[應用程式的網頁瀏覽器 tooWeb](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application)。
2. hello Azure AD 授權端點重新導向 hello 使用者代理程式後 toohello 用戶端應用程式並提供授權碼。 hello 使用者代理程式傳回授權碼 toohello 用戶端應用程式的重新導向 URI。
3. hello web 應用程式需要 tooacquire 存取權杖，使其可以 toohello web API 進行驗證和擷取 hello 所需的資源。 它會要求 tooAzure AD 的權杖端點，以提供 hello 認證、 用戶端識別碼和 web API 的應用程式識別碼 URI。 它會呈現 hello 授權程式碼 tooprove 該 hello 使用者已經同意。
4. Azure AD 驗證 hello 應用程式，並傳回是使用的 toocall hello web API 的 JWT 存取權杖。
5. 透過 HTTPS，hello web 應用程式會使用 hello hello 要求 toohello web API hello 授權標頭中傳回 JWT 存取權杖 tooadd hello 含有"Bearer"稱號的 JWT 字串。 hello web 應用程式開發介面，然後驗證 hello JWT 權杖中，而如果驗證成功，傳回 hello 需要資源。

在 「 應用程式識別碼 」 流程中，hello web API 信任該 hello web 應用程式已驗證的 hello 使用者。 基於這個理由，這種模式稱為受信任子系統。 hello[此頁面上的圖表](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code)說明授權碼授與流程的運作方式。

在取得授權權杖的限制，我們會遵循 hello 相同的受信任的子系統模式。 Azure 媒體服務中的 hello 授權傳遞服務，且 hello web API 資源 hello 「 後端資源 」 的 web 應用程式需要 tooaccess。 因此，其中是 hello 存取權杖？

的確，我們會從 Azure AD 取得存取權杖。 使用者驗證成功之後，會傳回授權碼。 hello 授權程式碼接著會使用，以及用戶端識別碼和應用程式金鑰，tooexchange 存取權杖。 Hello 存取權杖是存取指向 「 指標 」 應用程式，或代表 Azure Media Services 授權傳遞服務。

我們需要 tooregister，並在 Azure AD 中的 hello 「 指標 」 應用程式設定下列 hello 步驟：

1. Hello Azure AD 租用戶中

   * 新增應用程式 (資源) 與登入 URL：

   https://[resource_name].azurewebsites.net/ 和

   * 應用程式識別碼 URL：

   https://[aad_tenant_name].onmicrosoft.com/[resource_name]；
2. 加入新的金鑰 hello 資源應用程式。
3. 更新 hello 應用程式資訊清單檔，使 hello groupMembershipClaims 屬性具有下列值的 hello:"groupMembershipClaims":"All"，  
4. Hello Azure AD 應用程式指向 toohello hello 區段 [權限 tooother applications] 中的，播放程式 web 應用程式中加入它上方步驟 1 中已加入 hello 資源應用程式。 在 [委派的權限] 底下勾選 [存取 [resource_name]] 核取記號。 如此 hello 的 web 應用程式權限 toocreate 存取權杖來存取 hello 資源應用程式。 您應該為此作業的 hello web 應用程式的本機和已部署版本如果您正在開發使用 Visual Studio 和 Azure web 應用程式。

因此，hello Azure AD 所簽發的 JWT 權杖確實是 hello 存取這項 「 指標 」 資源的存取權杖。

### <a name="what-about-live-streaming"></a>即時串流呢？
在上述的 hello，我們討論具有已將焦點放在隨資產。 即時串流呢？

hello 好消息是，您可以使用完全相同的設計和實作保護即時資料流在 Azure Media Services 中，將為"VOD asset"的程式相關聯的 hello 資產 hello。

具體來說，它是已知 toodo live streaming Azure Media Services 中，您需要 toocreate 通道，然後在 hello 通道下的程式。 toocreate hello 程式，您需要 toocreate 其中將包含 hello 程式 hello 即時封存資產。 中的 hello 實況內容，您只需要 toodo，多重 DRM 保護的順序 tooprovide CENC 會 tooapply hello 相同的安裝程式/處理 toohello 資產如同開始 hello 程式之前，它會是"VOD asset"。

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>在 Azure 媒體服務外部的授權伺服器呢？
通常，客戶可能會在他們自己的資料中心或由 DRM 服務提供者裝載的位置，投資授權伺服器陣列。 幸運的是，Azure 媒體服務內容保護可讓您 toooperate 以混合模式： 內容裝載，並動態地加以保護 Azure Media Services 中，雖然 DRM 授權都已傳遞方法外 Azure Media Services 的伺服器。 在此情況下，有下列變更的考量因素的 hello:

1. hello Secure Token Service 的需求 tooissue 語彙基元會被可接受和可驗證 hello 授權伺服器陣列。 比方說，Axinom 所提供的 hello Widevine 授權伺服器要求特定 JWT 權杖中包含 「 權利訊息 」。 因此，您需要 toohave STS tooissue 這類的 JWT 語彙基元。 hello 作者完這類實作，而且您可以找到 hello 詳細資料，在下列文件中的 hello [Azure 文件中心](https://azure.microsoft.com/documentation/):[使用 Axinom toodeliver Widevine 授權 tooAzure Media Services](media-services-axinom-integration.md).
2. 您不再需要 tooconfigure 授權傳遞服務 (ContentKeyAuthorizationPolicy) Azure 媒體服務中。 您的需要 toodo 是 tooprovide hello 授權取得 Url （針對 PlayReady、 Widevine 和 FairPlay） 中使用多重 DRM 設定 CENC 設定 AssetDeliveryPolicy 時。

### <a name="what-if-i-want-toouse-a-custom-sts"></a>如果我想 toouse 自訂 STS 嗎？
可能有少數客戶可能會選擇 toouse 自訂 STS (Secure Token Service) 提供的 JWT 權杖的原因。 以下是其中一些原因：

1. hello 身分識別提供者 (IDP) 使用 hello 客戶不支援 STS。 在此情況下，自訂 STS 是一個選項。
2. hello 客戶可能需要更多彈性或緊密控制中的客戶的訂閱者 」 計費系統整合 STS。 例如，MVPD 運算子可能提供 OTT 訂閱者的多個封裝，例如 premium、 basic、 運動、 等 hello 運算子可能會想要 toomatch hello 宣告在權杖中的訂閱者的封裝，如此只有 hello 右封裝中的內容開放使用。 在此情況下，自訂 STS 提供 hello 所需的彈性和控制。

兩項變更需要 toobe 時使用的自訂 STS:

1. 設定資產的授權傳遞服務時，您會需要用來驗證的 hello 自訂 STS （以下詳細說明），而不是從 Azure Active Directory 的 hello 目前金鑰 toospecify hello 安全性金鑰。
2. 產生 JTW 語彙基元時，而不是 hello 的 Azure Active Directory 中的 hello 目前 X509 憑證的私用金鑰指定的安全性金鑰。

有兩種類型的安全性金鑰：

1. 對稱金鑰： hello 產生和驗證 JWT 權杖中，使用相同的金鑰
2. 非對稱金鑰： 在 X509 憑證用於私用金鑰來加密/產生 JWT 語彙基元和 hello 公開金鑰來驗證 hello 語彙基元公開-私密金鑰組。

#### <a name="tech-note"></a>技術提示
如果您使用.NET Framework C# 開發平台，作為 hello X509 / 用於非對稱安全性金鑰的憑證必須具有金鑰長度至少為 2048年。 這是 hello 類別 System.IdentityModel.Tokens.X509AsymmetricSecurityKey.NET Framework 中的需求。 否則，會擲回下列例外狀況的 hello:

IDX10630: hello 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' 的簽章不能小於 '2048' 位元。

## <a name="hello-completed-system-and-test"></a>hello 完成系統和測試
我們將逐步引導幾個案例 hello 完成端對端系統中，讓讀者可以再取得登入帳戶有基本的 hello 行為的 「 圖片 」。

hello player web 應用程式和其登入可以找到[這裡](https://openidconnectweb.azurewebsites.net/)。

如果您需要的是 「 非整合式 」 案例： 哪些是未受保護或受 DRM 保護裝載在 Azure Media Services 視訊資產，但沒有 （發出要求的方式授權 toowhoever） 權杖的驗證，您可以測試它沒有登入 （藉由切換tooHTTP 如果視訊串流是透過 HTTP)。

如果您需要的是端對端整合的案例： 在 Azure Media Services 動態的 DRM 保護，權杖驗證與由 Azure AD 產生的 JWT 語彙基元是視訊資產，您需要 toologin。

### <a name="user-login"></a>使用者登入
在訂單 tootest hello 端對端整合 DRM 系統中，您需要 toohave 「 帳戶 」 建立或加入。

哪個帳戶？

雖然 Azure 原先只允許 Microsoft 帳戶使用者進行存取，但它現在可讓這兩個系統的使用者進行存取。 這項作業完成透過所有 hello Azure 屬性信任 Azure AD 進行驗證，讓 Azure AD 驗證組織使用者，以及建立的同盟關係讓 Azure AD 信任 hello Microsoft 帳戶消費者識別系統tooauthenticate 取用者的使用者。 如此一來，Azure AD 便能 tooauthenticate 「 來賓 」 Microsoft 帳戶，以及 「 原生 」 Azure AD 帳戶。

由於 Azure AD 信任 Microsoft 帳戶 (MSA) 網域，您可以加入任何帳戶，從任何 hello 下列網域 toohello 自訂的 Azure AD 租用戶，並使用 hello 帳戶 toologin:

| **網域名稱** | **網域** |
| --- | --- |
| **自訂 Azure AD 租用戶網域** |somename.onmicrosoft.com |
| **公司網域** |microsoft.com |
| **Microsoft 帳戶 (MSA) 網域** |outlook.com、live.com、hotmail.com |

您可以連絡任何 hello 作者 toohave 建立或加入為您的帳戶。

以下是不同的網域帳戶所使用的不同的登入頁面的 hello 螢幕擷取畫面。

**自訂的 Azure AD 租用戶的網域帳戶**： 在此情況下，請參閱 hello 自訂的 Azure AD 租用戶網域 hello 自訂登入頁面。

![自訂 Azure AD 租用戶網域帳戶](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Microsoft 網域帳戶使用智慧卡**： 在此情況下您會看到 hello 登入頁面自訂 microsoft 公司 IT 使用雙因素驗證。

![自訂 Azure AD 租用戶網域帳戶](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Microsoft 帳戶 (MSA)**： 在此情況下，您看到 hello Microsoft 帳戶登入頁面的消費者。

![自訂 Azure AD 租用戶網域帳戶](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Using Encrypted Media Extensions for PlayReady (使用 PlayReady 的加密媒體擴充)
在新式瀏覽器與加密媒體擴充功能 (EME) 的支援，例如 Windows 10 PlayReady 上的 Windows 8.1 和，IE 11 和 Microsoft Edge 瀏覽器將的 PlayReady hello EME 基礎 DRM。

![針對 PlayReady 使用 EME](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

hello 深色的播放程式區域是視訊的因為 toohello 事實 PlayReady 保護可防止一個進行螢幕擷取畫面的受保護。

hello 下列畫面顯示 hello player 外掛程式和 MSE/EME 支援。

![針對 PlayReady 使用 EME](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

Windows 10 的 Microsoft Edge 及 IE 11 中的 EME，允許支援 [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) 的 Windows 10 裝置上的 PlayReady SL3000 叫用。 PlayReady SL3000 解除鎖定 hello 資料流程增強的優質內容 (4k 首，等) 和新的內容傳遞模型 （如增強內容的早期視窗）。

專注於 hello Windows 裝置： PlayReady 是 hello 只在 Windows 裝置 (PlayReady SL3000) hello HW 中的 DRM。 串流服務可透過 EME 或 UWP 應用程式來使用 PlayReady，並利用 PlayReady SL3000 來提供比其他 DRM 所能提供更高的影片品質， 一般而言，2k 內容將通過 Chrome 或 Firefox，而且 4 K 透過 Microsoft Edge/IE11 或 UWP 應用程式內容 hello 相同裝置 （取決於服務設定和實作）。

#### <a name="using-eme-for-widevine"></a>針對 Widevine 使用 EME
Google Widevine EME/Widevine 上的支援，例如 Chrome 41 + Windows 10、 Windows 8.1、 Mac OSX Yosemite，以及 Chrome Android 的第 4.4.4 的新式瀏覽器是 hello EME 背後的 DRM。

![針對 Widevine 使用 EME](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

請注意，Widevine 不會防止對受保護的視訊進行螢幕擷取。

![針對 Widevine 使用 EME](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>不是有權限的使用者
如果使用者不是 「 標題為使用者 」 群組的成員，hello 使用者不會檢查無法 toopass 」 權限 」，而且 hello 多重 DRM 授權服務會拒絕 tooissue hello 要求的授權，如下所示。 hello 詳細的描述是 「 授權取得失敗 」，這是專為。

![無權限的使用者](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Running custom Secure Token Service (執行自訂安全權杖服務)
執行自訂安全性權杖服務 (STS) 中的 hello 案例中，hello JWT 權杖中將會發出 hello 自訂 STS 所使用對稱或非對稱金鑰。

使用對稱金鑰 （使用 Chrome） 的 hello 案例：

![執行自訂 STS](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

hello 案例使用非對稱金鑰透過 X509 憑證 （使用 Microsoft 新式瀏覽器）。

![執行自訂 STS](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

在這兩 hello 上述情況下，使用者驗證會 hello 相同 – 透過 Azure AD。 hello 唯一的差別在於 hello 自訂 STS，而不是 Azure AD 所簽發的 JWT 語彙基元。 當然，在設定動態 CENC 保護時，授權傳遞服務的 hello 限制指定 hello 類型 JWT 權杖中，對稱或非對稱金鑰。

## <a name="summary"></a>摘要
在本文件中，我們討論了透過權杖驗證的 CENC 與多重原生 DRM 和存取控制：它的設計和實作使用 Azure、Azure 媒體服務和 Azure Media Player。

* 其中包含 DRM/CENC 子系統; 中的 hello 必要元件會參考設計
* Azure、Azure 媒體服務和 Azure Media Player 的參考實作。
* 也會討論一些 hello 設計與實作中直接相關的主題。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
