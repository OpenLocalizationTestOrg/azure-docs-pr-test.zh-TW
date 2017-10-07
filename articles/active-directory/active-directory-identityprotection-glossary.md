---
title: "Active Directory Identity Protection 字彙 aaaAzure |Microsoft 文件"
description: "Azure Active Directory Identity Protection 詞彙"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則, 詞彙"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Azure Active Directory Identity Protection 詞彙
### <a name="at-risk-user"></a>有風險 (使用者)
具有一或多個作用中風險事件的使用者。 

### <a name="atypical-sign-in-location"></a>非典型登入位置
登入不是標準 hello 特定使用者、 類似使用者，或 hello 租用戶的地理位置。

### <a name="azure-ad-identity-protection"></a>Azure AD Identity Protection
Azure Active Directory 的安全性模組，可供整合檢視會影響組織身分識別的風險事件和潛在弱點。

### <a name="conditional-access"></a>條件式存取
保護存取 tooresources 的原則。 條件式存取規則儲存在 hello Azure Active Directory，而且由 Azure AD 授與存取 toohello 資源之前加以評估。  範例規則包括根據使用者位置、裝置健康狀態或使用者驗證方法來限制存取。

### <a name="credentials"></a>認證
包含之識別與已使用的 toogain 存取 toolocal 和網路資源的識別證明的資訊。 認證範例包括使用者名稱和密碼、智慧卡和憑證。

### <a name="event"></a>Event
Azure Active Directory 中的活動記錄。

### <a name="false-positive-risk-event"></a>誤判 (風險事件)
手動設定識別身分保護使用者，表示該 hello 風險事件已調查和不正確地標示為風險事件的風險事件狀態。

### <a name="identity"></a>身分識別
必須透過以密碼或憑證等準則為基礎的驗證作業來確認的個人或實體。

### <a name="identity-risk-event"></a>身分識別風險事件
由 Identity Protection 標示為異常的 AAD 事件，有可能表示身分識別已被入侵。

### <a name="ignored-risk-event"></a>已忽略 (風險事件)
手動設定識別身分保護使用者，指出該 hello 風險事件已關閉但不採取補救動作的風險事件狀態。

### <a name="impossible-travel-from-atypical-locations"></a>不可能來自非典型位置的移動
周遊這些之間的風險事件觸發時需要 toophysically 兩個相同的使用者會偵測到，其中至少一個是從非典型的登入位置，以及在 hello hello 登入之間的時間長度小於最小的 hello 時間的 hello 登入。位置。  

### <a name="investigation"></a>調查
hello 檢閱 hello 活動、 記錄和其他相關資訊的程序相關 tooa 風險事件 toodecide 是否補救或安全防護功能步驟，了解如何 hello 身分識別已遭到洩露，並了解如何 hello使用遭盜用身分識別。

### <a name="leaked-credentials"></a>認證外洩
風險事件觸發時發現目前的使用者認證 （使用者名稱和密碼） 公開公佈在我們的研究人員 hello 深色 web。

### <a name="mitigation"></a>緩和
動作 toolimit 或消除 hello 的攻擊者 tooexploit 遭盜用身分識別或裝置的能力，而不還原 hello 身分識別或裝置 tooa 安全狀態。 緩和措施無法解決先前 hello 身分識別或裝置相關聯的風險事件。

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
驗證方法，需要兩個或多個驗證方法，其可能包括 hello 使用者擁有的項目，這類憑證;項目 hello 使用者知道，例如使用者名稱、 密碼或複雜密碼。實體的屬性，例如指紋。與個人的屬性，例如個人簽章。

### <a name="offline-detection"></a>離線偵測
hello 偵測異常和 hello 事實，已發生的事件之後的事件，例如登入嘗試的 hello 風險評估。

### <a name="policy-condition"></a>原則條件
安全性原則會定義 hello 實體群組、 使用者、 應用程式、 裝置平台，裝置狀態、 IP 範圍 （用戶端類型） 從它 hello 原則中包含或排除的一部分。

### <a name="policy-rule"></a>原則規則
hello 部分說明 hello 情況會觸發 hello 原則以及 hello 所採取動作時，就會觸發 hello 原則的安全性原則。

### <a name="prevention"></a>預防
動作 tooprevent 損害 toohello 透過濫用的組織的身分識別或裝置懷疑，或者知道 toobe 入侵。 防止動作不保護 hello 裝置或識別，並無法解決先前的風險事件。

### <a name="privileged-user"></a>特殊權限 (使用者)
在 Azure Active Directory，例如為全域管理員，具有永久或暫時的系統管理員權限 tooone 或更多資源的 hello 的風險事件期間，在使用者計費管理員、 服務系統管理員、 使用者管理員和密碼系統管理員。 

### <a name="real-time"></a>即時
請參閱即時偵測。

