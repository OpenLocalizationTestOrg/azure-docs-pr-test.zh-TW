---
title: "Azure Active Directory 條件式存取的指引 aaaDeveloper |Microsoft 文件"
description: "Azure Active Directory 條件式存取的開發人員指引和案例"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Azure Active Directory 條件式存取的開發人員指引

Azure Active Directory (AD) 提供數種方式 toosecure 您的應用程式，並保護服務。  這些獨特功能其中之一就是條件式存取。  條件式存取可讓開發人員和企業客戶 tooprotect 服務的方式包括：

* Multi-Factor Authentication
* 允許只 Intune 註冊裝置 tooaccess 特定服務
* 限制使用者位置及 IP 範圍

多個 hello 完整功能條件式存取的詳細資訊，請參閱[hello Azure 傳統入口網站中的條件式存取](../active-directory-conditional-access.md)。 

在本文中，我們會著重在哪些條件式存取權就表示 toodevelopers 建置應用程式的 Azure AD。  它假設對於[單一](active-directory-integrating-applications.md)和[多租用戶](active-directory-devhowto-multi-tenant-overview.md)應用程式以及[常見驗證模式](active-directory-authentication-scenarios.md)的認知。

我們將探討 hello 影響存取您沒有在控制項的資源，可能會有套用條件式存取原則。  此外，我們探討 hello 含意 hello 代表的資料流程中的條件式存取的 web 應用程式，存取 hello Microsoft Graph 和呼叫 Api。

## <a name="how-does-conditional-access-impact-an-app"></a>條件式存取如何影響應用程式？

### <a name="app-topologies-impacted"></a>受影響的應用程式拓樸

在最常見的情況下，條件式存取不會變更應用程式的行為，或需要 hello 開發人員從任何變更。  只有在某些情況下當應用程式間接或無訊息方式要求的語彙基元服務中，應用程式會要求程式碼會變更 toohandle 條件式存取 「 挑戰"。  這有如執行互動式登入要求一樣簡單。 

具體來說，hello 下列案例需要程式碼 toohandle 條件式存取 「 挑戰": 

* 存取 hello Microsoft Graph 應用程式
* 應用程式執行 hello 代表的流程
* 存取多個服務/資源的應用程式
* 使用 ADAL.js 的單一頁面應用程式

條件式存取原則可以套用的 toohello 應用程式，但也可以套用的 tooa web API 應用程式存取。 toolearn 深入了解 tooconfigure 條件式存取原則，請參閱[開始使用 Azure Active Directory 條件式存取](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules)。

根據 hello 的案例，企業客戶可以套用，並隨時移除條件式存取原則。  為了讓您的應用程式 toocontinue 正常運作時套用新原則時，您需要 tooimplement hello"挑戰 」 處理。 下列範例中的 hello 說明挑戰處理。 

### <a name="conditional-access-examples"></a>條件式存取範例

某些案例需要程式碼變更 toohandle 條件式存取，而其他人可正常是。  以下是幾個使用條件式存取，提供一些深入 hello 差異 toodo multi-factor authentication 的案例。

* 您要建置單一租用戶 iOS 應用程式，並套用條件式存取原則。  hello 應用程式登入使用者，並不會要求存取 tooan API。  當 hello 使用者登入時，會自動叫用 hello 原則，以及 hello 使用者需要 tooperform multi-factor authentication (MFA)。 
* 您要建置使用 hello Microsoft Graph tooaccess 交換，在其他服務之間的多租用戶 web 應用程式。  採用此應用程式的企業客戶要設定 SharePoint Online 上的原則。  當 hello web 應用程式要求語彙基元 MS 圖形時，要套用的原則上的任何 Microsoft 服務 （特別是服務可以透過 graph 存取）。  系統會提示這個使用者進行 MFA。 Hello 的情況下，在 hello 使用者登入有效的語彙基元中，宣告"挑戰"會傳回 toohello web 應用程式。  
* 您要建置使用中介層服務 tooaccess hello Microsoft Graph 的原生應用程式。  企業客戶在 hello 公司中使用此應用程式適用於原則 tooExchange 線上。  當使用者登入時，hello 原生應用程式要求存取 toohello 中介層，並將傳送嗨 token。  hello 中介層執行上-代表 」 流程 toorequest 存取 toohello MS 圖形。  此時，宣告"挑戰"呈現 toohello 中介層。 hello 中介層會傳送 hello 挑戰後 toohello 原生應用程式，這需要 toocomply 與 hello 條件式存取原則。

