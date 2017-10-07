---
title: "aaaHow toobuild 可以登入 Azure AD 中的任何使用者的應用程式 |Microsoft 文件"
description: "如何建置可讓使用者從任何 Azure Active Directory 租用戶登入之應用程式 (也稱為多租用戶應用程式) 的逐步解說。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>如何在任何 Azure Active Directory (AD) 使用者使用 toosign hello 多租用戶應用程式模式
如果您提供 「 軟體即服務應用程式 toomany 組織，您可以設定您應用程式 tooaccept 登入任何 Azure AD 租用戶。  在 Azure AD 中，這稱為讓您的應用程式成為多租用戶應用程式。  在任何 Azure AD 租用戶中的使用者將無法 tooyour 後的應用程式中無法 toosign 同意 toouse 其帳戶與您的應用程式。  

如果您的現有應用程式有其自己的帳戶系統，或支援從其他雲端提供者執行其他登入方式，則新增從任何租用戶執行 Azure AD 登入很簡單。 只要註冊您的應用程式、透過 OAuth2、OpenID Connect 或 SAML 新增登入程式碼，然後將 [使用 Microsoft 登入] 按鈕放在您的應用程式上即可。 按一下下列按鈕 toolearn 深入了解您的應用程式的商標 hello。

[![登入按鈕][AAD-Sign-In]][AAD-App-Branding]

本文假設您已經熟悉如何為 Azure AD 建置單一租用戶應用程式。  如果您不這樣做，head 備份 toohello[開發人員指南首頁][ AAD-Dev-Guide] ，然後再次嘗試我們的快速入門的其中一個 ！

有四個簡單步驟 tooconvert 到 Azure AD 多租用戶應用程式的應用程式：

1. 更新您的應用程式註冊 toobe 多租用戶
2. 更新您的程式碼 toosend 要求 toohello /common 端點 
3. 更新您的程式碼 toohandle 多個簽發者值
4. 了解使用者和系統管理員的同意意向並進行適當的程式碼變更

讓我們仔細看看每個步驟。 您也可以直接太跳[這份清單的多租用戶範例][AAD-Samples-MT]。

## <a name="update-registration-toobe-multi-tenant"></a>更新註冊 toobe 多租用戶
Azure AD 中的 Web 應用程式/API 註冊預設是單一租用戶。  您可以讓您註冊多租用戶尋找您的應用程式註冊在 hello hello 屬性頁面上的 hello"多 Tenanted"切換[Azure 入口網站][ AZURE-portal]並將其設定太"Yes"。

也請注意之前的應用程式可以由多租用戶，, Azure AD 需要 hello hello 應用程式 toobe 全域唯一的應用程式識別碼 URI。 hello 應用程式識別碼 URI 是應用程式識別通訊協定訊息中的 hello 方法之一。  單一租用戶應用程式中，就足夠 hello 應用程式識別碼 URI toobe 該租用戶中唯一的。  為多租用戶應用程式，它必須是全域唯一讓 Azure AD 可以跨所有租用戶尋找 hello 應用程式。  藉由要求 hello 應用程式識別碼 URI toohave 符合 hello Azure AD 租用戶的已驗證的網域主機名稱會強制執行全域的唯一性。  例如，如果您的租用戶的 hello 名稱 contoso.onmicrosoft.com 則有效應用程式識別碼 URI 會`https://contoso.onmicrosoft.com/myapp`。  如果租用戶具有已驗證的網域 `contoso.com`，則有效的「應用程式識別碼 URI」也會是 `https://contoso.com/myapp`。  Hello 應用程式識別碼 URI 未遵循此模式設定為多租用戶的應用程式將會失敗。

原生用戶端註冊預設即為多租用戶。  您不需要任何動作 toomake 的原生用戶端應用程式註冊多租用戶 tootake。

## <a name="update-your-code-toosend-requests-toocommon"></a>更新您的程式碼 toosend 要求太/一般
在單一租用戶應用程式中，登入要求會傳送 toohello 租用戶登入端點。 例如，如 contoso.onmicrosoft.com hello 端點將會是：

    https://login.microsoftonline.com/contoso.onmicrosoft.com

