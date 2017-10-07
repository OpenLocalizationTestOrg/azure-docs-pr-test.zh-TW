---
title: "Azure AD Application Proxy 的 aaaSecurity 考量 |Microsoft 文件"
description: "涵蓋使用 Azure AD 應用程式 Proxy 的安全性考量"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量

本文說明 Azure Active Directory 應用程式 Proxy 如何提供遠端發佈及存取應用程式的安全服務。

下列圖表顯示 Azure AD 的 hello 可讓安全遠端存取 tooyour 在內部部署應用程式。

 ![透過 Azure AD 應用程式 Proxy 進行安全遠端存取的示意圖](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>安全性優點

Azure AD 應用程式 Proxy 提供下列安全性優點的 hello:

### <a name="authenticated-access"></a>已驗證的存取 

如果您選擇 toouse Azure Active Directory 預先驗證時，已驗證的連線可以存取您的網路。

Azure AD Application Proxy 依賴 hello 所有驗證的 Azure AD 安全性權杖服務 (STS)。  預先驗證，本質，區塊中，大量的匿名攻擊，因為只驗證之身分識別可以存取 hello 後端應用程式。

如果您選擇 Passthrough 作為預先驗證方法，就無法獲得這項優點。 

### <a name="conditional-access"></a>條件式存取

適用於更豐富的原則控制項之前 tooyour 網路建立的連接。

與[條件式存取](active-directory-conditional-access-azuread-connected-apps.md)，您可以定義哪些流量的限制允許 tooaccess 後端應用程式。 您可以位置、驗證強度和使用者風險狀況作為基礎，來建立限制登入的原則。

您也可以使用條件式存取 tooconfigure 多重要素驗證原則，新增另一層的安全性 tooyour 使用者驗證。 

### <a name="traffic-termination"></a>流量終止

所有流量會都終止 hello 雲端中。

因為 Azure AD Application Proxy 是反向 proxy，所有流量 tooback 端應用程式會都終止在 hello 服務。 hello 工作階段可以取得重新建立只能搭配 hello 後端伺服器，也就是說，您的後端伺服器在不公開 toodirect HTTP 流量。 此設定表示，您會受到更妥善的保護，可免於目標型攻擊。

### <a name="all-access-is-outbound"></a>所有存取都是輸出 

您不需要 tooopen 傳入的連接 toohello 公司網路。

應用程式 Proxy 連接器只使用輸出連線 toohello Azure AD 應用程式 Proxy 服務，這表示沒有必要 tooopen 防火牆連接埠的連入連線。 傳統的 proxy 所需的周邊網路 (也稱為*DMZ*，*非軍事區域*，或*過濾的子網路*)，允許存取 toounauthenticated在 hello 網路邊緣的連接。 此案例需要許多額外的投資在 web 應用程式的防火牆產品 tooanalyze 流量，並提供加法保護 toohello 環境。 使用應用程式 Proxy，您就不需要周邊網路，因為所有連線皆為輸出方向，並且是透過安全通道來傳輸。

如需連接器的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。

### <a name="cloud-scale-analytics-and-machine-learning"></a>雲端級別分析與機器學習 

取得最新的安全性保護。

因為它是 Azure Active Directory 的一部分，可以利用應用程式 Proxy [Azure AD Identity Protection](active-directory-identityprotection.md)、 機器學習驅動智慧與 hello Microsoft Security Response Center 和數位犯罪單位的資料。 我們共同主動識別遭入侵的帳戶，並提供來自高風險登入的即時防護。我們考慮許多因素，例如來自受感染裝置、透過匿名網路以及來自非典型與假位置的存取。

這些報告和事件中有許多已可透過 API 與安全性資訊和事件管理 (SIEM) 系統整合。

### <a name="remote-access-as-a-service"></a>遠端存取即服務

您不需要 tooworry 關於維護及修補內部部署伺服器。

未更新的軟體仍需負責處理大量攻擊。 Azure AD Application Proxy 是 Microsoft 所擁有，網際網路規模服務，因此您一定要取得最新安全性修補程式 hello 與升級。

tooimprove hello 由 Azure AD Application Proxy 發行應用程式的安全性，我們會封鎖從編製索引和封存您的應用程式的 web crawler 機器人。 每次 Web 編目程式傀儡程式嘗試擷取已發佈應用程式的傀儡程式設定時，應用程式 Proxy 會以含有 `User-agent: * Disallow: /` 的 robots.txt 檔案回覆。

## <a name="under-hello-hood"></a>Hello 幕後

Azure AD 應用程式 Proxy 是由兩個部分組成︰

* hello 雲端式服務： 此服務執行於 Azure，且其中 hello 外部的用戶端/使用者連線。
* [hello 內部部署連接器](application-proxy-understand-connectors.md): hello 連接器在內部部署元件會接聽來自 hello Azure AD 應用程式 Proxy 服務的要求和處理連線 toohello 內部應用程式。 

建立 hello 連接器與 hello 應用程式 Proxy 服務之間的資料流程時：

* 先設定 hello 連接器。
* hello 連接器會提取從 hello 應用程式 Proxy 服務的組態資訊。
* 使用者會存取發佈的應用程式。

>[!NOTE]
>所有的通訊會透過 SSL，而且它們永遠都是源自於 hello 連接器 toohello 應用程式 Proxy 服務。 hello 服務僅輸出。

hello 連接器會使用用戶端憑證 tooauthenticate toohello 幾乎所有呼叫的應用程式 Proxy 服務。 hello 只例外狀況 toothis 程序是 hello 初始設定步驟中，建立 hello 用戶端憑證的位置。

### <a name="installing-hello-connector"></a>安裝 hello connector

當第一次設定 hello 連接器時，hello 遵循的流程事件會發生：

1. hello 連接器註冊 toohello 服務就會發生 hello hello 連接器安裝的一部分。 使用者會提示的 tooenter 其 Azure AD 系統管理員認證。 從這項驗證權杖會接著呈現 toohello Azure AD 應用程式 Proxy 服務。
2. hello 應用程式 Proxy 服務會評估 hello 語彙基元。 它會確保該 hello 使用者即 hello 語彙基元的 hello 租用戶內的公司系統管理員已發出。 如果 hello 使用者不是系統管理員，則會終止 hello 程序。
3. hello 連接器產生的用戶端憑證要求，並傳遞，連同 hello 語彙基元，toohello 應用程式 Proxy 服務。 hello 服務接著會驗證 hello 語彙基元，並簽署 hello 用戶端憑證要求。
4. hello 連接器會使用與 hello 應用程式 Proxy 服務的未來通訊 hello 用戶端憑證。
5. hello 連接器 hello 系統組態資料的初始提取從 hello 服務使用用戶端憑證，並已準備好 tootake 要求。

### <a name="updating-hello-configuration-settings"></a>更新 hello 組態設定

每當應用程式 Proxy 服務的 hello 更新 hello 組態設定，hello 遵循的流程事件會發生：

1. hello 連接器會使用其用戶端憑證，以連接 toohello hello 應用程式 Proxy 服務設定端點。
2. Hello 應用程式 Proxy 服務已驗證 hello 用戶端憑證之後，傳回組態資料 toohello 連接器 （例如，hello 連接器的 hello 連接器群組應該是的一部分）。
3. 如果 180 天以前 hello 目前的憑證，hello 連接器會產生新的憑證要求，並有效地更新每 180 天 hello 用戶端憑證。

### <a name="accessing-published-applications"></a>存取已發佈的應用程式

當使用者存取已發行的應用程式時，hello 下列事件會發生 hello 應用程式 Proxy 服務之間 hello 應用程式 Proxy 連接器：

1. [hello 服務會驗證 hello hello 應用程式的使用者](#the-service-checks-the-configuration-settings-for-the-app)
2. [hello 服務會將要求放在 hello 連接器佇列](#The-service-places-a-request-in-the-connector-queue)
3. [連接器處理 hello hello 佇列要求](#the-connector-receives-the-request-from-the-queue)
4. [hello 連接器等候回應](#the-connector-waits-for-a-response)
5. [hello 服務資料流資料 toohello 使用者](#the-service-streams-data-to-the-user)

深入了解什麼發生在每個步驟，toolearn 保留讀取。


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1.hello 服務會驗證 hello hello 應用程式的使用者

如果您設定 hello 應用程式 toouse 傳遞做為其預先驗證方法時，會略過本節中的 hello 步驟。

如果您使用 Azure AD 設定 hello 應用程式 toopreauthenticate，使用者會重新導向的 toohello Azure AD STS tooauthenticate，而且 hello 下列步驟進行：

1. 應用程式 Proxy 會檢查任何 hello 特定應用程式的條件式存取原則需求。 這個步驟可確保該 hello 使用者已獲指派 toohello 應用程式。 如果需要雙步驟驗證，hello 驗證順序就會提示 hello 使用者在第二個驗證方法。

2. 已通過所有檢查之後，hello Azure AD STS 發出 hello 應用程式的簽署語彙基元，並重新導向 hello 使用者回復 toohello 應用程式 Proxy 服務。

3. 應用程式 Proxy 會確認該 hello 語彙基元發出 toocorrect hello 應用程式。 它也會執行其他檢查權杖簽署由 Azure AD，例如確保該 hello，它仍在 hello 有效的視窗。

4. 應用程式 Proxy 設定發生驗證 toohello 應用程式加密的驗證 cookie tooindicate。 hello cookie 包含根據 hello 來自 Azure AD 的權杖及其他資料的到期時間戳記，例如 hello hello 驗證的使用者名稱為基礎。 使用已知 toohello 應用程式 Proxy 服務的私密金鑰來加密 hello cookie。

5. 應用程式 Proxy 重新導向 hello 使用者回復 toohello 原始要求的 URL。

如果 hello 預先驗證步驟的任何部分失敗，hello 使用者的要求遭到拒絕，並 hello 使用者顯示訊息，指出 hello hello 問題來源。


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2.hello 服務會將要求放在 hello 連接器佇列

連接器會將輸出連線開啟 toohello 應用程式 Proxy 服務。 當要求進入時，則會將 hello 服務上的向上 hello 連接器 toopick hello 開啟連接的其中一個 hello 要求排入佇列。

hello 要求包含項目從 hello 應用程式，例如 hello 要求標頭，從 hello 加密 cookie 資料、 hello 使用者進行 hello 要求，並 hello 要求識別碼。 雖然資料從 hello 加密 cookie 傳送 hello 要求，但不是本身 hello 驗證 cookie。

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3.hello 連接器處理 hello 從 hello 佇列的要求。 

根據 hello 要求，應用程式 Proxy 會執行下列動作的 hello 的其中一個：

* 如果 hello 要求是簡單的作業 (例如，沒有資料現況 RESTful hello 主體內*取得*要求)，hello 連接器可讓連接 toohello 目標內部資源，然後等候回應。

* 如果 hello 要求有與其相關聯 hello 主體中的資料 (例如，RESTful *POST*作業)，hello 連接器可藉由使用 hello 用戶端憑證 toohello 應用程式 Proxy 執行個體的輸出連線。 它會建立此連線 toorequest hello 資料，並開啟連接 toohello 內部資源。 在收到 hello 連接器 hello 要求之後，hello 應用程式 Proxy 服務開始接受來自 hello 使用者內容，並將轉寄資料 toohello 連接器。 hello 連接器，亦會將轉送 hello 資料 toohello 內部資源。

#### <a name="4-hello-connector-waits-for-a-response"></a>4.hello 連接器等候回應。

Hello 要求及所有內容 toohello 傳輸回後端完成，hello 連接器等候回應。

收到回應後，hello 連接器可讓輸出連線 toohello 應用程式 Proxy 服務，tooreturn hello 標頭的詳細資料，並開始串流處理 hello 傳回資料。

#### <a name="5-hello-service-streams-data-toohello-user"></a>5.hello 服務資料流資料 toohello 使用者。 

一些處理 hello 應用程式可能會發生以下。 如果您在應用程式中設定應用程式 Proxy tootranslate 標頭或 Url，該處理會視需要在此步驟進行。


## <a name="next-steps"></a>後續步驟

[使用 Azure AD 應用程式 Proxy 時的網路拓撲考量](application-proxy-network-topology-considerations.md)

[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)
