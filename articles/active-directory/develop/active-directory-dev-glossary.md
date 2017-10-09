---
title: "aaaAzure Active Directory 開發人員詞彙 |Microsoft 文件"
description: "常用 Azure Active Directory 開發人員概念與功能的詞彙清單。"
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Azure Active Directory 開發人員詞彙
這份文件包含一些 hello 核心 Azure Active Directory (AD) 開發人員概念，也就是很有幫助，深入了解 Azure AD 的應用程式開發時定義。

## <a name="access-token"></a>存取權杖
一種[安全性權杖](#security-token)發給[授權伺服器](#authorization-server)，並用[用戶端應用程式](#client-application)中順序 tooaccess[受保護的資源伺服器](#resource-server). 通常在 hello 形式的[JSON Web Token (JWT)][JWT]，hello 語彙基元意 hello 授權授與 toohello 用戶端 hello[資源擁有者](#resource-owner)，針對要求的層級存取權。 hello 權杖會包含所有適用[宣告](#claim)關於 hello 主旨，啟用 hello 用戶端應用程式 toouse 它做為一種認證時存取指定的資源。 這也會刪除 hello 需要 hello 資源擁有者 tooexpose 認證 toohello 用戶端。

存取語彙基元有時是參照的 tooas 「 使用者 + 應用程式 」 或者 「 應用程式-僅限 」，根據 hello 認證所表示。 例如，當用戶端應用程式使用：

* [「 授權程式碼 」 授權授與](#authorization-grant)、 hello 結束使用者第一次定義 hello 資源擁有者驗證之後，用戶端 tooaccess 委派授權 toohello hello 資源。 取得 hello 存取權杖時，則 hello 用戶端會驗證之後。 hello 語彙基元有時可能參考的 toomore 為 「 使用者 + 應用程式 」 的語彙基元，特別是當它表示這兩個 hello 使用者獲授權 hello 用戶端應用程式，以及 hello 應用程式。
* [「 用戶端認證 」 授權授與](#authorization-grant)hello 用戶端提供 hello 唯一驗證，因此 hello 語彙基元有時可以運作 hello 資源擁有者的驗證/授權，而可參考的 tooas 「 應用程式-僅限 」 的語彙基元。

如需詳細資訊，請參閱 [Azure AD 權杖參考][AAD-Tokens-Claims]。

## <a name="application-manifest"></a>應用程式資訊清單
Hello 所提供的功能[Azure 入口網站][AZURE-portal]，這會產生 hello 應用程式的身分識別設定，做為其相關聯的更新機制的 JSON 表示法[應用程式][ AAD-Graph-App-Entity]和[ServicePrincipal] [ AAD-Graph-Sp-Entity]實體。 請參閱[了解 hello Azure Active Directory 應用程式資訊清單][ AAD-App-Manifest]如需詳細資訊。

## <a name="application-object"></a>應用程式物件
當您註冊/更新的應用程式在 hello [Azure 入口網站][AZURE-portal]，hello 入口網站建立/更新的應用程式物件和對應[服務主體物件](#service-principal-object)該租用戶。 hello 應用程式物件*定義*hello 應用程式的身分識別設定全域 （它已經在此對話方塊存取的所有租用戶） 之間，提供的範本，其對應的服務主體的物件會從其中*衍生*以供在本機執行階段 （在特定的租用戶）。

如需詳細資訊，請參閱[應用程式物件和服務主體物件][AAD-App-SP-Objects]。

## <a name="application-registration"></a>應用程式註冊
在排序與應用程式 toointegrate 和委派身分識別和存取管理功能 tooAzure AD tooallow、 必須向 Azure AD[租用戶](#tenant)。 當您使用 Azure AD 註冊您的應用程式時，您提供身分識別設定您的應用程式，讓它與 Azure AD toointegrate，並使用下列功能：

* 使用 Azure AD 身分識別管理和 [OpenID Connect][OpenIDConnect] 通訊協定實作，健全地管理單一登入
* 太代理存取[受保護資源](#resource-server)由[用戶端應用程式](#client-application)，透過 Azure AD 的 OAuth 2.0[授權伺服器](#authorization-server)實作
* [同意架構](#consent)管理用戶端存取 tooprotected，根據資源的資源擁有者授權。

如需詳細資訊，請參閱[整合應用程式與 Azure Active Directory][AAD-Integrating-Apps]。

## <a name="authentication"></a>驗證
hello 具挑戰性的合作對象合法的認證，提供建立用於身分識別和存取控制的安全性主體的 toobe hello 基礎等操作。 期間[OAuth2 授權授與](#authorization-grant)hello 角色中的其中一個 hello 合作對象驗證過的例如[資源擁有者](#resource-owner)或[用戶端應用程式](#client-application)，取決於hello 授與使用。

## <a name="authorization"></a>授權
授與已驗證的安全性主體的權限 toodo 東西的 hello 動作。 Hello Azure AD 的程式設計模型中有兩個主要使用案例：

* 期間[OAuth2 授權授與](#authorization-grant)流程： 當 hello[資源擁有者](#resource-owner)授與授權 toohello[用戶端應用程式](#client-application)，讓 tooaccess hello 的 hello 用戶端資源擁有者的資源。
* Hello 用戶端的資源存取期間： hello 由實作[資源伺服器](#resource-server)，使用 hello[宣告](#claim)值出現在 hello[存取權杖](#access-token)toomake 存取控制根據他們的決策。

## <a name="authorization-code"></a>授權碼
一個簡短存在"token"提供 tooa[用戶端應用程式](#client-application)由 hello[授權端點](#authorization-endpoint)，hello 「 授權程式碼 」 流程的一部分，其中一個 hello 四個 OAuth2[授權授與](#authorization-grant). hello 程式碼會傳回 toohello 用戶端應用程式中的回應 tooauthentication[資源擁有者](#resource-owner)，指出 hello 資源擁有者已委派授權 tooaccess hello 要求的資源。 Hello 流程的一部分，hello 程式碼稍後贖回[存取權杖](#access-token)。

## <a name="authorization-endpoint"></a>授權端點
其中一個 hello 端點實作 hello[授權伺服器](#authorization-server)，toointeract 搭配 hello[資源擁有者](#resource-owner)中順序 tooprovide[授權授與](#authorization-grant)期間OAuth2 授權授與流程。 根據 hello 授權授與流程，hello 實際授與提供可能會不同，包括[授權碼](#authorization-code)或[安全性權杖](#security-token)。

請參閱 hello OAuth2 規格[授權授與類型][ OAuth2-AuthZ-Grant-Types]和[授權端點][ OAuth2-AuthZ-Endpoint]區段及 hello [OpenIDConnect 規格][ OpenIDConnect-AuthZ-Endpoint]如需詳細資訊。

## <a name="authorization-grant"></a>授權授與
代表 hello 認證[資源擁有者](#resource-owner)[授權](#authorization)tooaccess 及其受保護的資源，授與 tooa[用戶端應用程式](#client-application)。 用戶端應用程式可以使用其中一個 hello[四個授與 hello OAuth2 授權架構所定義的類型][ OAuth2-AuthZ-Grant-Types] tooobtain 授與，根據用戶端型別需求: 「 授權碼授與，""用戶端認證授與 」、 「 隱含授與 「 和 」 資源擁有者密碼認證授與 「。 hello 認證傳回 toohello 用戶端是[存取權杖](#access-token)，或[授權碼](#authorization-code)（交換稍後存取權杖），視使用授權授與 hello 類型而定。

## <a name="authorization-server"></a>受保護的資源
所定義的 hello [OAuth2 授權架構][OAuth2-Role-Def]，hello 伺服器負責簽發存取語彙基元 toohello[用戶端](#client-application)成功驗證之後hello[資源擁有者](#resource-owner)並取得其授權。 A[用戶端應用程式](#client-application)互動 hello 授權伺服器，在執行階段透過其[授權](#authorization-endpoint)和[語彙基元](#token-endpoint)根據 hello OAuth2 定義的端點[授權授與](#authorization-grant)。

在 Azure AD 應用程式整合的 hello 情況下，Azure AD 實作 hello 授權伺服器角色的 Azure AD 應用程式和 Microsoft 服務 Api，例如[Microsoft Graph Api][Microsoft-Graph]。

## <a name="claim"></a>宣告
A[安全性權杖](#security-token)包含約一個實體提供判斷提示的宣告 (例如[用戶端應用程式](#client-application)或[資源擁有者](#resource-owner)) tooanother 實體 （例如 hello[資源伺服器](#resource-server))。 宣告是轉送事項 hello 權杖主體的名稱/值組 (例如，hello 安全性主體通過驗證 hello[授權伺服器](#authorization-server))。 指定的權杖中的 hello 宣告是權杖的取決於數個變數，包括 hello 的型別、 hello 型別使用的認證 tooauthenticate hello 主旨、 hello 應用程式組態、 等等。

如需詳細資訊，請參閱 [Azure AD 權杖參考][AAD-Tokens-Claims]。

## <a name="client-application"></a>用戶端應用程式
所定義的 hello [OAuth2 授權架構][OAuth2-Role-Def]，應用程式，讓受保護資源要求代表 hello[資源擁有者](#resource-owner)。 hello 詞彙 「 用戶端 」 不代表任何特定的硬體實作特性，（比方說，不論 hello 應用程式執行的桌面或其他裝置的伺服器上）。  

用戶端應用程式要求[授權](#authorization)從中資源擁有者 tooparticipate [OAuth2 授權授與](#authorization-grant)流程，並可能 hello 資源擁有者的身分存取 Api/資料。 hello OAuth2 授權架構[定義兩種類型的用戶端][OAuth2-Client-Types]、 「 公司機密 」 和 「 公用 」，根據其認證的用戶端 hello 能力 toomaintain hello 機密性。 應用程式可實作在 Web 伺服器上執行的 [Web 用戶端 (機密)](#web-client)、安裝在裝置上的[原生用戶端 (公用)](#native-client)，或在裝置的瀏覽器中執行的[使用者代理程式型用戶端 (公用)](#user-agent-based-client)。

## <a name="consent"></a>同意
hello 的程序[資源擁有者](#resource-owner)授與授權 tooa[用戶端應用程式](#client-application)，tooaccess 受保護的資源在特定[權限](#permissions)，代表 hello資源擁有者。 根據 hello hello 用戶端要求的權限，系統管理員或使用者必須同意 tooallow 存取 tootheir 組織/個人資料分別。 請注意，在[多租用戶](#multi-tenant-application)情節、 hello 應用程式的[服務主體](#service-principal-object)也會記錄在 hello 租用戶的 hello 同意的使用者。

## <a name="id-token"></a>識別碼權杖
[OpenID Connect] [ OpenIDConnect-ID-Token] [安全性權杖](#security-token)提供[授權伺服器的](#authorization-server)[授權端點](#authorization-endpoint)，其中包含[宣告](#claim)相關 toohello 驗證使用者的[資源擁有者](#resource-owner)。 和存取權杖一樣，識別碼權杖也會以數位簽署的 [JSON Web 權杖 (JWT)][JWT] 來表示。 不同於存取權杖，ID 權杖的宣告不會使用針對用途相關的 tooresource 存取和特別存取控制。

如需詳細資訊，請參閱 [Azure AD 權杖參考][AAD-Tokens-Claims]。

## <a name="multi-tenant-application"></a>多租用戶應用程式
可讓登入的應用程式的類別和[同意](#consent)由使用者在任何 Azure AD 中佈建[租用戶](#tenant)，包括租用戶以外 hello hello 用戶端登錄的其中一個。 [原生用戶端](#native-client)應用程式會根據預設，多租用戶而[web 用戶端](#web-client)和[web API資源/](#resource-server)應用程式有 hello 能力 tooselect 單一或多租用戶之間。 相反地，web 應用程式註冊為單一租用戶，則只允許從佈建的 hello 相同 hello 其中一個為租用戶的使用者帳戶的登入係 hello 應用程式。

請參閱[如何在任何 Azure AD 使用者使用 toosign hello 多租用戶應用程式模式][ AAD-Multi-Tenant-Overview]如需詳細資訊。

## <a name="native-client"></a>原生用戶端
裝置上原生安裝的 [用戶端應用程式](#client-application) 類型。 因為裝置上執行的所有程式碼時，它會被視為 「 公用 」 的用戶端，因為 tooits 無法 toostore 認證私下/保密。 如需詳細資訊，請參閱 [OAuth2 用戶端類型和設定檔][OAuth2-Client-Types]。

## <a name="permissions"></a>權限
A[用戶端應用程式](#client-application)提升存取 tooa[資源伺服器](#resource-server)藉由宣告權限要求。 其可用類型有兩種︰

* 「 委派 」 權限，指定[領域為主](#scopes)存取使用委派授權從登入的 hello[資源擁有者](#resource-owner)，會在執行階段做為呈現 toohello 資源["scp「 宣告](#claim)在用戶端 hello[存取權杖](#access-token)。
* 「 應用程式 」 的權限，可指定[以角色為基礎](#roles)存取使用 hello 用戶端應用程式的認證識別碼，會在執行階段做為呈現 toohello 資源[「 角色 」 宣告](#claim)在 hello用戶端的存取權杖。

也在 hello 介面[同意](#consent)程序中，提供 hello 系統管理員或資源擁有者 hello 機會 toogrant/拒絕 hello 用戶端存取 tooresources 其租用戶中。

Hello"應用程式] 上設定的權限要求 [設定] 索引標籤的 hello / [Azure 入口網站][AZURE-portal]、 在 [必要的權限]、 選取 hello 預期 「 委派的權限 」 和 「應用程式權限 > （後者 hello 需要 hello 全域管理員角色的成員資格）。 因為[公用的用戶端](#client-application)無法安全地維護的認證，它只能要求委派的權限，雖然[機密用戶端](#client-application)具有 hello 能力 toorequest 委派和應用程式權限。 用戶端 hello[應用程式物件](#application-object)宣告中的權限的存放區 hello 其[requiredResourceAccess 屬性][AAD-Graph-App-Entity]。

## <a name="resource-owner"></a>資源擁有者
所定義的 hello [OAuth2 授權架構][OAuth2-Role-Def]，能夠授與存取 tooa 實體受保護資源。 個人 hello 資源擁有者時，會參照的 tooas 終端使用者。 例如，當[用戶端應用程式](#client-application)想 tooaccess hello 透過使用者的信箱[Microsoft Graph API][Microsoft-Graph]，它需要的 hello 資源擁有者的權限。hello 信箱。

## <a name="resource-server"></a>資源伺服器
所定義的 hello [OAuth2 授權架構][OAuth2-Role-Def]，主機受保護的資源，能夠接受並回應 tooprotected 資源的伺服器，要求[用戶端應用程式](#client-application)該存在[存取權杖](#access-token)。 它也稱為「受保護的資源伺服器」或「資源應用程式」。

資源伺服器公開 Api，並強制執行存取 tooits 受保護的資源，透過[範圍](#scopes)和[角色](#roles)，使用 hello OAuth 2.0 授權架構。 範例包括 hello Azure AD Graph API 可提供存取 tooAzure AD 租用戶資料和 hello Office 365 Api 來提供存取 toodata，例如郵件和行事曆。 這些都是也可透過 hello 存取[Microsoft Graph API][Microsoft-Graph]。  

就像用戶端應用程式，透過建立資源應用程式的身分識別組態[註冊](#application-registration)在 Azure AD 租用戶提供 hello 應用程式和服務主體物件。 某些 Microsoft 提供的 Api，例如 hello Azure AD Graph API 預先註冊供所有租用戶中期間佈建的服務主體。

## <a name="roles"></a>角色
像[範圍](#scopes)，角色會提供方法讓[資源伺服器](#resource-server)toogovern 存取 tooits 受保護的資源。 有兩種類型: 「 使用者 」 角色實作以角色為基礎的存取控制，針對需要存取 toohello 資源，同時實作 「 應用程式 」 角色的使用者/群組 hello 相同[用戶端應用程式](#client-application)需要的存取。

角色是資源定義的字串 (例如 「 經費支出核准者 」，「 唯讀 」、 「 Directory.ReadWrite.All")、 在 hello managed [Azure 入口網站][ AZURE-portal]透過 hello 資源[應用程式資訊清單](#application-manifest)，並儲存在 hello 資源[appRoles 屬性][AAD-Graph-Sp-Entity]。 hello Azure 入口網站太也使用的 tooassign 使用者 「 使用者 」 角色，並設定用戶端[應用程式權限](#permissions)tooaccess 「 應用程式 」 角色。

Azure AD Graph API 所公開的 hello 應用程式角色的詳細討論，請參閱[Graph API 權限範圍][AAD-Graph-Perm-Scopes]。 如需逐步實作範例，請參閱[雲端應用程式中使用 Azure AD 的角色型存取控制][Duyshant-Role-Blog]。

## <a name="scopes"></a>範圍
像[角色](#roles)，範圍為提供的方式[資源伺服器](#resource-server)toogovern 存取 tooits 受保護的資源。 領域都是使用的 tooimplement[領域為主][ OAuth2-Access-Token-Scopes]的存取控制，[用戶端應用程式](#client-application)，具有委派的存取 toohello 資源由其擁有者。

範圍是資源定義的字串 （例如"Mail.Read"、"Directory.ReadWrite.All"），在 hello 管理[Azure 入口網站][ AZURE-portal]透過 hello 資源[應用程式資訊清單](#application-manifest)，並儲存在 hello 資源[oauth2Permissions 屬性][AAD-Graph-Sp-Entity]。 hello Azure 入口網站也是使用的 tooconfigure 用戶端應用程式[委派權限](#permissions)tooaccess 範圍。

最佳的作法命名慣例，是 toouse"resource.operation.constraint 」 格式。 Azure AD Graph API 所公開的 hello 範圍的詳細討論，請參閱[Graph API 權限範圍][AAD-Graph-Perm-Scopes]。 如需 Office 365 服務所公開的範圍，請參閱 [Office 365 API 權限參考][O365-Perm-Ref]。

## <a name="security-token"></a>安全性權杖
包含 OAuth2 權杖或 SAML 2.0 判斷提示等宣告的已簽署文件。 對於 OAuth2 [授權授與](#authorization-grant)而言，[存取權杖](#access-token) (OAuth2) 和[識別碼權杖](http://openid.net/specs/openid-connect-core-1_0.html#IDToken)皆為安全性權杖類型，而且這兩種類型都會實作為 [JSON Web 權杖 (JWT)][JWT]。

## <a name="service-principal-object"></a>服務主體物件
當您註冊/更新的應用程式在 hello [Azure 入口網站][AZURE-portal]，hello 入口網站建立/更新同時[應用程式物件](#application-object)和對應的服務主體該租用戶的物件。 hello 應用程式物件*定義*hello 全域 （跨越所有租用戶相關聯的 hello 應用程式具有已獲授與存取），應用程式的身分識別組態是從中 hello 範本和其相對應的服務主體的物件是*衍生*以供在本機執行階段 （在特定的租用戶）。

如需詳細資訊，請參閱[應用程式物件和服務主體物件][AAD-App-SP-Objects]。

## <a name="sign-in"></a>登入
hello 的程序[用戶端應用程式](#client-application)起始使用者驗證和擷取相關的狀態，用於取得的 hello 用途[安全性權杖](#security-token)及範圍設定 hello 應用程式工作階段 toothat狀態。 狀態中可包含使用者設定檔資訊之類的構件，以及衍生自權杖宣告的資訊。

hello 登入應用程式的功能是常用的 tooimplement 單一登入 (SSO)。 它可能還加上 「 註冊 」 的函式，為 hello 終端使用者 toogain 存取 tooan 應用程式 （在第一個登入） 的進入點。 hello 註冊函式是使用的 toogather 保存其他的狀態 toohello 特定使用者，且可能需要[使用者同意](#consent)。

## <a name="sign-out"></a>登出
hello 程序的未驗證使用者，卸離 hello hello 與相關聯的使用者狀態[用戶端應用程式](#client-application)工作階段期間[登入](#sign-in)

## <a name="tenant"></a>tenant
Azure AD 目錄的執行個體是參照的 tooas Azure AD 租用戶。 它可提供各種功能，包括︰

* 整合式應用程式的登錄服務
* 驗證使用者帳戶和已註冊的應用程式
* REST 端點所需 toosupport 各種通訊協定包括 OAuth2 和 SAML，包括 hello[授權端點](#authorization-endpoint)，[權杖端點](#token-endpoint)hello 「 通用 」 所使用的端點和[多租用戶應用程式](#multi-tenant-application)。

租用戶也是 Azure AD 與相關聯或 Office 365 訂用帳戶在佈建的 hello 訂用帳戶，提供 hello 訂用帳戶的身分識別與存取管理功能。 請參閱[tooget Azure Active Directory 的租用戶][ AAD-How-To-Tenant] hello 的詳細資訊的各種方式可讓您存取 tooa 租用戶。 請參閱[如何 Azure 訂用帳戶相關聯 Azure Active Directory] [ AAD-How-Subscriptions-Assoc]如 hello 訂用帳戶與 Azure AD 租用戶之間的關聯性的詳細資訊。

## <a name="token-endpoint"></a>權杖端點
其中一個 hello 端點實作 hello[授權伺服器](#authorization-server)toosupport OAuth2[授權授與](#authorization-grant)。 根據 hello 授與，它可以是使用的 tooacquire[存取權杖](#access-token)（及相關的 「 重新整理 」 的權杖） tooa[用戶端](#client-application)，或[ID 語彙基元](#ID-token)hello 搭配使用時[OpenID Connect] [ OpenIDConnect]通訊協定。

## <a name="user-agent-based-client"></a>使用者代理程式型用戶端
一種 [用戶端應用程式](#client-application) ，可從 Web 伺服器下載程式碼並在使用者代理程式 (例如，網頁瀏覽器) 中執行，例如單一頁面應用程式 (SPA)。 因為裝置上執行的所有程式碼時，它會被視為 「 公用 」 的用戶端，因為 tooits 無法 toostore 認證私下/保密。 如需詳細資訊，請參閱 [OAuth2 用戶端類型和設定檔][OAuth2-Client-Types]。

## <a name="user-principal"></a>使用者主體
Toohello 相似的服務主體物件是安全性的使用的 toorepresent 應用程式執行個體，使用者主體的物件是安全性的另一種類型主體，這表示使用者。 hello Azure AD Graph[使用者實體][ AAD-Graph-User-Entity]定義使用者物件，包括使用者相關的屬性，例如名字和姓氏、 使用者主體名稱、 目錄角色成員資格等 hello 結構描述。這會提供 hello 使用者身分識別設定的 Azure AD tooestablish 使用者在執行階段原則。 hello 使用者主體是使用的 toorepresent 已驗證使用者的單一登入，錄製[同意](#consent)委派，讓存取控制決定等等。

## <a name="web-client"></a>Web 用戶端
一種[用戶端應用程式](#client-application)執行所有程式碼上 web 伺服器，並能 toofunction 做為 「 公司機密 」 的用戶端安全地將它的認證儲存在 hello 伺服器上。 如需詳細資訊，請參閱 [OAuth2 用戶端類型和設定檔][OAuth2-Client-Types]。

## <a name="next-steps"></a>後續步驟
hello [Azure AD 開發人員手冊 》] [ AAD-Dev-Guide]是 hello 入口 toouse 所有 Azure AD 開發的相關主題，包括概觀[應用程式整合][AAD-How-To-Integrate]與 hello 基本概念的[Azure AD 驗證和支援的驗證案例][AAD-Auth-Scenarios]。

請使用下列註解區段 tooprovide 回應 hello 和幫助我們改善並圖形我們的內容，包括要求新的定義，或更新現有的 ！

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