### <a name="complying-with-a-conditional-access-policy"></a>遵守條件式存取原則

對於數個不同的應用程式的拓撲，條件式存取原則會評估建立 hello 工作階段。  與條件式存取原則的應用程式和服務的 hello 資料粒度上，會叫用所在的 hello 點取決於 hello 案例中，您正嘗試 tooaccomplish。

當您的應用程式嘗試 tooaccess 具有條件式存取原則的服務時，它可能會遇到的條件式存取的挑戰。  這項挑戰，會編碼在 hello`claims`傳入從 Azure AD 的回應或 hello Microsoft Graph 參數。  以下是這項挑戰參數的範例： 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

開發人員可以使用這項挑戰，並將其附加到新的要求 tooAzure AD。  傳遞此狀態會提示 hello 使用者 tooperform 任何動作的必要 toocomply 與 hello 條件式存取原則。 在下列案例的 hello，說明 hello 錯誤和如何 tooextract hello 參數特性。 

## <a name="scenarios"></a>案例

### <a name="prerequisites"></a>必要條件

Azure AD 條件式存取是 [Azure AD Premium](../active-directory-whatis.md#choose-an-edition) 中包含的一項功能。  您可以進一步了解授權需求在 hello[未經授權的使用方式報表](../active-directory-conditional-access-unlicensed-usage-report.md)。  開發人員可以加入 hello [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx)，包括免費訂用帳戶 toohello Enterprise Mobility Suite 包含 Azure AD Premium。

### <a name="considerations-for-specific-scenarios"></a>特定情節的考量

hello 下列資訊僅適用於這些條件式存取案例：

* 存取 hello Microsoft Graph 應用程式
* 應用程式執行 hello 代表的流程
* 存取多個服務/資源的應用程式
* 使用 ADAL.js 的單一頁面應用程式

在下列各節的 hello，我們將會成常見的案例是更複雜。  hello 核心作業系統的原則是條件式存取原則在時間會評估 hello 要求 hello 語彙基元 hello 服務已套用，除非它正由 hello Microsoft Graph 存取的條件式存取原則。

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>存取 hello Microsoft Graph 的案例： 應用程式

在此案例中，我們逐步 hello 案例 web 應用程式要求存取 toohello Microsoft Graph 時。 hello 條件式存取原則在此情況下無法 tooSharePoint、 Exchange 或指派做為工作負載，透過 hello Microsoft Graph 存取的一些其他服務。  在此範例中，假設 Sharepoint Online 上具有條件式存取原則。

![應用程式存取 hello Microsoft Graph 流程圖](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

hello 應用程式第一次要求授權 toohello 需要存取沒有條件式存取的下游工作負載的 Microsoft 圖形。  hello 要求成功，而不叫用任何原則和 hello 應用程式接收 Microsoft Graph 的權杖。  此時，hello 應用程式可能使用 hello 存取權杖承載要求中的 hello 端點要求。 現在，hello 應用程式需要 tooaccess Sharepoint Online 的 Microsoft Graph 端點，例如：`https://graph.microsoft.com/v1.0/me/mySite`

hello 應用程式已有有效的語彙基元 hello Microsoft Graph，讓它可以執行 hello 新要求，而不發出新的權杖。 此要求會失敗並從 hello 形式 HTTP 403 禁止使用的 Microsoft Graph 發出宣告挑戰```WWW-Authenticate```挑戰。
Hello 回應的範例如下： 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

hello 宣告挑戰位於 hello```WWW-Authenticate```標頭，它可以是 hello 下一個要求的已剖析的 tooextract hello 宣告參數。  一旦附加的 toohello 新要求，Azure AD 登入 hello 使用者和 hello 應用程式現在已符合 hello 條件式存取原則時，就會知道 tooevaluate hello 條件式存取原則。  重複 hello 要求 toohello Sharepoint Online 端點就會成功。

程式碼範例示範如何 toohandle hello 宣告挑戰，請參閱 toohello [.NET 桌面程式碼範例](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop)ADAL.NET 或 hello[代表的程式碼範例](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca)ADAL.net。

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>案例： 應用程式執行 hello 代表的流程

在此案例中，我們逐步解說中的原生應用程式呼叫 web 服務 API 的 hello 案例。  接著，此服務會執行[hello"代表的 「 資料流程](active-directory-authentication-scenarios.md#application-types-and-scenarios)toocall 下游服務。  在此案例中，我們已經套用我們條件式存取原則 toohello 下游服務 (Web API 2)，會使用原生應用程式，而不是伺服器/精靈應用程式。 

![應用程式執行 hello 代表的流程圖](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

hello 語彙基元的初始要求 Web API 1 不會提示 hello 的多重要素驗證的使用者，因為 Web API 1 可能不會永遠達到 hello 下游應用程式開發介面。  Web API 1 會 toorequest 語彙基元代表的 hello 使用者嘗試對 Web API 2，一旦 hello 要求失敗，因為 hello 使用者不具有登入多重要素驗證。

Azure AD 會傳回 HTTP 回應，包含一些有趣的資料： 

> [!NOTE]
> 這個執行個體中很多因素驗證錯誤的描述，但有各種不同的`interaction_required`可能相關 tooconditional 存取。  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

在我們的 Web API 1，攔截 hello 錯誤`error=interaction_required`，並傳送後 hello`claims`挑戰 toohello 傳統型應用程式。  此時，hello 桌面應用程式可以進行新`acquireToken()`呼叫，並附加 hello`claims`做為額外的查詢字串參數的挑戰。  這個新的要求需要 hello 使用者 toodo 多因素驗證，然後傳送這個新的語彙基元後 tooWeb API 1 和完整 hello 代表的流程。

tootry 出此案例中，請參閱我們[.NET 程式碼範例](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca)。  它會示範如何 toopass hello 宣告挑戰，從 Web API 1 toohello 原生應用程式，並建構 hello 用戶端應用程式內的新要求。 

### <a name="scenario-app-accessing-multiple-services"></a>情節：存取多個服務的應用程式

在此案例中，我們逐步 hello 案例 web 應用程式存取兩個服務都有一個具有條件式存取原則指派。  根據您的應用程式邏輯，可能存在您的應用程式不需要存取 tooboth web 服務的路徑。  在此案例中，您可以在其中要求權杖的 hello 順序會扮演重要角色 hello 使用者體驗中。

假設我們有 A 和 B 的 web 服務，而 web 服務 B 已套用我們的條件式存取原則。  雖然 hello 初始互動式驗證要求需要兩個服務的同意，hello 條件式存取原則不需要在所有情況下。  如果 hello 應用程式要求 web 服務 B 的語彙基元，然後叫用 hello 原則和 web 服務的後續要求也成功，如下所示。

![存取多個服務的應用程式流程圖](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

或者，如果 hello 應用程式一開始要求 web 服務的權杖，hello 使用者不會叫用 hello 條件式存取原則。  這允許 hello 應用程式開發人員 toocontrol hello 使用者體驗，並不會強制 hello 條件式存取原則 toobe 在所有情況下叫用。 hello 很難解釋的情況是如果 hello 應用程式接著會要求 web 服務 b 的語彙基元此時，hello 使用者需要 toocomply 與 hello 條件式存取原則。  當 hello 應用程式嘗試過`acquireToken`，可能會產生下列錯誤 （hello 下列圖表中所述） 的 hello: 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![存取多個要求新權杖之服務的應用程式](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

如果 hello 應用程式使用 hello ADAL 程式庫，失敗 tooacquire hello 權杖永遠重試一次以互動方式。  此互動式要求時，hello 使用者有 hello 機會 toocomply hello 條件式存取。  這是 true，除非 hello 要求`AcquireTokenSilentAsync`或`PromptBehavior.Never`hello 應用程式在此情況下需要互動式 tooperform```AcquireToken```要求 toogive hello 結束使用 hello 機會 toocomply hello 原則。 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>情節：使用 ADAL.js 的單一頁面應用程式 (SPA)

在此案例中，我們逐步解說 hello 案例我們有單一頁面應用程式 (SPA) 時，使用 ADAL.js toocall 條件式存取受保護的 web API。  這是簡單的架構，但有一些需要 toobe 開發周圍條件式存取時列入考量的細節。

在 ADAL.js 中，有幾個函式可取得權杖：`login()`、`acquireToken(...)`、`acquireTokenPopup(…)` 和 `acquireTokenRedirect(…)`。 

* `login()` 會透過互動式登入要求取得 ID 權杖，但不會取得任何服務的存取權杖 (包括受條件式存取保護的 web API)。  
* `acquireToken(…)`可以是使用的 toosilently 取得存取權杖，這表示它不在任何情況下顯示 UI。  
* `acquireTokenPopup(…)`和`acquireTokenRedirect(…)`會同時使用的 toointeractively 要求權杖的資源，這表示它們永遠會顯示登入 UI。

當應用程式需要存取語彙基元 toocall Web API 時，它會試著`acquireToken(…)`。  如果 hello 語彙基元的工作階段已過期，或者我們需要 toocomply 與條件式存取原則，然後 hello *acquireToken*函式會失敗，並 hello 應用程式會使用`acquireTokenPopup()`或`acquireTokenRedirect()`。

![使用 ADAL 的單一頁面應用程式流程圖](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

我們會使用條件式存取情節來步解說範例。  hello 使用者只要登陸 hello 站台，並不會有一個工作階段。  我們執行 `login()` 呼叫時，無需進行多重要素驗證即可取得 ID 權杖。  然後 hello 使用者點擊需要 hello 應用程式 toorequest 資料從 web API 的按鈕。  hello 應用程式會嘗試 toodo`acquireToken()`卻會呼叫失敗，因為未執行多重要素驗證尚未 hello 使用者，而且需要 toocomply 與 hello 條件式存取原則。

Azure AD 會傳送下列 HTTP 回應的回復 hello: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

我們的應用程式需要 toocatch hello `error=interaction_required`。  hello 應用程式可以接著使用`acquireTokenPopup()`或`acquireTokenRedirect()`在 hello 相同資源。  hello 使用者是強制的 toodo 多重要素驗證。 Hello 應用程式 hello 使用者完成 hello 多重要素驗證之後，會發出從頭 hello 的存取權杖要求的資源。

tootry 出此案例中，請參閱我們[JS SPA 代表的程式碼範例](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca)。  Hello 條件式存取原則和 web 應用程式開發介面，您先前註冊與 JS SPA toodemonstrate 這種情況下，會使用此程式碼範例。 它會顯示如何 tooproperly 控制代碼 hello 宣告挑戰，並取得存取權杖可用於您的 Web API。 一般或者，簽出 hello [Angular.js 程式碼範例](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp)如角度 SPA 的指引


## <a name="see-also"></a>另請參閱

* toolearn 進一步了解 hello 功能，請參閱[在 Azure AD 中的條件式存取](../active-directory-conditional-access.md)。
* 如需更多的 Azure AD 程式碼範例，請參閱[程式碼範例的 Github 存放庫](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory)。 
* 如需 hello ADAL SDK 及存取 hello 參考文件的詳細資訊，請參閱[文件庫指南](active-directory-authentication-libraries.md)。
* toolearn 進一步了解多租用戶的案例中，請參閱[如何在使用者使用 hello 多租用戶模式 toosign](active-directory-devhowto-multi-tenant-overview.md)。