### <a name="real-time-detection"></a>即時偵測
hello 異常偵測的事件，例如登入嘗試 hello 事件之前的 hello 風險評估允許和 tooproceed。

### <a name="remediated-risk-event"></a>已補救 (風險事件)
自動設定的識別身分保護，指出該 hello 風險事件補救這種類型的風險事件使用 hello 標準的補救動作的風險事件狀態。 例如，當 hello 使用者密碼重設時，許多指示該 hello 先前的密碼已遭到洩露的風險事件都會自動補救。

### <a name="remediation"></a>補救
動作 toosecure 身分識別或先前可疑或已知 toobe 的裝置遭到洩露。 補救動作還原 hello 身分識別或裝置 tooa 安全的狀態，並解決先前 hello 身分識別或裝置相關聯的風險事件。

### <a name="resolved-risk-event"></a>已解決 (風險事件)
手動設定識別身分保護使用者，表示 hello 使用者採取適當的補救動作以外的識別身分保護，且該 hello 風險事件應該被視為風險事件狀態已關閉。

### <a name="risk-event-status"></a>風險事件狀態
風險事件屬性，指出是否 hello 事件為作用中，而且如果已關閉，關閉它 hello 原因。

### <a name="risk-event-type"></a>風險事件類型
某項分類 hello 的風險事件，指出造成 hello 事件 toobe 視為危險的異常 hello 型別。

### <a name="risk-level-risk-event"></a>風險層級 (風險事件)
（高、 中或低） 它們的相對值指示 hello 風險事件 toohelp 識別身分保護使用者 hello 嚴重性排定優先順序採取 tooreduce hello 風險 tootheir 組織 hello 動作。 

### <a name="risk-level-sign-in"></a>風險層級 (登入)
表示 （高、 中或低） hello 可能性特定登入，其他人正在嘗試 toouse hello 使用者的身分識別。

### <a name="risk-level-user-compromise"></a>風險層級 (使用者入侵)
Hello 身分識別已遭洩漏的可能性表示 （高、 中或低）。

### <a name="risk-level-vulnerability"></a>風險層級 (弱點)
（高、 中或低） 它們的相對值指示 hello 弱點 toohelp 識別身分保護使用者 hello 嚴重性排定優先順序採取 tooreduce hello 風險 tootheir 組織 hello 動作。

### <a name="secure-identity"></a>安全 (身分識別)
採取補救動作，例如密碼變更或重新安裝映像 toorestore 潛在受危害的身分識別 tooan 洩露的狀態機器。

### <a name="security-policy"></a>安全性原則
原則規則和條件的集合。 原則可以套用的 tooentities 像是使用者、 群組、 應用程式、 裝置、 裝置平台，裝置狀態、 IP 範圍，以及 Auth2.0 用戶端類型。 啟用原則時，它會評估每次發出資源的語彙基元 hello 原則中所包含的實體時。

### <a name="sign-in-v"></a>登入 (動詞)
在 Azure Active Directory tooauthenticate tooan 身分識別。

### <a name="sign-in-n"></a>登入 (名詞)
hello 程序或驗證 Azure Active Directory 和擷取這項作業的 hello 事件中的身分識別的動作。

### <a name="sign-in-from-anonymous-ip-address"></a>從匿名 IP 位址登入
從被視為匿名 Proxy IP 位址的 IP 位址成功登入之後所觸發的風險事件。

### <a name="sign-in-from-infected-device"></a>從受感染的裝置登入
風險事件觸發時登入來自已知 toobe 裝置所使用一或多個遭入侵，主動嘗試 toocommunicate bot 伺服器的 IP 位址。

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>從具有可疑活動的 IP 位址登入
從短期內透過多個使用者帳戶多次嘗試登入失敗的 IP 位址成功登入之後所觸發的風險事件。

### <a name="sign-in-from-unfamiliar-location"></a>從不熟悉的位置登入
當使用者從新的位置 (IP、經緯度和 ASN) 成功登入時所觸發的風險事件。

### <a name="sign-in-risk"></a>登入風險
請參閱風險層級 (登入)

### <a name="sign-in-risk-policy"></a>登入風險原則
條件式存取原則，評估 hello 風險 tooa 特定登入，並根據預先定義的條件和規則的防護措施。

### <a name="user-compromise-risk"></a>使用者入侵風險
請參閱風險層級 (使用者入侵)

### <a name="user-risk"></a>使用者風險
請參閱風險層級 (使用者入侵)。

### <a name="user-risk-policy"></a>使用者風險原則
條件式存取原則，會考慮 hello 登入，並根據預先定義的條件和規則的防護措施。

### <a name="users-flagged-for-risk"></a>標示有風險的使用者
具有作用中或已補救之風險事件的使用者

### <a name="vulnerability"></a>弱點
設定或讓 hello 目錄很容易遭受 tooexploits 或潛在威脅的 Azure Active Directory 中的條件。

## <a name="see-also"></a>另請參閱
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

