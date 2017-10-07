---
title: "Active Directory 識別身分保護 aaaAzure |Microsoft 文件"
description: "了解如何 Azure AD Identity Protection 可讓您 toolimit hello 能力，攻擊者 tooexploit 遭盜用身分識別的裝置或 toosecure 盜用身分識別或先前已 toobe 可疑或已知的裝置。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory 識別身分保護是可讓您的 Azure AD Premium P2 hello 版本的功能：

- 偵測會影響組織的身分識別的潛在弱點

- 設定自動化的回應 toodetected 可疑動作相關的 tooyour 組織的身分識別  

- 調查可疑的事件，並採取適當的動作 tooresolve 它們   


## <a name="getting-started"></a>開始使用

Microsoft 保護雲端身分識別已經超過十多年。 Azure Active Directory 識別身分保護，在您環境中，您可以使用 hello 相同保護系統 Microsoft 會使用 toosecure 身分識別。

攻擊者竊取使用者的身分識別取得存取 tooan 環境時，就會放置 hello 大部分的安全性缺口，這需要。 Hello 年來，攻擊者已成為逐漸有效運用第三方漏洞，並使用複雜的網路釣魚攻擊。 攻擊者存取 tooeven 低特殊權限的使用者帳戶，因為它是相當簡單，透過橫向移動 toogain 存取 tooimportant 公司資源。

如此一來，您必須：

- 保護所有的識別身分，不論其權限層級

- 主動防止遭入侵的身分識別被濫用

探索遭入侵的身分識別並不容易。 啟發學習法 toodetect 異常和可疑的事件，以表示可能會受到危害之身分識別和 azure Active Directory 使用彈性的機器學習演算法。 Identity Protection 使用這項資料，產生的報告和警示，讓您 tooevaluate hello 偵測到問題並採取適當的安全防護或修復動作。

Azure Active Directory Identity Protection 不只是監視和報告工具而已。 tooprotect 貴組織的身分識別，您可以設定在達到指定的風險層級時，自動回應 toodetected 問題的風險為基礎原則。 這些原則，除了 tooother 條件式存取 Azure Active Directory 和 EMS 所提供的控制項，可以自動封鎖或起始自動調整的修復動作，包括密碼重設以及強制多因素驗證。


#### <a name="identity-protection-capabilities"></a>Identity Protection 功能

**偵測弱點和風險帳戶：**  

* 提供自訂的建議 tooimprove 透過的弱點可能會反白顯示整體的安全性狀態
* 計算登入風險層級
* 計算使用者風險層級


**調查風險事件：**

* 傳送風險事件的通知
* 使用相關和內容資訊來調查風險事件
* 提供基本工作流程 tootrack 調查
* 讓您輕鬆存取 tooremediation 動作，例如密碼重設

**以風險為基礎的條件式存取原則：**

* 原則 toomitigate 風險登入所封鎖登入，或要求多重要素驗證挑戰。
* 原則 tooblock 或安全風險的使用者帳戶
* 原則 toorequire 使用者 tooregister 的多重要素驗證



## <a name="identity-protection-roles"></a>Identity Protection 角色

tooload 平衡 hello 管理活動的識別身分保護實作，您可以指派有數個角色。 Azure AD Identity Protection 支援 3 種目錄角色：

| 角色                         | 可以執行                          | 無法執行
| :--                          | ---                                |  ---   |
| 全域管理員         | 完整存取 tooIdentity 保護，內建的識別身分保護| |
| 安全性系統管理員       | 完整存取 tooIdentity 保護 | 將 Identity Protection 上架、重設使用者密碼 |
| 安全性讀取者              | 唯讀存取 tooIdentity 保護 | 讓 Identity Protection 上線、修復使用者、設定原則、重設密碼 |




如需詳細資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>偵測

### <a name="vulnerabilities"></a>弱點

Azure Active Directory Identity Protection 會分析您的組態，並偵測可能影響您使用者身份識別的弱點。 如需詳細資訊，請參閱 [Azure Active Directory Identity Protection 偵測到的弱點](active-directory-identityprotection-vulnerabilities.md)。