傳送要求的租用戶 tooa 端點中該租用戶中的租用戶 tooapplications 登入使用者 （或來賓）。  與多租用戶應用程式，並不知道 hello 應用程式最前面位置 hello 租用戶的使用者是從，因此無法傳送要求 tooa 租用戶端點。  相反地，要求會傳送信號分離跨所有的 Azure AD 租用戶的 tooan 端點：

    https://login.microsoftonline.com/common

當 Azure AD 會收到要求時在 hello/一般端點，它 hello 使用者登入，而結果會探索哪些租用戶 hello 使用者是從。  hello/一般端點可以使用所有的 hello Azure AD 支援的驗證通訊協定： OpenID Connect、 OAuth 2.0、 SAML 2.0 和 WS-同盟。

hello 登入回應 toohello 然後應用程式包含代表 hello 使用者的權杖。  hello 權杖中的 hello 簽發者值會告訴應用程式租用戶的 hello 使用者是從。  當回應會傳回從 hello/一般端點，hello 權杖中的 hello 簽發者值會對應 toohello 使用者的租用戶。  它是重要 toonote hello/一般端點不是租用戶，而且不是簽發者，只要多工器。  使用時 /common，在您的應用程式 toovalidate 權杖中的 hello 邏輯必須更新 toobe tootake 這納入考量。 

稍早提到、 多租用戶應用程式也應該為使用者提供一致的登入體驗，如下列 hello Azure AD 應用程式的商標指導方針。 按一下下列按鈕 toolearn 深入了解您的應用程式的商標 hello。

[![登入按鈕][AAD-Sign-In]][AAD-App-Branding]

讓我們看看 hello /common hello 使用端點和您的程式碼中實作更多詳細資料。

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>更新您的程式碼 toohandle 多個簽發者值
Web 應用程式和 Web API 會接收並驗證來自 Azure AD 的權杖。  

> [!NOTE]
> 在原生用戶端應用程式要求並接收來自 Azure AD 的權杖時，它們執行的動作是 toosend 它們 tooAPIs，驗證其中。  原生應用程式不會驗證權杖，而且必須將它們視為不透明。
> 
> 

讓我們看看應用程式如何驗證它從 Azure AD 接收的權杖。  單一租用戶應用程式通常會採用類似以下的端點值：

    https://login.microsoftonline.com/contoso.onmicrosoft.com

並使用它 tooconstruct 中繼資料 URL （在此情況下，OpenID Connect） 類似：

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload 兩個重要的資訊片段，這是使用的 toovalidate 權杖： hello 租用戶的簽署金鑰和簽發者值。  每個 Azure AD 租用戶的簽發者唯一值為 hello 表單：

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

其中 hello GUID 值是 hello hello 租用戶的租用戶識別碼 hello 重新命名安全版本。  如果您按一下前的中繼資料連結的 hello `contoso.onmicrosoft.com`，您可以看到這個 hello 文件中的簽發者值。

當單一租用戶應用程式會驗證權杖時，它會檢查 hello 權杖簽署金鑰 hello 中繼資料文件的 hello hello 簽章。 這可以讓它 toomake 確定 hello 簽發者值 hello 語彙基元的相符項目 hello 一個 hello 中繼資料文件中找到。

由於 hello/一般端點未對應 tooa 租用戶，而且不是簽發者，當您檢查 hello 中繼資料中的 hello 簽發者值/常見它具有一個樣板化的 URL，而不是實際的值：

    https://sts.windows.net/{tenantid}/

因此，多租用戶應用程式時，無法只藉由比對以 hello hello 中繼資料中的 hello 簽發者值驗證語彙基元`issuer`hello 權杖中的值。  多租用戶應用程式的簽發者值有效，而且可不需要邏輯 toodecide，根據 hello 租用戶識別碼部分 hello 簽發者值。  

例如，如果多租用戶應用程式僅允許登入特定的租用戶已註冊的服務，然後它必須檢查 hello 簽發者值或 hello`tid`宣告在 hello 語彙基元 toomake 確定該租用戶的清單中的值訂閱者。  如果多租用戶應用程式僅處理個人版，並沒有做出任何存取根據租用戶，則其可以忽略 hello 簽發者值完全。

