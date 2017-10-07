---
title: "aaaUnderstanding hello OAuth2 隱含授與流程在 Azure AD 中 |Microsoft 文件"
description: "深入了解 Azure Active Directory 的實作 hello OAuth2 隱含授與流程，以及它是否適合您的應用程式。"
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>了解 hello OAuth2 隱含授與流程在 Azure Active Directory (AD)
hello OAuth2 隱含授予是昭彰的 hello 授與具有 hello hello OAuth2 規格中的安全性顧慮的最長的清單。 而棒的是，這是 hello ADAL JS 和一個撰寫 SPA 應用程式時，我們建議您使用 hello 所實作的方法。 為何會這樣呢？ 它是所有的權衡取捨:，且證明，hello 隱含授予 hello 最好的方法，您可以嘗試使用 Web API 透過 JavaScript 從瀏覽器的應用程式。

## <a name="what-is-hello-oauth2-implicit-grant"></a>Hello OAuth2 隱含授予是什麼？
典型的 hello [OAuth2 授權碼授與](https://tools.ietf.org/html/rfc6749#section-1.3.1)是 hello 授權授與它使用兩個單獨的端點。 hello 使用者互動階段中，會導致授權程式碼會使用 hello 授權端點。 hello 用戶端接著會使用 hello 語彙基元端點來交換存取權杖，且經常重新整理權杖的 hello 程式碼。 Web 應用程式是必要的 toopresent 他們自己的應用程式認證 toohello 權杖端點，如此 hello 授權伺服器可以驗證 hello 用戶端。

hello [OAuth2 隱含授予](https://tools.ietf.org/html/rfc6749#section-1.3.2)是其他授權授與。 它可讓用戶端 tooobtain 存取權杖 (id_token 時使用和[OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) 直接從 hello 授權端點，而不連絡 hello 權杖端點，也不驗證 hello 用戶端。 此變異，專為以 JavaScript 為基礎的 Web 瀏覽器中執行的應用程式： hello 原始 OAuth2 規格，在語彙基元會傳回 URI 片段中。 會讓 hello 語彙基元的位元可用 toohello JavaScript 程式碼在 hello 用戶端，但它可以保證不會納入朝 hello 伺服器的重新導向。 直接從 hello 授權端點傳回語彙基元，透過瀏覽器重新導向。 它也有 hello 優點消除跨原始呼叫，也就是 hello JavaScript 應用程式是否需要的 toocontact hello 權杖端點所需的任何需求。

Hello OAuth2 隱含授予的重要特性在於這類流程永遠不會傳回重新整理語彙基元 toohello 用戶端的 hello 事實。 我們將會看到 hello 下一節中，，不是真有必要，因此實際上會有安全性問題。

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>授與的 hello OAuth2 隱含適合案例
Hello OAuth2 規格本身宣告，如 hello 隱含授予已設計的 tooenable 使用者代理程式的應用程式 – 是 toosay，瀏覽器中執行的 JavaScript 應用程式。 hello 定義這類應用程式的特性是 JavaScript 程式碼，用來存取伺服器資源 (通常是 Web API) 及 hello 應用程式 UX 據此更新。 考慮應用程式，例如 Gmail 或 Outlook Web Access： 當您選取訊息收件匣中，只有 hello 訊息，視覺效果面板變更 toodisplay hello 新選取項目，同時 hello hello 頁面其餘部分維持不修改。 這是相較於傳統重新導向式 Web 應用程式，其中每個使用者互動會導致完整網頁回傳和新的伺服器回應 hello 整頁轉譯。

應用程式來充分 hello JavaScript 為基礎的方法 tooits 極端稱為單一頁面應用程式或 SPAs: hello 概念是，這些應用程式只有提供初始的 HTML 網頁和相關聯的 JavaScript 含有的所有後續的互動透過 JavaScript 執行 web 應用程式開發介面呼叫。 不過，混合式方法，其中 hello 應用程式大致回傳導向，但執行偶爾 JS 呼叫，並不常見，-也是相關的 hello 隱含流程使用方式的討論。

重新導向型應用程式通常會透過 Cookie 來保護其要求，不過，這種方法並非也適用於 JavaScript 應用程式。 Cookie 用於 hello 它們已產生的當 JavaScript 呼叫可能會導向其他網域的網域。 事實上，經常會 hello 案例： 考慮叫用 Microsoft Graph API，Office 應用程式開發介面，Azure API – 從 hello 應用程式提供其中 hello 網域之外的所有位於應用程式。 JavaScript 應用程式的趨勢日益是 toohave 任何後端，其商務功能信賴憑證者在第 3 個合作對象的 Web Api tooimplement 100%。

目前，hello 保護呼叫 tooa Web 應用程式開發介面的慣用的方法是 toouse hello OAuth2 bearer 權杖的方法，其中每個呼叫會伴隨 OAuth2 存取權杖。 hello Web API 會檢查 hello 連入的存取權杖，而如果它在中找到它 hello 必要的範圍，它會授與存取 toohello 要求的作業。 hello 隱含流程提供方便的機制，JavaScript 應用程式 tooobtain 存取權杖的 Web API，供應項目中的有很多優點尊重 toocookies:

* 語彙基元可以可靠地取得而不需要跨原始呼叫 – 強制註冊 hello 重新導向 URI toowhich 語彙基元會傳回可保證，語彙基元是不脫離頁面
* JavaScript 應用程式可以針對任意數量的鎖定 Web API 取得所需數量的存取權杖 – 不限網域
* HTML5 功能類似工作階段或本機儲存體而 cookie 管理是不透明 toohello 應用程式授與完整控制權杖快取和存留期管理
* 存取權杖不容易受到 tooCross 站台要求偽造 (CSRF) 攻擊

hello 隱含授與流程不會發出重新整理權杖，主要是基於安全性考量。 重新整理權杖的範圍不像存取權杖那麼窄，前者會授與更多權力，因此萬一洩露出去，將會造成更大的損害。在 hello 隱含流程中，hello URL 中傳遞權杖，因此攔截 hello 風險高於 hello 授權碼授與。

不過請注意 JavaScript 應用程式有另一個機制，在進行處置時的更新存取權杖，而不會重複提示 hello 使用者提供認證。 hello 應用程式可以使用隱藏的 iframe tooperform 新權杖要求對 hello Azure AD 授權端點： 只要 hello 瀏覽器仍有作用中的工作階段 (讀取： 有一個工作階段 cookie) 針對 hello Azure AD 網域 hello 驗證要求順利執行而不需要使用者互動。

此模型會授與 hello JavaScript 應用程式 hello 能力 tooindependently 更新存取權杖，而且即使取得新 api 的新的 （前提是 hello 使用者之前同意它們。 這可避免 hello 加入的負擔取得、 維護和保護高價值成品，例如重新整理權杖。 hello 成品這樣 hello 無訊息更新能，hello Azure AD 工作階段 cookie，管理 hello 應用程式之外。 這種方法的另一個好處是使用者可以登出任何登入 Azure AD 中，執行任何 hello 瀏覽器索引標籤中的 hello 應用程式，使用 Azure AD。 這會導致 hello hello Azure AD 工作階段 cookie，刪除與 hello JavaScript 應用程式會自動遺失 hello 能力 toorenew 語彙基元的 hello 登出使用者。

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>適合 hello 隱含授與我的應用程式嗎？
hello 隱含授予有更多的風險，比其他授權的而且您需要 toopay 注意 tooare 記載完善的 hello 區域。 例如，[誤用的存取權杖 tooImpersonate 資源擁有者在隱含流程][ OAuth2-Spec-Implicit-Misuse]和[OAuth 2.0 威脅模型與安全性考量][OAuth2-Threat-Model-And-Security-Implications]). 不過，hello 高風險設定檔是主要是因為 toohello 事實，是執行遠端資源 tooa 瀏覽器所服務的使用中程式碼的 tooenable 應用程式。 如果您計劃 SPA 架構中，有任何後端元件，或是想 tooinvoke 透過 JavaScript 的 Web 應用程式開發介面，建議使用的 hello 隱含流程權杖取得。

如果您的應用程式是原生用戶端，hello 隱含流程不好調整。 原生用戶端 hello 內容中的 hello Azure AD 工作階段 cookie 的 hello 缺乏 deprives hello 表示維護長期的工作階段的應用程式。 取得新資源的存取權杖時，這表示您的應用程式會重複會提示 hello 使用者。

如果您正在開發 Web 應用程式包括後端，並使用它的後端程式碼的 API，hello 隱含流程也會不適合。 其他授與可提供您更多權力。 例如，hello OAuth2 用戶端認證授與提供 hello 能力 tooobtain 語彙基元，以反映 hello 權限指派 toohello 應用程式本身，但不要的 toouser 委派。 這表示 hello 用戶端 hello 能力 toomaintain 以程式設計方式存取 tooresources 即使使用者未主動參與工作階段，依此類推。 不只如此，這類授與也能提供較高的安全性保證。 比方說，永遠不會傳輸透過 hello 使用者瀏覽器的存取權杖，它們不在 hello 瀏覽器歷程記錄中儲存的風險等。 hello 用戶端應用程式在要求權杖時，也可以執行強式驗證。

## <a name="next-steps"></a>後續步驟
* 如需開發人員資源的完整清單，包括 hello 通訊協定和 OAuth2 授權授與流程支援的 Azure AD 中，參考資訊，請參閱 toohello [Azure AD 開發人員指南][AAD-Developers-Guide]
* 請參閱[如何 toointegrate 應用程式與 Azure AD] [ ACOM-How-To-Integrate] hello 應用程式整合程序上的其他深度。

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