### <a name="risk-events"></a>風險事件

Azure Active Directory 使用彈性的機器學習演算法和啟發學習法 toodetect 可疑動作相關的 tooyour 使用者的身分識別。 hello 系統會建立每個偵測到可疑的動作記錄。 這些記錄又名風險事件。  
如需詳細資訊，請參閱 [Azure Active Directory風險事件](active-directory-identity-protection-risk-events.md)。


## <a name="investigation"></a>調查
此外，透過識別身分保護您旅途愉快通常會以 hello Identity Protection 儀表板啟動。

![補救](./media/active-directory-identityprotection/1000.png "補救")

hello 儀表板可讓您：

* 報告，例如 [標示有風險的使用者]、[風險事件] 和 [弱點]
* 設定，例如 hello 設定您**安全性原則**，**通知**和**註冊多重要素驗證**

它通常是您開始進行調查，是檢閱 hello 活動、 記錄和相關的 tooa 的風險事件 toodecide 是否補救或安全防護功能步驟所需的其他相關資訊的 hello 程序，和 hello 身分識別的方式遭到洩露，而且了解如何 hello 盜用身分識別使用。

您可以將繫結您調查活動 toohello[通知](active-directory-identityprotection-notifications.md)Azure Active Directory Protection 會將每個電子郵件傳送。

hello 下列各節提供更多詳細資料和相關的 tooan 調查的 hello 步驟。  


## <a name="risky-sign-ins"></a>有風險的登入

