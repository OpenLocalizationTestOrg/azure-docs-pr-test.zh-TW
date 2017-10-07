---
title: "aaaAzure Active Directory 的風險事件 |Microsoft 文件"
description: "本主題詳述何謂風險事件。"
services: active-directory
keywords: "azure active directory identity protection, 安全性, 風險, 風險層級, 弱點, 安全性原則"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Azure Active Directory 風險事件

攻擊者竊取使用者的身分識別取得存取 tooan 環境時，就會放置 hello 大部分的安全性缺口，這需要。 探索遭入侵的身分識別並不容易。 Azure Active Directory 使用彈性的機器學習演算法和啟發學習法 toodetect 可疑動作相關的 tooyour 使用者帳戶。 偵測到的每個可疑動作會儲存在名為*風險事件*的記錄中。

Azure Active Directory 目前會偵測六種風險事件類型：

- [認證外洩的使用者](#leaked-credentials) 
- [從匿名 IP 位址登入](#sign-ins-from-anonymous-ip-addresses) 
- [不可能的旅遊 tooatypical 位置](#impossible-travel-to-atypical-locations) 
- [從不熟悉的位置登入](#sign-in-from-unfamiliar-locations)
- [從受感染的裝置登入](#sign-ins-from-infected-devices) 
- [從具有可疑活動的 IP 位址登入](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![風險事件](./media/active-directory-reporting-risk-events/91.png)

本主題提供您哪些風險事件的詳細的概觀會和您可以如何使用這些 tooprotect 您 Azure AD 身分識別。


## <a name="risk-event-types"></a>風險事件類型

hello 風險事件類型的屬性是已建立 hello 可疑動作的風險事件記錄的識別碼。  
Microsoft 的連續投資放在 hello 偵測處理程序會導致：

- 現有的風險事件的增強功能 toohello 偵測正確性 
- 將在未來的 hello 中加入的新風險事件類型

### <a name="leaked-credentials"></a>認證外洩

當 cybercriminals 洩露合法使用者的有效密碼時，hello 罪犯通常會共用這些認證。 這通常是經由張貼公開 hello 深色 web 或貼上站台上，或由交易或銷售 hello 黑市 hello 認證。 hello Microsoft 外洩認證服務取得使用者名稱 / 密碼組藉由監視公用及深色的網站，並使用：

- 研究員
- 執法機關
- Microsoft 安全性小組
- 其他受信任的來源 

當 hello 服務取得使用者名稱 / 密碼組，它們會針對檢查 AAD 使用者的目前有效的認證。 找到相符項目時，表示使用者的密碼已遭入侵，並已建立認證外洩風險事件。

### <a name="sign-ins-from-anonymous-ip-addresses"></a>從匿名 IP 位址登入

此風險事件類型會識別從被視為匿名 Proxy IP 位址的 IP 位址成功登入的使用者。 這些 proxy 是 toohide 的人使用其裝置的 IP 位址，並可用於被用於惡意用途。


### <a name="impossible-travel-tooatypical-locations"></a>不可能的旅遊 tooatypical 位置

這個風險事件類型識別兩個登入來自不同地理位置不同的位置，其中至少一個 hello 位置也可能慣用 hello 使用者，根據過去的行為。 此外，hello hello 兩次登入之間的時間長度小於 hello 階段需花費 hello 使用者 tootravel 從第一個位置 toohello hello 第二個，表示有不同的使用者正在使用 hello 相同的認證。 

會忽略明顯此機器學習演算法"*誤判*」 參與 toohello 不可能的旅遊條件，例如 Vpn 和定期使用 hello 組織中其他使用者的位置。  hello 系統具有初始學習期間內，是在 14 天的期間，它學習新的使用者登入行為。

### <a name="sign-in-from-unfamiliar-locations"></a>從不熟悉的位置登入

這個風險事件類型會考慮過去的登入位置 (IP、 緯度 / 經度和 ASN) toodetermine 新 / 不熟悉的位置。 hello 系統儲存的使用者，使用先前的位置的相關資訊，並將這些 「 熟悉"的位置。 hello 風險事件觸發 hello 登入，就會發生的位置，還不熟悉的位置 hello 清單中。 hello 系統具有初始學習期間的 30 天，在它不會不加上旗標任何新位置中，如不熟悉的位置。 hello 系統也會忽略從熟悉的裝置登入，並屬於不同地理位置關閉 tooa 熟悉的位置。 

### <a name="sign-ins-from-infected-devices"></a>從受感染的裝置登入

這個風險事件類型會識別裝置感染惡意程式碼，稱為 tooactively bot 伺服器通訊的登入。 這取決於相互關聯的 hello 使用者的裝置已 bot 伺服器的 IP 位址的 IP 位址。 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>從具有可疑活動的 IP 位址登入
此風險事件類型會識別在短期內透過多個使用者帳戶多次嘗試登入失敗的 IP 位址。 這符合攻擊者，所使用的 IP 位址的流量模式，而且是強式的指標帳戶可能已經或即將 toobe 入侵。 這是會忽略明顯的機器學習演算法"*false 誤判*"，例如 IP 位址的定期供 hello 組織中其他使用者。  hello 系統有 14 天的初始學習期間內，它會學習 hello 登入新的使用者和新的租用戶的行為。


## <a name="detection-type"></a>偵測類型

hello 偵測類型屬性都是指標 （即時或離線） 的風險事件 hello 偵測時間範圍內。  
目前，大部分的風險事件皆偵測為離線後置處理作業中發生 hello 風險事件之後。

hello 下表列出花費的時間偵測類型 tooshow 相關的報表中的 hello 數量：

| 偵測類型 | 報告延遲 |
| --- | --- |
| 即時 | 5 too10 分鐘 |
| 離線 | 2 too4 小時 |


Azure Active Directory 偵測到 hello 風險事件類型，hello 偵測類型為：

| 風險事件類型 | 偵測類型 |
| :-- | --- | 
| [認證外洩的使用者](#leaked-credentials) | 離線 |
| [從匿名 IP 位址登入](#sign-ins-from-anonymous-ip-addresses) | 即時 |
| [不可能的旅遊 tooatypical 位置](#impossible-travel-to-atypical-locations) | 離線 |
| [從不熟悉的位置登入](#sign-in-from-unfamiliar-locations) | 即時 |
| [從受感染的裝置登入](#sign-ins-from-infected-devices) | 離線 |
| [從具有可疑活動的 IP 位址登入](#sign-ins-from-ip-addresses-with-suspicious-activity) | 離線|


## <a name="risk-level"></a>風險層級

hello 風險層級屬性的風險事件是 hello 嚴重性和 hello 信賴度的風險事件的指標 （高、 中或低）。 這個屬性可協助您您必須採取 tooprioritize hello 動作。 

hello hello 風險事件嚴重性的身分識別洩漏預測工具以表示 hello hello 訊號強度。  
hello 信心是 hello 可能性誤判的指標。 

例如， 

* **高**：高信賴度和高嚴重性風險事件。 這些事件是強式的指標，hello 使用者的身分識別已遭洩漏，，和任何受影響的使用者帳戶應該立即進行補救。

* **中**：高嚴重性，但信賴度較低的風險事件，或反之亦然。 這些事件具有潛在風險，而且應該補救任何受影響的使用者帳戶。

* **低**：低信賴度和低嚴重性風險事件。 此事件可能不需要立即採取行動，但是結合其他風險的事件，則可能會受到強式表示 hello 身分識別提供。

![風險層級](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>認證外洩

外洩風險事件分類為認證**高**，因為它們提供清楚 hello 使用者名稱和密碼是可用 tooan 攻擊者的指示。

### <a name="sign-ins-from-anonymous-ip-addresses"></a>從匿名 IP 位址登入

這個風險事件類型的 hello 風險層級是**媒體**因為匿名 IP 位址不是強式帳戶遭到入侵的指示。  
我們建議您立即連絡 hello 使用者 tooverify，如同使用匿名 IP 位址。


### <a name="impossible-travel-tooatypical-locations"></a>不可能的旅遊 tooatypical 位置

不可能的旅遊通常是很好的指標，駭客已能 toosuccessfully 登入。 不過，使用新的裝置，還是使用通常不是由 hello 組織中其他使用者的 VPN 旅途使用者，可能會發生 false 誤判。 False 誤判的另一個來源是不正確地為用戶端 Ip 時，可能會提供給 hello 外觀傳遞伺服器 Ip 的應用程式的登入裝載 hello 其中該應用程式的後端的資料中心發生 （這些通常是 Microsoft 資料中心，這可能會產生 hello 外觀的登入正在進行中，從 Microsoft 所擁有的 IP 位址)。 因為這些假象，而這個風險事件 hello 風險層級是**媒體**。

> [!TIP]
> 您可以減少這個風險事件類型的報告 false positves 的 hello 數量設定[名為位置](active-directory-named-locations.md)。 

### <a name="sign-in-from-unfamiliar-locations"></a>從不熟悉的位置登入

不熟悉的位置可提供強式表示攻擊者可以 toouse 遭竊的身分識別。 當使用者正在移動、試用新裝置或使用新的 VPN 時，可能會發生誤判。 由於這些誤判 hello 風險層級，此事件類型是**媒體**。

### <a name="sign-ins-from-infected-devices"></a>從受感染的裝置登入

此風險事件可識別 IP 位址，而不是使用者裝置。 如果數個裝置位於單一 IP 位址，且只有一些會受 bot 網路，請從其他裝置的登入我的觸發程序此事件不必要地，即 hello 原因來分類此風險事件做為**低**。  

我們建議您連絡 hello 使用者並掃描所有 hello 使用者的裝置。 它也是可能感染使用者的個人裝置，或如先前所述，有其他人已使用受感染的裝置 hello 從相同 IP 位址以 hello 使用者。 受感染的裝置通常會受到防毒軟體尚未識別，也可能表示為不正確的使用者習慣可能造成 hello 裝置 toobecome 感染的惡意程式碼。

如需有關如何 tooaddress 惡意程式碼的感染項目，請參閱 hello[惡意程式碼防護中心](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409)。


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>從具有可疑活動的 IP 位址登入

我們建議您連絡 hello 使用者 tooverify，如果它們實際用來登入已標記為可疑的 IP 位址。 hello 風險層級，此事件類型是"**媒體**"因為數個裝置可能在後方 hello 相同的 IP 位址，而只對某些可能會負責 hello 可疑的活動。 


 
## <a name="next-steps"></a>後續步驟

風險事件是 hello foundation 來保護您的 Azure AD 身分識別。 Azure AD 目前可以偵測六種風險事件： 


| 風險事件類型 | 風險層級 | 偵測類型 |
| :-- | --- | --- |
| [認證外洩的使用者](#leaked-credentials) | 高 | 離線 |
| [從匿名 IP 位址登入](#sign-ins-from-anonymous-ip-addresses) | 中型 | 即時 |
| [不可能的旅遊 tooatypical 位置](#impossible-travel-to-atypical-locations) | 中型 | 離線 |
| [從不熟悉的位置登入](#sign-in-from-unfamiliar-locations) | 中型 | 即時 |
| [從受感染的裝置登入](#sign-ins-from-infected-devices) | 低 | 離線 |
| [從具有可疑活動的 IP 位址登入](#sign-ins-from-ip-addresses-with-suspicious-activity) | 中型 | 離線|

可以從何處 hello 偵測到您的環境中的風險事件？
您可以在兩個地方檢閱已報告的風險事件：

 - **Azure AD 報告** - 風險事件屬於 Azure AD 的安全性報表。 如需詳細資訊，請參閱 hello[風險安全性報告使用者](active-directory-reporting-security-user-at-risk.md)和 hello[危險的登入安全性報告](active-directory-reporting-security-risky-sign-ins.md)。

 - **Azure AD Identity Protection** - 風險事件也屬於 [Azure Active Directory Identity Protection](active-directory-identityprotection.md) 的報告功能。
    

Hello 偵測的風險事件已代表保護您的身分識別的重要層面，而您也可以手動加以解決，或甚至會藉由設定條件式存取原則實作自動化的回應 hello 選項 tooeither。 如需詳細資料，請參閱 [Azure Active Directory Identity Protection](active-directory-identityprotection.md)。
 
