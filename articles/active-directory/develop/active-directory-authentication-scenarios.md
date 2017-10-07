---
title: "Azure AD 的案例 aaaAuthentication |Microsoft 文件"
description: "Hello 五個最常見的驗證案例的 Azure Active Directory (AAD) 的概觀"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Azure AD 的驗證案例
Azure Active Directory (Azure AD) 形式提供身分識別服務，以支援業界標準通訊協定例如 OAuth 2.0 和 OpenID Connect，以及開放原始碼程式庫，針對不同平台 toohelp 您簡化開發人員的驗證開始撰寫程式碼快速。 本文件將協助您了解 hello 各種案例 Azure AD 支援，而且會顯示 tooget 的啟動方式。 分成下列各節的 hello:

* [Azure AD 中的驗證基本概念](#basics-of-authentication-in-azure-ad)
* [Azure AD 安全性權杖中的宣告](#claims-in-azure-ad-security-tokens)
* [在 Azure AD 中登錄應用程式的基本概念](#basics-of-registering-an-application-in-azure-ad)
* [應用程式類型和案例](#application-types-and-scenarios)
  
  * [Web 瀏覽器 tooWeb 應用程式](#web-browser-to-web-application)
  * [單一頁面應用程式 (SPA)](#single-page-application-spa)
  * [原生應用程式 tooWeb 應用程式開發介面](#native-application-to-web-api)
  * [Web 應用程式 tooWeb 應用程式開發介面](#web-application-to-web-api)
  * [精靈或伺服器應用程式 tooWeb 應用程式開發介面](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Azure AD 中的驗證基本概念
如果您不熟悉 Azure AD 中的驗證基本概念，請閱讀本節。 否則，您可能會想 tooskip 向太[應用程式類型和案例](#application-types-and-scenarios)。

讓我們看一下 hello 最基本的案例中需要身分識別的地方： 使用者在網頁瀏覽器需要 tooauthenticate tooa web 應用程式。 Hello 中更詳細描述此案例[應用程式的網頁瀏覽器 tooWeb](#web-browser-to-web-application)  區段中，但它的有效開始點 tooillustrate hello Azure AD 功能和概念 hello 案例的運作方式。 請考慮 hello 遵循此案例的圖表：

![登入 tooweb 應用程式的概觀](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

與 hello 圖記住，以下是您的需要 tooknow 有關其各種的元件：

* Azure AD 是 hello 身分識別提供者，負責確認 hello 識別的使用者和組織的目錄中的應用程式，以及最後發行這些使用者和應用程式驗證成功後的安全性權杖。
* 想 toooutsource 驗證 tooAzure AD 應用程式必須註冊在 Azure AD 中註冊並唯一識別 hello hello 目錄中的應用程式。
* 開發人員可以使用 hello 開放原始碼 Azure AD 驗證程式庫 toomake 驗證容易藉由為您處理 hello 通訊協定詳細資料。 如需詳細資訊，請參閱 [Azure Active Directory 驗證程式庫](active-directory-authentication-libraries.md) 。

• 一次使用者已驗證、 hello 應用程式必須驗證 hello 使用者的安全性語彙基元 tooensure 的 hello 能用於合作對象的驗證已成功。 開發人員可以使用提供的任何權杖驗證程式庫 toohandle 驗證從 Azure AD，包括 JSON Web Token (JWT) 或 SAML 2.0 hello。 若要手動 tooperform 驗證，請參閱 hello [JWT 權杖處理常式](https://msdn.microsoft.com/library/dn205065.aspx)文件。

> [!IMPORTANT]
> Azure AD 使用公開金鑰密碼編譯 toosign 語彙基元，並確認它們都有效。 請參閱[重要資訊有關簽署金鑰變換在 Azure AD 中](active-directory-signing-key-rollover.md)如需詳細資訊在 hello 必要邏輯上，您必須在應用程式 tooensure 一律以更新 hello 最新的索引鍵。
> 
> 

• hello 流程要求和回應 hello 驗證程序由 hello 驗證通訊協定所使用，例如 OAuth 2.0、 OpenID Connect、 Ws-federation 或 SAML 2.0。 在 hello 中詳細討論這些通訊協定[Azure Active Directory 驗證通訊協定](active-directory-authentication-protocols.md)主題和 hello 的以下各節中。

> [!NOTE]
> Azure AD 支援 OAuth 2.0 hello 和廣泛的 OpenID Connect 標準使用持有者權杖，包括以 Jwt 表示的持有者權杖。 承載權杖是輕巧型的安全性權杖會授與 hello"bearer"存取 tooa 受保護資源。 就這個意義而言，hello"bearer"是指可出示 hello 語彙基元任何一方。 合作對象必須先通過驗證 Azure AD tooreceive hello 持有者權杖，必要時 hello toosecure 傳輸和儲存體中的 hello 語彙基元不採取步驟，但它可以攔截和使用非預期的合作對象。 雖然某些安全性權杖都有內建的機制，可防止未經授權的人士使用權杖，但持有者權杖沒有這項機制，而必須以安全通道來傳輸，例如傳輸層安全性 (HTTPS)。 持有人權杖傳送 hello 清除中時，如果攔截 hello 攻擊可由惡意的合作對象 tooacquire hello 語彙基元，並使用未經授權的存取 tooa 受保護資源的。 hello 儲存或快取持有者權杖供以後使用時，適用相同的安全性原則。 務必確定您的應用程式以安全的方式傳輸和儲存持有者權杖。 關於持有者權杖的其他安全性考量，請參閱 [RFC 6750 第 5 節](http://tools.ietf.org/html/rfc6750)。
> 
> 

您已經有概觀 hello 基本概念，讀取 toounderstand 下方的 hello 區段如何在 Azure AD 中佈建運作方式及 hello Azure AD 支援常見案例。

## <a name="claims-in-azure-ad-security-tokens"></a>Azure AD 安全性權杖中的宣告
Azure AD 所簽發的安全性權杖包含宣告或判斷提示的已驗證的 hello 主題的資訊。 這些宣告可供 hello 應用程式的各種工作。 例如，它們可以是使用的 toovalidate hello 語彙基元、 識別 hello 主旨目錄租用戶、 顯示使用者資訊、 判斷 hello 主旨授權等等。 任何指定的安全性權杖中的 hello 宣告是權杖的依存於 hello 的型別、 hello 類型使用的認證 tooauthenticate hello 使用者，以及 hello 應用程式組態。 下列的 hello 資料表中會提供每個 Azure AD 所發出的宣告類型的簡短描述。 如需詳細資訊，請參閱太[支援權杖和宣告類型](active-directory-token-and-claims.md)。

| 宣告 | 說明 |
| --- | --- |
| 應用程式識別碼 |識別正在使用 hello 語彙基元的 hello 應用程式。 |
| 對象 |識別 hello 收件者資源 hello 權杖是否適用於。 |
| 應用程式驗證內容類別參考 |指出 hello 用戶端的已驗證 （公用用戶端 vs.機密用戶端） 的方式。 |
| 驗證即刻 |記錄 hello hello 驗證發生時日期和時間。 |
| 驗證方法 |表示 hello hello 權杖主體的驗證方式 （密碼、 憑證等）。 |
| 名字 |提供 Azure AD 中設定 hello hello 使用者指定名稱。 |
| 群組 |包含物件識別碼的 Azure AD hello 使用者群組的成員。 |
| 識別提供者 |記錄 hello 驗證 hello hello 權杖主體的身分識別提供者。 |
| 發出時間 |記錄 hello 的 hello 權杖的發出時間，通常用於權杖的有效性。 |
| 簽發者 |識別 hello STS 發出 hello 語彙基元，以及 hello Azure AD 租用戶。 |
| 姓氏 |提供 Azure AD 中設定 hello hello 使用者姓氏。 |
| 名稱 |提供人類可讀取的值，以識別 hello 主體 hello 語彙基元。 |
| 物件識別碼 |包含 Azure AD 中的 hello 主旨不變且唯一識別項。 |
| 角色 |包含的易記名稱的 Azure AD 應用程式角色 hello 使用者已授與。 |
| Scope |指出 hello 權限授與 toohello 用戶端應用程式。 |
| 主旨 |指出哪些 hello 權杖判斷提示的相關資訊的 hello 主體。 |
| 租用戶識別碼 |包含權杖 hello hello 目錄租用戶不變且唯一的識別碼。 |
| 權杖存留期 |定義權杖的有效 hello 時間間隔。 |
| 使用者主體名稱 |包含 hello hello 主體的使用者主體名稱。 |
| 版本 |包含 hello 語彙基元 hello 版本號碼。 |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>在 Azure AD 中登錄應用程式的基本概念
將工作委外驗證 tooAzure AD 必須註冊在目錄中的任何應用程式。 此步驟涉及向 Azure AD 說明您的應用程式，包括其所在的 hello URL，您的應用程式及其他驗證後，hello URI tooidentify 中回覆 hello URL toosend。 需要這項資訊有幾個主要理由：

* Azure AD 在處理登入或交換權杖時，需要座標 toocommunicate 與 hello 應用程式。 這些需求包括下列 hello:
  
  * 應用程式的應用程式識別碼 URI: hello 識別碼。 這個值會傳送哪些應用程式 hello 呼叫端需要之權杖的驗證 tooindicate 期間 tooAzure AD。 此外，這個值會包含在 hello 語彙基元因此 hello 應用程式知道它就是 hello 適合目標。
  * 回覆 URL 和重新導向 URI： 在 web API 或 web 應用程式的 hello 情況下，hello 回覆 URL 是 hello 位置 toowhich Azure AD 會傳送 hello 驗證回應，包括權杖，如果驗證成功。 在原生應用程式的 hello 情況下，hello 重新導向 URI 是唯一的識別項 toowhich Azure AD 將會重新導向 hello 使用者代理程式在 OAuth 2.0 要求中。
  * 應用程式識別碼： hello 的應用程式，由 Azure AD 註冊 hello 應用程式時所產生的識別碼。 當要求授權碼或權杖，hello 應用程式識別碼和金鑰會傳送 tooAzure AD 在驗證期間。
  * 驗證 tooAzure AD toocall web API 時，會將應用程式識別碼一起傳送索引鍵： hello 索引鍵。
* Azure AD 需要 tooensure hello 應用程式有 hello 您目錄的資料，您的組織中其他應用程式的必要權限 tooaccess 等等

當您了解可以開發及與 Azure AD 整合的應用程式有兩種類別時，佈建就變得更清楚：

* 單一租用戶應用程式：單一租用戶應用程式適合在一個組織中使用。 這些通常是由企業開發人員撰寫的企業營運 (LoB) 應用程式。 單一租用戶應用程式只需要一個目錄中的使用者存取 toobe，如此一來，它只需要 toobe 佈建一個目錄中。 這些應用程式通常是由開發人員在 hello 組織中註冊。
* 多租用戶應用程式：多租用戶應用程式適合在許多組織中使用，而不只一個組織。 這些通常是由獨立軟體廠商 (ISV) 撰寫的軟體即服務 (SaaS) 應用程式。 多租用戶應用程式需要在每個目錄中會使用這些，需要使用者或系統管理員同意 tooregister 中佈建 toobe 它們。 應用程式已註冊 hello 目錄中，且會指定存取 toohello Graph API 或其他 web API 時，就會啟動此同意程序。 當使用者或系統管理員身分從不同的組織註冊 toouse hello 應用程式，他們會看到一個對話方塊，顯示 hello hello 應用程式所需的權限。 hello 使用者或系統管理員可以同意 toohello 應用程式，它將提供 hello 應用程式存取 toohello 所述的資料，並暫存器最後 hello 他們的目錄中的應用程式。 如需詳細資訊，請參閱[hello 同意架構的概觀](active-directory-integrating-applications.md#overview-of-the-consent-framework)。

開發多租用戶應用程式，而非單一租用戶應用程式時，有一些其他考量需要注意。 例如，如果您要進行您應用程式可用 toousers 多個目錄中，您需要機制 toodetermine 它們在哪個租用戶。 單一租用戶應用程式只需要 toolook 它自己的目錄中的使用者，而多租用戶應用程式需要 tooidentify 所有 hello 目錄的特定使用者在 Azure AD 中。 tooaccomplish 這個工作中，Azure AD 提供的任何多租用戶應用程式可以直接登入要求，而非租用戶專用端點的其中一個共同驗證端點。 這個端點是在 Azure AD 中 https://login.microsoftonline.com/common 所有目錄，而租用戶專用端點可能是 https://login.microsoftonline.com/contoso.onmicrosoft.com。hello 一般端點時，特別是重要的 tooconsider 開發應用程式，因為您將需要 hello 必要的邏輯 toohandle 多個租用戶在登入、 登出和權杖驗證期間。

如果您目前在開發單一租用戶應用程式，但想 toomake 它可用 toomany 組織中，您可以輕鬆地進行變更 toohello 應用程式和其組態在 Azure AD toomake 它能夠多租用戶。 此外，Azure AD 會使用 hello 相同簽署所有目錄中的所有權杖的金鑰是否您提供的單一租用戶或多租用戶應用程式中的驗證。

本文件列出的每個案例都有一個小節來說明其佈建需求。 如需深入了解有關佈建 Azure AD 中的應用程式和 hello 單一和多租用戶應用程式之間的差異，請參閱[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)如需詳細資訊。 繼續在 Azure AD 中讀取 toounderstand hello 常見的應用程式案例。

## <a name="application-types-and-scenarios"></a>應用程式類型和案例
每一個 hello 這份文件中所述的案例可以使用各種語言與平台進行開發。 它們都所有由完整的程式碼範例，可在我們[程式碼範例會引導](active-directory-code-samples.md)，或直接從 hello 對應[GitHub 範例儲存機制](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory)。 此外，如果您的應用程式需要端對端案例的特定片段或區段，在大部分情況下可以獨立加入這項功能。 例如，如果您有呼叫 web API 的原生應用程式，您可以輕鬆加入 web 應用程式也會呼叫 hello web API。 hello 下列圖表說明這些案例和應用程式類型，以及您可新增不同的元件：

![應用程式類型和案例](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

這些是 hello Azure AD 支援五個主要的應用程式案例：

* [Web 應用程式的瀏覽器 tooWeb](#web-browser-to-web-application)： 使用者需要 toosign Azure AD 所保護的 tooa web 應用程式中。
* [單一頁面應用程式 (SPA)](#single-page-application-spa)： 使用者需要 toosign tooa 單一頁面應用程式中，Azure AD 所保護。
* [原生應用程式 tooWeb API](#native-application-to-web-api): 原生應用程式上執行的電話、 平板電腦或電腦的需求 tooauthenticate 使用者 tooget 資源 web API 從 Azure AD 所保護。
* [Web 應用程式 tooWeb API](#web-application-to-web-api): web 應用程式需要從 Azure AD 所保護的 web API 的 tooget 資源。
* [精靈或伺服器應用程式 tooWeb API](#daemon-or-server-application-to-web-api)： 需要從 Azure AD 所保護的 web API 的 tooget 資源精靈應用程式或伺服器應用程式與 web 使用者介面。

### <a name="web-browser-tooweb-application"></a>Web 瀏覽器 tooWeb 應用程式
本章節描述來驗證使用者 web 瀏覽器 tooa web 應用程式中的應用程式。 在此案例中，hello web 應用程式會引導 hello 使用者的瀏覽器 toosign tooAzure AD 中。 Azure AD 傳回的登入回應透過 hello 使用者的瀏覽器，其中包含關於安全性權杖中的 hello 使用者宣告。 這個案例支援登入使用 hello WS-同盟、 SAML 2.0 和 OpenID Connect 通訊協定。

#### <a name="diagram"></a>圖表
![瀏覽器 tooweb 應用程式的驗證流程](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>通訊協定流程的描述
1. 當使用者造訪 hello 應用程式，且需要 toosign 中時，會被重新導向透過登入要求 toohello 驗證端點在 Azure AD 中。
2. hello 使用者登入 hello 登入頁面。
3. 如果驗證成功，Azure AD 會建立驗證權杖，並傳回 hello Azure 入口網站中設定的登入回應 toohello 應用程式的回覆 URL。 對於實際執行應用程式，此回覆 URL 應該為 HTTPS。 hello 傳回權杖包含關於 hello 使用者和 Azure AD 所需的 hello 應用程式 toovalidate hello 權杖的宣告。
4. hello 應用程式會使用公開簽署金鑰和簽發者資訊 hello 同盟中繼資料文件在 Azure AD 的驗證 hello 語彙基元。 Hello 應用程式會驗證 hello 語彙基元之後，Azure AD 會啟動新的工作階段與 hello 使用者。 此工作階段在到期之前，允許 hello 使用者 tooaccess hello 應用程式。

#### <a name="code-samples"></a>程式碼範例
請參閱網頁瀏覽器 tooWeb 應用程式案例的 hello 程式碼範例。 而且，請經常回來查看--我們隨時都 hello 加入新的範例。 [Web 應用程式的瀏覽器 tooWeb](active-directory-code-samples.md#web-browser-to-web-application)。

#### <a name="registering"></a>註冊
* 單一租用戶： 如果您要建置應用程式只會為您的組織，它必須註冊您的公司目錄中使用 hello Azure 入口網站。
* 多租用戶： 如果您要建置的應用程式，可供組織外的使用者，必須註冊在公司的目錄中，但也必須在每個組織的目錄將會使用 hello 應用程式中註冊。 toomake 至他們的目錄中可用的應用程式，您可以為您的客戶，讓他們 tooconsent tooyour 應用程式包含註冊程序。 當他們註冊您的應用程式 」 時，它們會顯示一個對話方塊，其中顯示 hello 權限 hello 應用程式需要，然後 hello tooconsent 選項。 視 hello 所需的權限，系統管理員可以在 hello 另一個組織可能會需要 toogive 同意。 當 hello 使用者或系統管理員同意時，hello 應用程式會註冊在他們的目錄。 如需詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。

#### <a name="token-expiration"></a>權杖到期
hello 的 hello Azure AD 所簽發的權杖的存留時間過期時，就會過期 hello 使用者工作階段。 如有需要，您的應用程式可以縮短這段時間，例如因為一段時間沒有活動而將使用者登出。 Hello 工作階段到期，hello 使用者將會是提示的 toosign 中一次。

### <a name="single-page-application-spa"></a>單一頁面應用程式 (SPA)
本章節描述的單一頁面應用程式，使用 Azure AD 驗證並 hello OAuth 2.0 隱含授權授與的 toosecure 其 web API 後端。 單一頁面應用程式通常會結構化為 hello 瀏覽器和伺服器執行的 Web API 後端中執行 JavaScript 展示層級 （前端），並實作 hello 應用程式的商務邏輯。 toolearn 進一步了解 hello 隱含授權授與，並協助您決定是否適合您應用程式的案例，請參閱[了解 hello OAuth2 隱含授予 Azure Active Directory 中的資料流程](active-directory-dev-understanding-oauth2-implicit-grant.md)。

在此案例中，當 hello 使用者登入時，hello JavaScript 前端會使用[Active Directory Authentication Library for JavaScript (ADAL。JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) hello 隱含授權授予 tooobtain ID 權杖 (id_token) 從 Azure AD。 hello 權杖進行快取並 hello 用戶端將其附加 toohello 要求為 hello 持有人權杖時進行呼叫 tooits Web API 後端，這使用 hello OWIN 中介軟體來保護。 

#### <a name="diagram"></a>圖表
![單一頁面應用程式圖表](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>通訊協定流程的描述
1. hello 使用者瀏覽 toohello web 應用程式。
2. hello 應用程式會傳回 hello JavaScript 前端 （顯示層） toohello 瀏覽器。
3. hello 使用者開始登入，例如按一下登入連結。 hello 瀏覽器傳送 GET toohello Azure AD 授權端點 toorequest ID 語彙基元。 此要求包含在 hello 查詢參數中的 hello 應用程式識別碼和回覆 URL。
4. Azure AD 會驗證的 hello hello 針對回覆 URL 註冊 hello Azure 入口網站中設定的回覆 URL。
5. hello 使用者登入 hello 登入頁面。
6. 如果驗證成功，Azure AD 會建立 ID 權杖，並傳回做為 URL fragment （#） toohello 應用程式的回覆 URL。 對於實際執行應用程式，此回覆 URL 應該為 HTTPS。 hello 傳回權杖包含關於 hello 使用者和 Azure AD 所需的 hello 應用程式 toovalidate hello 權杖的宣告。
7. hello 瀏覽器中執行的 hello JavaScript 用戶端程式碼從 hello 回應 toouse 保護 toohello 應用程式的 web API 後端的呼叫中擷取 hello token。
8. hello 瀏覽器呼叫 hello 應用程式的 web API 後端 hello 授權標頭中的 hello 存取權杖。

#### <a name="code-samples"></a>程式碼範例
單一頁面應用程式 (SPA) 」 案例的 hello 程式碼範例，請參閱。 會確定 toocheck 後經常-我們加入新的範例所有 hello 時間。 [單一頁面應用程式 (SPA)](active-directory-code-samples.md#single-page-application-spa)。

#### <a name="registering"></a>註冊
* 單一租用戶： 如果您要建置應用程式只會為您的組織，它必須註冊您的公司目錄中使用 hello Azure 入口網站。
* 多租用戶： 如果您要建置的應用程式，可供組織外的使用者，必須註冊在公司的目錄中，但也必須在每個組織的目錄將會使用 hello 應用程式中註冊。 toomake 至他們的目錄中可用的應用程式，您可以為您的客戶，讓他們 tooconsent tooyour 應用程式包含註冊程序。 當他們註冊您的應用程式 」 時，它們會顯示一個對話方塊，其中顯示 hello 權限 hello 應用程式需要，然後 hello tooconsent 選項。 視 hello 所需的權限，系統管理員可以在 hello 另一個組織可能會需要 toogive 同意。 當 hello 使用者或系統管理員同意時，hello 應用程式會註冊在他們的目錄。 如需詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。

在註冊之後 hello 應用程式，它必須設定的 toouse OAuth 2.0 隱含授予通訊協定。 根據預設，應用程式都停用此通訊協定。 tooenable hello OAuth2 隱含授予通訊協定，應用程式編輯 hello Azure 入口網站從其應用程式資訊清單，並設定 hello"oauth2AllowImplicitFlow"值 tootrue。 如需詳細指示，請參閱 [啟用單一頁面應用程式的 OAuth 2.0 隱含授權](active-directory-integrating-applications.md)。

#### <a name="token-expiration"></a>權杖到期
當您使用 ADAL.js toomanage 驗證搭配 Azure AD 時，因此您可以從數個功能，以便重新整理過期的權杖，以及取得 hello 應用程式可能會呼叫其他 web API 資源權杖。 當 hello 使用者已成功向 Azure AD 時，hello 使用者 hello 瀏覽器和 Azure AD 之間建立的 cookie 保護的工作階段。 Hello 工作階段存在 hello 使用者與 Azure AD 之間及 not between hello 使用者和 hello hello 伺服器上執行的 web 應用程式的重要 toonote 它。 當權杖到期時，ADAL.js 會使用此工作階段 toosilently 取得另一個權杖。 它會使用隱藏的 iFrame toosend 並收到 hello 要求使用 hello OAuth 隱含授予通訊協定。 ADAL.js 也可以使用相同的機制 toosilently 取得存取權杖，從 Azure AD 的其他 web API 資源的 hello 應用程式會呼叫，只要這些資源支援跨原始資源共用 (CORS)，已登錄在 hello 使用者目錄中，並所有必要的同意 hello 使用者登入期間指定。

### <a name="native-application-tooweb-api"></a>原生應用程式 tooWeb 應用程式開發介面
本節描述代表使用者呼叫 Web API 的原生應用程式。 此案例根據 hello OAuth 2.0 授權碼授與類型為公用的用戶端與 hello 第 4.1 節中所述[OAuth 2.0 規格](http://tools.ietf.org/html/rfc6749)。 hello 原生應用程式使用 hello OAuth 2.0 通訊協定來取得 hello 使用者的存取權杖。 然後，此存取權杖會傳送 hello 要求 toohello web API 中，以授權 hello 使用者，並傳回 hello 所需的資源。

#### <a name="diagram"></a>圖表
![原生應用程式 tooWeb API 圖表](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>原生應用程式 tooAPI 的驗證流程
#### <a name="description-of-protocol-flow"></a>通訊協定流程的描述
如果您使用 hello AD 驗證程式庫，大部分的 hello 如下所述的通訊協定詳細資料會幫您處理，例如 hello 瀏覽器快顯視窗、 權杖快取和重新整理權杖的處理。

1. 使用瀏覽器快顯，hello 原生應用程式可讓 Azure AD 中要求 toohello 授權端點。 Hello Azure 入口網站中，與 hello 應用程式識別碼 URI hello web API 中所示，此要求包含 hello 應用程式識別碼和 hello 重新導向的 hello 原生應用程式的 URI。 如果 hello 使用者尚未登入，則提示的 toosign 中一次
2. Azure AD 會驗證 hello 使用者。 如果它是多租用戶應用程式，且同意需要的 toouse hello 應用程式，hello 使用者將會需要的 tooconsent 如果它們尚未這樣做。 授與同意之後和成功驗證，Azure AD 會發出授權碼回應後 toohello 用戶端應用程式的重新導向 URI。
3. 當 Azure AD 發出授權碼回應回 toohello 重新導向 URI，hello 用戶端應用程式會停止瀏覽器互動和擷取 hello 授權 hello 回應碼。 利用這個授權碼，hello 用戶端應用程式傳送包含 hello 授權碼要求 tooAzure AD 的權杖端點、 詳細資料有關 hello （應用程式識別碼和重新導向 URI） 的用戶端應用程式與 hello 所需的資源 （應用程式識別碼URI hello web 應用程式開發介面)。
4. Azure AD 會驗證 hello 授權碼及 hello 用戶端應用程式和 web API 的相關資訊。 成功驗證後，Azure AD 會傳回兩個權杖：JWT 存取權杖和 JWT 重新整理權杖。 此外，Azure AD 傳回的基本資訊 hello 使用者，例如其顯示名稱和租用戶識別碼。
5. 透過 HTTPS，hello 用戶端應用程式會使用 hello hello 要求 toohello web API hello 授權標頭中傳回 JWT 存取權杖 tooadd hello 含有"Bearer"稱號的 JWT 字串。 hello web 應用程式開發介面，然後驗證 hello JWT 權杖中，而如果驗證成功，傳回 hello 需要資源。
6. Hello 存取權杖過期時，hello 用戶端應用程式會收到錯誤，指出 hello 使用者需要 tooauthenticate 一次。 如果 hello 應用程式具有有效的重新整理權杖，它可以是新的存取權杖，而不提示 hello 使用者 toosign 中的一次使用的 tooacquire。 Hello 的應用程式如果 hello 重新整理權杖到期時，需要 toointeractively 再次驗證 hello 使用者。

> [!NOTE]
> hello 重新整理權杖由 Azure AD 發出可以是使用的 tooaccess 多個資源。 例如，如果您有權限 toocall 兩個 web Api 的用戶端應用程式，hello 重新整理權杖可以用的 tooget 向以及存取語彙基元 toohello 其他 web API。
> 
> 

#### <a name="code-samples"></a>程式碼範例
原生應用程式 tooWeb API 」 案例的 hello 程式碼範例，請參閱。 而且，請經常回來查看--我們隨時都 hello 加入新的範例。 [原生應用程式 tooWeb API](active-directory-code-samples.md#native-application-to-web-api)。

#### <a name="registering"></a>註冊
* 單一租用戶： 兩者 hello 原生應用程式和 hello web API 必須註冊在 hello Azure AD 中相同的目錄。 hello web API 可以設定的 tooexpose 一組權限，也就是使用的 toolimit hello 原生應用程式的存取 tooits 資源。 然後 hello 用戶端應用程式從 hello Azure 入口網站中的 hello 」 權限 tooOther 應用程式 」 的下拉式清單功能表選取想要的 hello 權限。
* 多租用戶： 首先，hello 原生應用程式僅註冊在 hello 開發人員或發行者的目錄。 其次，hello 原生應用程式是設定的 tooindicate hello 權限，它需要 toobe 功能。 這份清單的必要權限會顯示在對話方塊中，當使用者或 hello 目的地目錄中的系統管理員能提供同意 toohello 應用程式，這會讓它成為可用 tootheir 組織時。 某些應用程式需要只使用者層級權限，hello 組織中的任何使用者都可表示同意。 其他應用程式需要系統管理員層級權限，無法表示同意 hello 組織中的使用者。 只有目錄管理員可以授與同意 tooapplications 需要此層級的權限。 當 hello 使用者或系統管理員同意時，只有 hello web API 會註冊在他們的目錄。 如需詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。

#### <a name="token-expiration"></a>權杖到期
當 hello 原生應用程式使用其授權碼 tooget JWT 存取權杖時，它也會收到 JWT 重新整理權杖。 Hello 重新整理權杖時 hello 存取權杖到期時，可能會使用的 toore-驗證 hello 使用者，而不需要它們 toosign 中的一次。 此重新整理權杖則使用的 tooauthenticate hello 的使用者，而這可能導致新的存取權杖，並重新整理權杖。

### <a name="web-application-tooweb-api"></a>Web 應用程式 tooWeb 應用程式開發介面
本節說明需要從 web API 的 tooget 資源的 web 應用程式。 在此案例中，有 hello web 應用程式的兩個識別類型可以使用 tooauthenticate，呼叫 hello web API： 應用程式識別或委派的使用者識別。

*應用程式識別：* OAuth 2.0 用戶端認證授與 hello 應用程式，並存取 hello tooauthenticate 此案例會使用 web 應用程式開發介面。 當使用應用程式識別，hello web API 只能偵測 hello web 應用程式正在呼叫它，hello 與 web 應用程式開發介面沒有收到 hello 使用者的任何資訊。 如果 hello 應用程式收到 hello 使用者的相關資訊，則會將傳送嗨應用程式通訊協定，透過，而且它並非由 Azure AD 簽署。 hello web API 信任 hello web 應用程式驗證 hello 使用者。 基於這個理由，這種模式稱為受信任子系統。

*委派的使用者識別* ：有兩種方式可實現此案例：OpenID Connect 和搭配機密用戶端的 OAuth 2.0 授權碼授與。 hello web 應用程式會取得 hello 使用者，這證明 toohello web API 的 hello 使用者已驗證成功 toohello web 應用程式和 hello web 應用程式已能夠 tooobtain 委派的使用者識別 toocall hello web API 的存取權杖。 此存取權杖會傳送 hello 要求 toohello web API 中，以授權 hello 使用者，並傳回 hello 所需的資源。

#### <a name="diagram"></a>圖表
![Web 應用程式 tooWeb API 圖表](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>通訊協定流程的描述
同時 hello 應用程式識別和委派的使用者識別類型會討論下列 hello 流程。 hello 它們之間的主要差異是 hello 委派使用者識別必須先取得授權碼 hello 使用者才能登入並取得存取 toohello web API。

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>採用 OAuth 2.0 用戶端認證授與的應用程式識別
1. 使用者登入 tooAzure AD hello web 應用程式中 (請參閱 hello[應用程式的網頁瀏覽器 tooWeb](#web-browser-to-web-application)上方)。
2. hello web 應用程式需要 tooacquire 存取權杖，使其可以 toohello web API 進行驗證和擷取 hello 所需的資源。 它會要求 tooAzure AD 的權杖端點，以提供 hello 認證、 應用程式識別碼和 web API 的應用程式識別碼 URI。
3. Azure AD 驗證 hello 應用程式，並傳回是使用的 toocall hello web API 的 JWT 存取權杖。
4. 透過 HTTPS，hello web 應用程式會使用 hello hello 要求 toohello web API hello 授權標頭中傳回 JWT 存取權杖 tooadd hello 含有"Bearer"稱號的 JWT 字串。 hello web 應用程式開發介面，然後驗證 hello JWT 權杖中，而如果驗證成功，傳回 hello 需要資源。

##### <a name="delegated-user-identity-with-openid-connect"></a>採用 OpenID Connect 的委派的使用者識別
1. 使用者登入 tooa web 應用程式使用 Azure AD (請參閱 hello[應用程式的網頁瀏覽器 tooWeb](#web-browser-to-web-application)上一節)。 如果 hello hello web 應用程式的使用者尚未同意 tooallowing hello web 應用程式 toocall hello web API 代替它，hello 使用者將需要 tooconsent。 hello 應用程式會顯示它所需的 hello 權限，而且如果其中任何系統管理員層級權限，hello 目錄中的標準使用者將無法能 tooconsent。 此同意程序僅適用於 toomulti 租用戶應用程式，而非單一租用戶應用程式，如 hello 應用程式將已擁有 hello 必要的權限。 Hello 使用者登入時，hello web 應用程式收到 hello 使用者，以及授權碼的相關資訊的 ID 語彙基元。
2. 使用 Azure AD 所簽發的 hello 授權碼，hello web 應用程式傳送包含 hello 授權碼要求 tooAzure AD 的權杖端點，hello 用戶端應用程式 （應用程式識別碼和重新導向 URI） 和 hello 詳細資料所需的資源 （應用程式識別碼 URI hello web 應用程式開發介面）。
3. Azure AD 會驗證 hello 授權碼及 hello web 應用程式和 web API 的相關資訊。 成功驗證後，Azure AD 會傳回兩個權杖：JWT 存取權杖和 JWT 重新整理權杖。
4. 透過 HTTPS，hello web 應用程式會使用 hello hello 要求 toohello web API hello 授權標頭中傳回 JWT 存取權杖 tooadd hello 含有"Bearer"稱號的 JWT 字串。 hello web 應用程式開發介面，然後驗證 hello JWT 權杖中，而如果驗證成功，傳回 hello 需要資源。

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>採用 OAuth 2.0 授權碼授與的委派的使用者識別
1. 使用者已經登入 tooa web 應用程式，其驗證機制與 Azure AD 無關。
2. hello web 應用程式需要授權程式碼 tooacquire 存取權杖，讓它發出要求，以透過 hello 瀏覽器 tooAzure AD 的授權端點，以提供應用程式識別碼 hello 與 hello web 應用程式之後重新導向 URI 成功驗證。 hello 使用者登入 tooAzure AD。
3. 如果 hello hello web 應用程式的使用者尚未同意 tooallowing hello web 應用程式 toocall hello web API 代替它，hello 使用者將需要 tooconsent。 hello 應用程式會顯示它所需的 hello 權限，而且如果其中任何系統管理員層級權限，hello 目錄中的標準使用者將無法能 tooconsent。 Tooboth 單一和多租用戶應用程式套用此同意。  在 hello 單一租用戶的情況下，為系統管理員可以代表使用者執行系統管理員同意 tooconsent。  這可以使用 hello`Grant Permissions`按鈕在 hello [Azure 入口網站](https://portal.azure.com)。 
4. Hello 使用者同意之後，hello web 應用程式會收到 hello 授權程式碼，它需要 tooacquire 存取權杖。
5. 使用 Azure AD 所簽發的 hello 授權碼，hello web 應用程式傳送包含 hello 授權碼要求 tooAzure AD 的權杖端點，hello 用戶端應用程式 （應用程式識別碼和重新導向 URI） 和 hello 詳細資料所需的資源 （應用程式識別碼 URI hello web 應用程式開發介面）。
6. Azure AD 會驗證 hello 授權碼及 hello web 應用程式和 web API 的相關資訊。 成功驗證後，Azure AD 會傳回兩個權杖：JWT 存取權杖和 JWT 重新整理權杖。
7. 透過 HTTPS，hello web 應用程式會使用 hello hello 要求 toohello web API hello 授權標頭中傳回 JWT 存取權杖 tooadd hello 含有"Bearer"稱號的 JWT 字串。 hello web 應用程式開發介面，然後驗證 hello JWT 權杖中，而如果驗證成功，傳回 hello 需要資源。

#### <a name="code-samples"></a>程式碼範例
Web 應用程式 tooWeb API 」 案例的 hello 程式碼範例，請參閱。 而且，請經常回來查看--我們隨時都 hello 加入新的範例。 Web[應用程式 tooWeb API](active-directory-code-samples.md#web-application-to-web-api)。

#### <a name="registering"></a>註冊
* 單一租用戶： Hello 應用程式識別和委派的使用者識別的案例 hello web 應用程式和 hello web API 必須註冊在 hello Azure AD 中相同的目錄。 hello web API 可以設定的 tooexpose 一組權限，也就是使用的 toolimit hello web 應用程式的存取 tooits 資源。 如果使用委派的使用者識別類型，hello web 應用程式會需要從 hello Azure 入口網站中的 hello 」 權限 tooOther 應用程式 」 的下拉式清單功能表 tooselect hello 所需權限。 如果正在使用 hello 應用程式識別類型，就不需要此步驟。
* 多租用戶： Hello web 應用程式第一次，是它需要 toobe 功能設定的 tooindicate hello 權限。 這份清單的必要權限會顯示在對話方塊中，當使用者或 hello 目的地目錄中的系統管理員能提供同意 toohello 應用程式，這會讓它成為可用 tootheir 組織時。 某些應用程式需要只使用者層級權限，hello 組織中的任何使用者都可表示同意。 其他應用程式需要系統管理員層級權限，無法表示同意 hello 組織中的使用者。 只有目錄管理員可以授與同意 tooapplications 需要此層級的權限。 當 hello 使用者或系統管理員的同意授權，hello web 應用程式和 hello web API 都會註冊在他們的目錄。

#### <a name="token-expiration"></a>權杖到期
當 hello web 應用程式使用其授權碼 tooget JWT 存取權杖時，它也會收到 JWT 重新整理權杖。 Hello 重新整理權杖時 hello 存取權杖到期時，可能會使用的 toore-驗證 hello 使用者，而不需要它們 toosign 中的一次。 此重新整理權杖則使用的 tooauthenticate hello 的使用者，而這可能導致新的存取權杖，並重新整理權杖。

### <a name="daemon-or-server-application-tooweb-api"></a>精靈或伺服器應用程式 tooWeb 應用程式開發介面
本節說明需要從 web API 的 tooget 資源精靈或伺服器應用程式。 有兩種套用 toothis 區段的子案例： 需要 toocall web API，在 OAuth 2.0 用戶端認證授與類型; 內建的協助程式而且需要 toocall 伺服器應用程式 （例如 web API) 的 web 應用程式開發介面，內建在 OAuth 2.0 On-Behalf-Of 草稿規格。

Hello 案例精靈應用程式需要 toocall web API 時，重要 toounderstand 幾件事。 首先，不可能精靈應用程式，需要 hello 應用程式 toohave 本身之身分識別與使用者互動。 批次工作或在 hello 背景中執行的作業系統服務精靈應用程式的範例。 這種類型的應用程式使用其應用程式識別，並提供給其應用程式識別碼、 認證 （密碼或憑證） 和應用程式識別碼 URI tooAzure AD 要求存取權杖。 成功驗證之後，hello 服務精靈會接收來自 Azure AD，則使用的 toocall hello web API 的存取權杖。

Hello 案例伺服器應用程式需要 toocall web API 時，很有幫助 toouse 範例。 假設使用者驗證在原生應用程式，而這個原生應用程式必須 toocall web API。 Azure AD 會發出 JWT 存取權杖 toocall hello web API。 如果 hello web API 需要 toocall 另一個下游 web API，它可以使用 hello 上-代表 」 流程 toodelegate hello 使用者的身分識別和驗證 toohello 第二層 web API。

#### <a name="diagram"></a>圖表
![精靈或伺服器應用程式的應用程式開發介面 tooWeb 圖表](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>通訊協定流程的描述
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>採用 OAuth 2.0 用戶端認證授與的應用程式識別
1. 首先，hello 伺服器應用程式需要 tooauthenticate 與 Azure AD 作為本身沒有任何人為互動，例如互動式登入對話方塊。 它會要求 tooAzure AD 的權杖端點，以提供 hello 認證、 應用程式識別碼和應用程式識別碼 URI。
2. Azure AD 驗證 hello 應用程式，並傳回是使用的 toocall hello web API 的 JWT 存取權杖。
3. 透過 HTTPS，hello web 應用程式會使用 hello hello 要求 toohello web API hello 授權標頭中傳回 JWT 存取權杖 tooadd hello 含有"Bearer"稱號的 JWT 字串。 hello web 應用程式開發介面，然後驗證 hello JWT 權杖中，而如果驗證成功，傳回 hello 需要資源。

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>採用 OAuth 2.0 On-Behalf-Of 草稿規格的委派的使用者識別
hello 流程如下所示假設使用者驗證 （例如原生應用程式），另一個應用程式上，且其使用者識別已使用的 tooacquire 存取語彙基元 toohello 第一層 web API。

1. hello 原生應用程式會傳送 hello 存取語彙基元 toohello 第一層 web API。
2. hello 第一層 web 應用程式開發介面傳送要求 tooAzure AD 的權杖端點，以提供其應用程式識別碼和認證，以及 hello 使用者的存取權杖。 此外，所傳送嗨要求包含參數，指出 hello on_behalf_of web API 正在要求新權杖代表 hello 原始使用者 toocall 下游 web API。
3. Azure AD 會驗證該 hello 第一層 web API 有權限 tooaccess hello 第二層 web API，並驗證 hello 要求傳回 JWT 存取權杖和 JWT 重新整理語彙基元 toohello 第一層 web API。
4. 透過 HTTPS，hello 第一層 web API 然後呼叫 hello 藉由附加 hello 要求中的 hello 授權標頭中的 hello 語彙基元字串的第二層 web API。 hello 第一層 web API 可以繼續 toocall hello 第二層 web API，只要 hello 存取權杖和重新整理語彙基元有效。

#### <a name="code-samples"></a>程式碼範例
請參閱 hello 精靈或伺服器應用程式的應用程式開發介面 tooWeb 案例的程式碼範例。 而且，請經常回來查看--我們隨時都 hello 加入新的範例。 [伺服器或精靈應用程式 tooWeb 應用程式開發介面](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>註冊
* 單一租用戶： Hello 應用程式識別和委派的使用者識別的案例 hello 精靈或伺服器應用程式必須註冊在 hello Azure AD 中相同的目錄。 hello web API 可以設定的 tooexpose 一組權限，也就是使用的 toolimit hello 精靈或伺服器的存取 tooits 資源。 如果使用委派的使用者識別類型，hello 伺服器應用程式會需要從 hello Azure 入口網站中的 hello 」 權限 tooOther 應用程式 」 的下拉式清單功能表 tooselect hello 所需權限。 如果正在使用 hello 應用程式識別類型，就不需要此步驟。
* 多租用戶： Hello 精靈或伺服器應用程式第一次，是它需要 toobe 功能設定的 tooindicate hello 權限。 這份清單的必要權限會顯示在對話方塊中，當使用者或 hello 目的地目錄中的系統管理員能提供同意 toohello 應用程式，這會讓它成為可用 tootheir 組織時。 某些應用程式需要只使用者層級權限，hello 組織中的任何使用者都可表示同意。 其他應用程式需要系統管理員層級權限，無法表示同意 hello 組織中的使用者。 只有目錄管理員可以授與同意 tooapplications 需要此層級的權限。 當 hello 使用者或系統管理員同意時，這兩個 hello web Api 會註冊在他們的目錄。

#### <a name="token-expiration"></a>權杖到期
當 hello 第一個應用程式使用其授權碼 tooget JWT 存取權杖時，它也會收到 JWT 重新整理權杖。 Hello 重新整理權杖時 hello 存取權杖到期時，可能會使用的 toore-hello 使用者不會提示輸入認證進行驗證。 此重新整理權杖則使用的 tooauthenticate hello 的使用者，而這可能導致新的存取權杖，並重新整理權杖。

## <a name="see-also"></a>另請參閱
[Azure Active Directory 開發人員指南](active-directory-developers-guide.md)

[Azure Active Directory 程式碼範例](active-directory-code-samples.md)

[Azure AD 中簽署金鑰變換的相關重要資訊](active-directory-signing-key-rollover.md)

[Azure AD 中的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)