Azure Active Directory 會以即時和離線方式偵測[風險事件類型](active-directory-reporting-risk-events.md#risk-event-types)。 每個偵測到的登入之使用者的風險事件佔 tooa 呼叫有風險的登入的邏輯概念。 高風險的登入是可能不是執行 hello 合法的使用者帳戶擁有者的登入嘗試的指標。


### <a name="sign-in-risk-level"></a>登入風險層級

登入風險層級是 （高、 中或低） 的指示 hello 可能性 hello 合法的使用者帳戶擁有者未執行的登入嘗試。

### <a name="mitigating-sign-in-risk-events"></a>緩和登入風險事件

緩和措施是動作 toolimit hello 攻擊者 tooexploit 遭盜用身分識別或裝置的能力而不還原 hello 身分識別或裝置 tooa 安全狀態。 緩和措施無法解決先前 hello 身分識別或裝置相關聯的登入的風險事件。

toomitigate 危險的登入，您可以設定登入風險安全性 policicies。 您使用這些原則，請考慮 hello 使用者或登入 tooblock hello hello 風險層級有風險的登入或需要 hello 使用者 tooperform 多重要素驗證。 這些動作可能防止攻擊者利用身分識別遭竊的 toocause 損毀，而且可能會提供一些時間 toosecure hello 身分識別。

### <a name="sign-in-risk-security-policy"></a>登入風險安全性原則
登入風險原則是條件式存取原則，評估 hello 風險 tooa 特定登入，並根據預先定義的條件和規則的防護措施。

![登入風險原則](./media/active-directory-identityprotection/1014.png "登入風險原則")

Azure AD Identity Protection 可協助您管理讓您以 hello 緩和風險的登入的：

* 設定使用者和群組 hello 原則會套用至 hello:

    ![登入風險原則](./media/active-directory-identityprotection/1015.png "登入風險原則")
* 設定 hello 登入風險層級閾值 （低、 中或高），會觸發 hello 原則：

    ![登入風險原則](./media/active-directory-identityprotection/1016.png "登入風險原則")
* 設定 hello 控制項 toobe hello 原則觸發程序時，強制執行：  

    ![登入風險原則](./media/active-directory-identityprotection/1017.png "登入風險原則")
* 切換原則的 hello 狀態：

    ![MFA 註冊](./media/active-directory-identityprotection/403.png "MFA 註冊")
* 檢閱和評估 hello 變更的影響層面之後再啟動它：

    ![登入風險原則](./media/active-directory-identityprotection/1018.png "登入風險原則")

#### <a name="what-you-need-tooknow"></a>您的需要 tooknow
您可以設定登入風險安全性原則 toorequire multi-factor authentication:

![登入風險原則](./media/active-directory-identityprotection/1017.png "登入風險原則")

不過，基於安全性理由，這項設定只適用於已註冊 Multi-Factor Authentication 的使用者。 如果您尚未註冊多重要素驗證的使用者會滿足 hello 條件 toorequire 多重要素驗證，則會封鎖 hello 使用者。

最佳作法是，如果您想 toorequire 多重要素驗證的高風險登入，您應該：

1. 啟用 hello[多重要素驗證註冊原則](#multi-factor-authentication-registration-policy)hello 受影響的使用者。
2. 需要 hello 受影響使用者 toologin 中非有風險的工作階段 tooperform MFA 註冊

完成這些步驟可確保有風險的登入一定需要 Multi-Factor Authentication。

#### <a name="best-practices"></a>最佳作法
選擇**高**臨界值會減少 hello 原則，就會觸發和次數 hello 影響 toousers 降到最低。  

不過，它會排除**低**和**媒體**登入標示為從 hello 原則可能不會封鎖從高畫質視訊識別攻擊的風險。

當設定 hello 原則

* 排除不會 / 不能有 Multi-Factor Authentication 的使用者
* 排除使用者在其中啟用 hello 原則不是實際的地區設定 (例如沒有存取 toohelpdesk)
* 排除的使用者可能 toogenerate 大量 false 誤判 （開發人員、 安全性分析師）
* 在原則推出初期，或如果您必須盡量減少使用者所看到的挑戰，請使用 [高]  臨界值。
* 如果您的組織需要更高的安全性，請使用 [低]  臨界值。 選取 [低]  臨界值會帶來額外的使用者登入挑戰，並提高安全性。

大部分的組織是 tooconfigure 的規則，建議使用預設的 hello**媒體**閾值 toostrike 可用性和安全性之間取得平衡。

hello 登入風險原則是：

* 套用的 tooall 瀏覽器，並使用新式驗證的登入。
* 停用使用舊的安全性通訊協定不套用的 tooapplications hello hello 同盟 IDP，例如 ADFS Ws-trust 端點。

hello**風險事件**hello Identity Protection 主控台中的頁面會列出所有事件：

* 此原則已套用至
* 您可以檢閱 hello 活動，並判斷 hello 動作是否已適當

Hello 的概觀與相關的使用者經驗，請參閱：

* [有風險的登入復原](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [已封鎖有風險的登入](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [使用 Azure AD Identity Protection 時的登入體驗](active-directory-identityprotection-flows.md)  

**tooopen hello 相關的組態對話方塊**:

- 在 hello **Azure AD Identity Protection**刀鋒視窗中的，在 hello**設定**區段中，按一下**風險原則登入**。

    ![使用者風險原則](./media/active-directory-identityprotection/1014.png "使用者風險原則")



## <a name="users-flagged-for-risk"></a>標示有風險的使用者

所有作用中[風險事件](active-directory-identity-protection-risk-events.md)，偵測到由 Azure Active Directory 的使用者參與 tooa 呼叫使用者風險的邏輯概念。 標幟為有風險的使用者表示可能被盜用的使用者帳戶。

![標示有風險的使用者](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>使用者風險層級

使用者的風險層級是 （高、 中或低） 的指示 hello 可能性 hello 使用者的身分識別已遭洩漏。 它會根據計算 hello 與使用者的身分識別相關聯的使用者的風險事件。

hello 」 狀態的風險事件是**Active**或**Closed**。 只有風險事件**Active**參與 toohello 使用者風險層級計算。

hello 使用者風險層級的計算使用 hello 下列輸入：

* 作用中的風險事件影響 hello 使用者
* 這些事件的風險層級
* 是否已採取任何補救動作

![使用者風險](./media/active-directory-identityprotection/1031.png "使用者風險")

您可以使用 hello 使用者風險層級 toocreate 條件式存取原則來封鎖危險的使用者無法登入，或強制其 toosecurely 變更其密碼。

### <a name="closing-risk-events-manually"></a>手動關閉風險事件

在大部分情況下，所採取的修復動作，例如安全的密碼重設 tooautomatically 關閉的風險事件。 但是，這不一定都可行。  
這是，比方說，hello 情況下，當：

* 已刪除具有作用中風險事件的使用者
* 調查會顯示 hello 合法使用者已執行報告的風險事件

風險事件是因為**Active**參與 toohello 使用者風險計算，您可能必須手動關閉風險事件，以降低風險層級的 toomanually。  
期間的調查 hello 過程中，您可以選擇 tootake 任何這些動作 toochange hello 狀態的風險事件：

![動作](./media/active-directory-identityprotection/34.png "動作")

* **解決**-如果之後調查風險事件中，您採取適當的補救動作外部識別身分保護，而您認為應該關閉，標記為已解決的 hello 事件視為該 hello 風險事件。 已解決的事件會 hello 風險事件的狀態 tooClosed 然後 hello 風險事件將無法再參與 toouser 風險。
* **標示為誤判** - 在某些情況下，您可能會調查某個風險事件並發現該事件被誤標為有風險。 您可以協助減少 hello 次數這種方式是標示為誤判 hello 風險事件。 這將有助於 hello 機器學習演算法 tooimprove hello 分類的類似事件，在未來的 hello。 hello 誤判事件狀態太**Closed**它們將無法再參與 toouser 風險。
* **忽略**-如果您未採取任何修復動作後，但想 hello 風險事件 toobe hello 作用中的清單中移除，您可以將標記風險事件忽略 hello 事件狀態將會關閉。 已忽略的事件不會構成 toouser 風險。 這個選項只能用於不尋常的情況下。
* **重新啟用**-風險已手動關閉的事件 (藉由選擇**解決**，**誤判**，或**忽略**) 就可以重新啟動，設定 hello事件狀態太回**Active**。 已重新啟動的風險事件參與 toohello 使用者風險層級計算。 無法重新啟用透過補救 (例如重設安全的密碼) 關閉的風險事件。

**tooopen hello 相關的組態對話方塊**:

1. 在 hello **Azure AD Identity Protection**刀鋒視窗底下**調查**，按一下**風險事件**。

    ![手動密碼重設](./media/active-directory-identityprotection/1002.png "手動密碼重設")
2. 在 hello**風險事件**清單中，按一下有風險。

    ![手動密碼重設](./media/active-directory-identityprotection/1003.png "手動密碼重設")
3. 在 hello 風險刀鋒視窗中，以滑鼠右鍵按一下使用者。

    ![手動密碼重設](./media/active-directory-identityprotection/1004.png "手動密碼重設")

### <a name="closing-all-risk-events-for-a-user-manually"></a>手動關閉使用者的所有風險事件
而不是以手動方式關閉個別使用者的風險事件，Azure Active Directory 識別身分保護也提供您方法 tooclose 所有事件的使用者。

![動作](./media/active-directory-identityprotection/2222.png "動作")

當您按一下**解除所有事件**，所有事件都已都關閉且 hello 受影響的使用者不再有風險。

### <a name="remediating-user-risk-events"></a>補救使用者風險事件

修復是識別碼或裝置先前可疑或已知 toobe 危害動作 toosecure。 補救動作還原 hello 身分識別或裝置 tooa 安全的狀態，並解決先前 hello 身分識別或裝置相關聯的風險事件。

tooremediate 使用者風險事件，您可以：

* 手動執行安全的密碼重設 tooremediate 使用者風險事件
* 設定使用者風險安全性原則 toomitigate 或自動補救使用者風險事件
* 重新安裝映像 hello 感染的裝置  

#### <a name="manual-secure-password-reset"></a>手動重設安全密碼
安全密碼重設為有效的補救，對於許多的風險事件，並執行時，自動關閉這些風險事件，並重新計算 hello 使用者風險層級。 您可以使用 hello Identity Protection 儀表板 tooinitiate 危險的使用者重設密碼。

hello 相關的對話方塊提供兩個不同的方法 tooreset 密碼：

**重設密碼**-選取**需要 hello 使用者 tooreset 密碼**tooallow hello 使用者 tooself 復原，如果 hello 使用者已註冊的多重要素驗證。 Hello 使用者下一步 在登入期間，hello 使用者將會需要進行 multi-factor authentication 成功挑戰的 toosolve 並且然後、 強制 toochange hello 密碼。 無法使用，如果 hello 使用者帳戶還不是已註冊的多重要素驗證此選項。

**暫時密碼**-選取**產生暫時密碼**tooimmediately 失效 hello 現有密碼，並建立新的暫時密碼 hello 使用者。 傳送 hello 新暫時密碼 tooan 替代電子郵件地址 hello 使用者或 toohello 使用者的管理員。 因為 hello 密碼是暫時性的 hello 使用者將會提示的 toochange hello 密碼登入。

![原則](./media/active-directory-identityprotection/1005.png "原則")

**tooopen hello 相關的組態對話方塊**:

1. 在 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **使用者加上旗標的風險**。

    ![手動密碼重設](./media/active-directory-identityprotection/1006.png "手動密碼重設")
2. 從 [hello] 清單中的使用者，選取具有至少一個風險事件的使用者。

    ![手動密碼重設](./media/active-directory-identityprotection/1007.png "手動密碼重設")
3. 在 hello 使用者刀鋒視窗中，按一下 **重設密碼**。

    ![手動密碼重設](./media/active-directory-identityprotection/1008.png "手動密碼重設")

### <a name="user-risk-security-policy"></a>使用者風險安全性原則
使用者的風險安全性原則是條件式存取原則，評估 hello 風險層級 tooa 特定使用者，並根據預先定義的條件和規則的補救和補救動作。

![使用者風險原則](./media/active-directory-identityprotection/1009.png "使用者風險原則")

Azure AD Identity Protection 可協助您管理 hello 降低與補救的使用者，讓您標示為進行風險：

* 設定使用者和群組 hello 原則會套用至 hello:

    ![使用者風險原則](./media/active-directory-identityprotection/1010.png "使用者風險原則")
* 設定 hello 使用者風險層級閾值 （低、 中或高），會觸發 hello 原則：

    ![使用者風險原則](./media/active-directory-identityprotection/1011.png "使用者風險原則")
* 設定 hello 控制項 toobe hello 原則觸發程序時，強制執行：

    ![使用者風險原則](./media/active-directory-identityprotection/1012.png "使用者風險原則")
* 切換原則的 hello 狀態：

    ![使用者風險原則](./media/active-directory-identityprotection/403.png "MFA 註冊")
* 檢閱和評估 hello 變更的影響層面之後再啟動它：

    ![使用者風險原則](./media/active-directory-identityprotection/1013.png "使用者風險原則")

選擇**高**臨界值會減少 hello 原則，就會觸發和次數 hello 影響 toousers 降到最低。
不過，它會排除**低**和**媒體**標示為受到 hello 原則，可能不安全身分識別或裝置的使用者先前已可疑或已知 toobe 入侵。

當設定 hello 原則

* 排除的使用者可能 toogenerate 大量 false 誤判 （開發人員、 安全性分析師）
* 排除使用者在其中啟用 hello 原則不是實際的地區設定 (例如沒有存取 toohelpdesk)
* 在原則推出初期，或如果您必須盡量減少使用者所看到的挑戰，請使用 [高]  臨界值。
* 如果您的組織需要更高的安全性，請使用 [低]  臨界值。 選取 [低]  臨界值會帶來額外的使用者登入挑戰，並提高安全性。

大部分的組織是 tooconfigure 的規則，建議使用預設的 hello**媒體**閾值 toostrike 可用性和安全性之間取得平衡。

Hello 的概觀與相關的使用者經驗，請參閱：

* [遭到入侵的帳戶復原流程](active-directory-identityprotection-flows.md#compromised-account-recovery)。  
* [遭到入侵的帳戶封鎖流程](active-directory-identityprotection-flows.md#compromised-account-blocked)。  

**tooopen hello 相關的組態對話方塊**:

- 在 hello **Azure AD Identity Protection**刀鋒視窗中的，在 hello**設定**區段中，按一下**使用者風險原則**。

    ![使用者風險原則](./media/active-directory-identityprotection/1009.png "使用者風險原則")

### <a name="mitigating-user-risk-events"></a>緩和使用者風險事件
系統管理員可以根據 hello 風險層級設定使用者風險安全性原則 tooblock 使用者在登入。

封鎖登入：

* 防止 hello 產生 hello 受影響使用者的新使用者的風險事件
* 可讓系統管理員 toomanually 補救 hello 風險事件影響 hello 使用者的身分識別，並將它還原 tooa 安全的狀態



## <a name="multi-factor-authentication-registration-policy"></a>Multi-Factor Authentication 註冊原則
Azure 多因素驗證是確認您的身分的方法需要 hello 使用不只是使用者名稱和密碼。 它提供安全性 toouser 登入和交易的第二層。  
建議您要求對使用者登入進行 Azure Multi-Factor Authentication，因為它：

* 提供增強式驗證與一系列簡單的驗證選項
* 扮演一個關鍵角色準備您的組織 tooprotect 並從帳戶項目都會破壞復原

![使用者風險原則](./media/active-directory-identityprotection/1019.png "使用者風險原則")

如需詳細資訊，請參閱 [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection 可協助您管理 hello 推出多因素驗證註冊的設定原則，可讓您：

* 設定使用者和群組 hello 原則會套用至 hello:

    ![MFA 原則](./media/active-directory-identityprotection/1020.png "MFA 原則")
* Hello 原則觸發程序時，強制執行設定 hello 控制項 toobe::  

    ![MFA 原則](./media/active-directory-identityprotection/1021.png "MFA 原則")
* 切換原則的 hello 狀態：

    ![MFA 原則](./media/active-directory-identityprotection/403.png "MFA 原則")
* 檢視目前登錄狀態 hello:

    ![MFA 原則](./media/active-directory-identityprotection/1022.png "MFA 原則")

Hello 的概觀與相關的使用者經驗，請參閱：

* [Multi-Factor Authentication 註冊流程](active-directory-identityprotection-flows.md#multi-factor-authentication-registration)。  
* [使用 Azure AD Identity Protection 時的登入體驗](active-directory-identityprotection-flows.md)。  

**tooopen hello 相關的組態對話方塊**:

- 在 hello **Azure AD Identity Protection**刀鋒視窗中的，在 hello**設定**區段中，按一下**multi-factor authentication 註冊**。

    ![MFA 原則](./media/active-directory-identityprotection/1019.png "MFA 原則")

## <a name="next-steps"></a>後續步驟
* [第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [啟用 Azure Active Directory Identity Protection](active-directory-identityprotection-enable.md)

* [Azure Active Directory Identity Protection 偵測到的弱點](active-directory-identityprotection-vulnerabilities.md)

* [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)

* [Azure Active Directory Identity Protection 通知](active-directory-identityprotection-notifications.md)

* [Azure Active Directory Identity Protection 腳本](active-directory-identityprotection-playbook.md)

* [Azure Active Directory Identity Protection 詞彙](active-directory-identityprotection-glossary.md)

* [使用 Azure AD Identity Protection 時的登入體驗](active-directory-identityprotection-flows.md)

* [Azure Active Directory 識別身分保護-如何 toounblock 使用者](active-directory-identityprotection-unblock-howto.md)

* [開始使用 Azure Active Directory Identity Protection 和 Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