在 hello hello 多租用戶範例[相關內容](#related-content)在本文中，簽發者驗證的 hello 結尾的區段是已停用的 tooenable 中的任何 Azure AD 租用戶 toosign。

現在讓我們看看 hello 登入 toomulti 租用戶應用程式的使用者的使用者體驗。

## <a name="understanding-user-and-admin-consent"></a>了解使用者和系統管理員的同意意向
Hello 應用程式必須針對使用者 toosign tooan 在 Azure AD 中的應用程式中，表示 hello 使用者的租用戶中。  這可讓組織 hello toodo 等項目套用唯一的原則，從其租用戶的使用者登入時 toohello 應用程式。  單一租用戶應用程式中，此註冊很簡單;它具有 hello hello 註冊 hello 應用程式時，會發生情況的其中一個[Azure 入口網站][AZURE-portal]。

為多租用戶應用程式，hello hello 應用程式的初始註冊位於 hello hello 開發人員所使用的 Azure AD 租用戶。  當使用者從不同的租用戶登入時 toohello 應用程式的 hello 第一次時，Azure AD 會要求他們 hello 應用程式所要求的 tooconsent toohello 權限。  如果他們同意，則 hello 應用程式的表示法稱為*服務主體*中建立 hello 使用者的租用戶，而且登入可以繼續。 委派，也會建立 hello 記錄 hello 使用者同意 toohello 應用程式的目錄中。 請參閱[應用程式與服務主體物件][ AAD-App-SP-Objects]需 hello 應用程式的應用程式和 ServicePrincipal 物件，和如何彼此 tooeach 其他詳細資料。

![同意 toosingle 層應用程式][Consent-Single-Tier] 

此同意體驗會受到 hello hello 應用程式所要求的權限。  Azure AD 支援兩種類型的權限，即僅限應用程式的權限和委派的權限︰

* 委派的權限授與應用程式 hello 能力 tooact，登入的使用者子集的 hello 事項 hello 使用者一樣。  例如，您可以授與登入使用者的行事曆應用程式 hello 委派權限 tooread hello。
* 僅限應用程式的權限授與直接 toohello hello 應用程式識別。  例如，您可以授與的應用程式 hello 僅限應用程式的權限 tooread hello 清單中的租用戶，不論使用者登入 toohello 應用程式的使用者。

某些權限可以是已獲得同意的 tooby 一般使用者，而有些則需要在租用戶系統管理員的同意。 

### <a name="admin-consent"></a>系統管理員同意
僅限應用程式的權限一律需要租用戶系統管理員的同意。  如果您的應用程式要求僅限應用程式的權限，而且使用者嘗試 toosign toohello 應用程式中的，將指出 hello 使用者不能 tooconsent 顯示錯誤訊息。

有些委派的權限也需要租用戶系統管理員的同意。  比方說，hello 能力 toowrite 後 tooAzure AD hello 登入的使用者為要求的租用戶系統管理員同意。  僅限應用程式的權限，例如，如果一般的使用者嘗試 toosign tooan 要求需要管理員同意的委派權限的應用程式中您的應用程式會收到錯誤。  需要權限獲得管理員同意取決於發行 hello 資源的 hello 開發人員，而且可以在 hello 文件以 hello 資源中找到。  連結 tootopics 說明 hello 可用權限 hello Azure AD Graph API 和 Microsoft Graph API 位於 hello[相關內容](#related-content)本文一節。

如果您的應用程式使用需要獲得管理員同意權限，您會需要 toohave 手勢，例如按鈕或連結 hello 系統管理員可以在其中啟動 hello 動作。  您的應用程式傳送這個動作是一般 OAuth2/OpenID Connect 授權要求，但也包含 hello hello 要求`prompt=admin_consent`查詢字串參數。  後續登入要求之後 hello 系統管理員同意和 hello 客戶的租用戶建立 hello 服務主體，不需要 hello`prompt=admin_consent`參數。 Hello 系統管理員決定 hello 要求權限是可接受，因為將會從該點之後的同意不提示 hello 租用戶中的任何其他使用者。

hello`prompt=admin_consent`要求權限，不需要獲得管理員同意的應用程式也可以使用參數。 這是當 hello 應用程式需要體驗其中 hello 租用戶系統管理員 「 註冊 」 一次，且沒有其他系統會提示使用者的同意層級從該點上。

如果應用程式需要系統管理員同意和管理員簽署在但 hello`prompt=admin_consent`參數不會傳送、 hello 系統管理員已成功將同意 toohello 應用程式**只為其使用者帳戶**。  一般使用者仍不會在無法 toosign 和同意 toohello 應用程式。  這非常有用，如果您想 toogive hello 租用戶系統管理員 hello 能力 tooexplore 您的應用程式，才能允許其他使用者的存取。

租用戶系統管理員可以停用一般使用者 tooconsent tooapplications hello 能力。  這項功能已停用，都一律需要 hello hello 租用戶中設定的應用程式 toobe 獲得管理員同意。  如果您想的 tootest 停用您的應用程式，一般使用者同意的情況下，您可以找到 hello 的組態參數： hello Azure AD 租用戶中的 hello 的組態區段[Azure 入口網站][AZURE-portal]。

> [!NOTE]
> 某些應用程式想要運作的一般使用者能 tooconsent 一開始，而稍後 hello 應用程式可能是 hello 系統管理員並要求權限的系統管理員同意體驗。  沒有任何方式 toodo 這與單一應用程式註冊在現今 Azure AD 中。  hello 即將推出的 Azure AD v2 端點可讓應用程式 toorequest 權限，在執行階段，而不是在登錄時，會啟用此案例。  如需詳細資訊，請參閱 hello [Azure AD 應用程式模型 v2 開發人員指南][AAD-V2-Dev-Guide]。
> 
> 

### <a name="consent-and-multi-tier-applications"></a>同意和多層應用程式
您的應用程式可能會有多層，每一層皆由它自己在 Azure AD 中的註冊代表。  例如，一個呼叫 Web API 的原生應用程式，或是一個呼叫 Web API 的 Web 應用程式。  在這兩種情況下，hello 用戶端 （原生應用程式或 web 應用程式） 會要求權限 toocall hello 資源 (web 應用程式開發介面)。  針對 hello 用戶端 toobe 成功同意至客戶的租用戶，它會要求權限的所有資源 toowhich 必須存都在於 hello 客戶的租用戶。  如果不符合此條件，Azure AD 會傳回必須先新增 hello 資源時發生錯誤。

**單一租用戶中的多層**

如果您的邏輯應用程式包含兩個或更多個應用程式註冊 (例如個別的用戶端和資源)，這可能會造成問題。  如何取得 hello 資源 hello 客戶租用戶到第一個？  Azure AD 涵蓋此案例藉由啟用用戶端和資源 toobe 同意以單一步驟。 hello 使用者會看見 hello 總和的 hello hello 用戶端和 hello 同意頁面上的資源要求的權限。  tooenable 這種行為，hello 資源的應用程式註冊必須包含 hello 用戶端應用程式識別碼，表示為`knownClientApplications`應用程式資訊清單中。  例如：

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

此屬性可以透過 hello 資源更新[應用程式的資訊清單][AAD-App-Manifest]。 這示範於多層式的原生用戶端，在 hello 呼叫 web API 範例[相關內容](#related-content)hello 本文結尾 > 一節。 hello 圖概略說明同意在單一租用戶中註冊之多層式應用程式：

![同意 toomulti 層已知的用戶端應用程式][Consent-Multi-Tier-Known-Client] 

**多個租用戶中的多層**

如果 hello 不同的應用程式層會在不同的租用戶中註冊，則會發生類似的案例。  例如，請考慮 hello 的建置呼叫 hello Office 365 Exchange Online API 的原生用戶端應用程式的大小寫。  應用程式，及更新版本的客戶的租用戶中的 hello 原生應用程式 toorun，toodevelop hello 原生、 hello Exchange Online 服務主體必須存在。  在此情況下，hello 開發人員和客戶購買 Exchange Online 的 hello 服務主體 toobe 其租用戶中建立。  

在應用程式開發介面，由 Microsoft 以外的組織所建立的 hello 情況下，hello 的 hello API 的開發人員必須 tooprovide 方式他們的客戶 tooconsent hello 的應用程式至其客戶的租用戶。 hello 建議設計為 hello 第 3 個合作對象開發人員 toobuild hello 應用程式開發介面，它也可以當作 web 用戶端 tooimplement 註冊：

1. 請遵循 hello 先前各節 tooensure hello API 實作 hello 多租用戶應用程式登錄/程式碼的需求
2. 此外 tooexposing hello 應用程式開發介面的範圍/角色，請確定 hello 註冊包含 hello 」 登入並讀取使用者設定檔"（預設值所提供） 的 Azure AD 權限
3. 在 hello web 用戶端，遵循 hello 中實作登在 /-註冊頁面[獲得管理員同意](#admin-consent)先前討論一般指導方針 
4. 一旦 hello 使用者同意 toohello 應用程式，hello 服務主體和同意委派連結便會建立在其租用戶和 hello 原生應用程式可以取得 hello API 的語彙基元

下列圖表中的 hello 概略說明同意在不同的租用戶中註冊之多層式應用程式：

![同意 toomulti 層多方應用程式][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>撤銷同意
使用者和系統管理員可以撤銷同意 tooyour 應用程式在任何時間：

* 使用者撤銷存取 tooindividual 應用程式移除它們從其[存取面板應用程式][ AAD-Access-Panel]清單。
* 系統管理員移除 hello hello Azure AD 管理一節，使用 Azure AD 撤銷存取 tooapplications [Azure 入口網站][AZURE-portal]。

如果系統管理員同意時 tooan 租用戶中的所有使用者的應用程式，使用者就無法個別撤銷存取權。  只有 hello 系統管理員可以撤銷存取權，而且只會針對 hello 整個應用程式。

### <a name="consent-and-protocol-support"></a>同意和通訊協定支援
同意 hello OAuth、 OpenID Connect，透過 Azure ad 支援 WS-同盟和 SAML 通訊協定。  hello SAML 和 WS-同盟通訊協定不支援 hello`prompt=admin_consent`參數，因此系統管理員同意才可透過 OAuth 和 OpenID Connect。

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>多租用戶應用程式和快取存取權杖
多租用戶應用程式也可以取得存取權杖 toocall Azure AD 所保護的應用程式開發介面。  使用 hello Active Directory 驗證程式庫 (ADAL) 的多租用戶應用程式時常見的錯誤 tooinitially 要求使用者使用 /common 語彙基元、 接收回應，然後要求該相同的使用者，同時也使用 /common 後續的權杖。  因為從 Azure AD 的 hello 回應不會從租用戶，/通用，ADAL 會快取為來自 hello 租用戶的 hello 語彙基元。 hello 後續呼叫太/一般 tooget hello 使用者遺漏 hello 快取項目和 hello 使用者的存取權杖是提示的 toosign 中一次。  tooavoid 遺漏 hello 快取，請確定後續已登入的使用者會呼叫 toohello 租用戶端點。

## <a name="next-steps"></a>後續步驟
在本文中，您學到如何 toobuild 可以登入任何 Azure Active Directory 租用戶中的應用程式。 啟用單一登入您的應用程式與 Azure Active Directory 之間之後, 您也可以更新您的應用程式 tooaccess Microsoft 資源，例如 Office 365 所公開的 Api。 因此您可以提供個人化的經驗中您的應用程式，例如顯示 toohello 使用者，其設定檔圖片或其下一個行事曆約會等內容的相關資訊。 toolearn 深入了解進行 API 呼叫 tooAzure Active Directory 和 Office 365 服務，例如 Exchange、 SharePoint、 OneDrive、 OneNote、 Planner、 Excel 和詳細資訊，請造訪： [Microsoft Graph API][MSFT-Graph-overview]。


## <a name="related-content"></a>相關內容
* [多租用戶應用程式範例][AAD-Samples-MT]
* [應用程式的商標指導方針][AAD-App-Branding]
* [Azure AD 開發人員指南][AAD-Dev-Guide]
* [應用程式物件和服務主體物件][AAD-App-SP-Objects]
* [整合應用程式與 Azure Active Directory][AAD-Integrating-Apps]
* [Hello 同意架構的概觀][AAD-Consent-Overview]
* [Microsoft Graph API 權限範圍][MSFT-Graph-permision-scopes]
* [Azure AD Graph API 權限範圍][AAD-Graph-Perm-Scopes]

請使用下列註解區段 tooprovide 意見反應的 hello，並協助我們改善並圖形內容。

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














