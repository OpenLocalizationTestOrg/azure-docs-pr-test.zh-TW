---
title: "深入探討︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設深入探討"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Azure AD 中的自助式密碼重設深入探討

SSPR 的運作方式 該選項什麼 hello 介面中？ 繼續閱讀 toofind 深入了解 Azure AD 自助式密碼重設。

## <a name="how-does-hello-password-reset-portal-work"></a>如何 hello 密碼重設入口網站的工作

當使用者巡覽 toohello 密碼重設入口網站時，工作流程會開始 toodetermine:

   * 如何當地語系化 hello 頁面？
   * 是有效的 hello 使用者帳戶？
   * Hello 使用者並屬於組織為何？
   * 其中被管理 hello 使用者的密碼嗎？
   * 是 hello 使用者授權的 toouse hello 功能？


閱讀下列有關 hello hello 密碼重設頁面背後的邏輯 toolearn 的 hello 步驟。

1. 使用者按一下 hello 無法存取您帳戶的連結，或直接進入太[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com)。
2. 基礎上 hello 瀏覽器地區設定 hello hello 適當的語言呈現體驗。 hello 密碼重設體驗已當地語系化成 Office 365 支援 hello 相同的語言。
3. 使用者輸入使用者識別碼並通過文字驗證。
4. Azure AD 會驗證 hello 使用者是否能 toouse 執行 hello 下列這項功能：
   * 會檢查該 hello 使用者已啟用這項功能並指派的 Azure AD 授權。
     * Hello 使用者並沒有啟用這項功能或將授權指派，hello 使用者是否要求 toocontact 其系統管理員 tooreset 他們的密碼。
   * 會檢查該 hello 使用者已在系統管理員原則根據帳戶中定義的 hello 正確驗證題目資料。
     * 如果原則要求只有一個挑戰，則會確保該 hello 使用者已定義至少一個 hello hello 系統管理員原則啟用的驗證題目 hello 適當的資料。
       * 如果 hello 使用者未設定，然後 hello 使用者是建議使用的 toocontact 其系統管理員 tooreset 他們的密碼。
     * 如果 hello 原則需要兩個驗證題目，則會確保該 hello 使用者已針對至少兩個 hello hello 系統管理員原則啟用的驗證題目，定義 hello 適當資料。
       * 如果未設定 hello 使用者，則我們 hello 使用者是建議使用的 toocontact 其系統管理員 tooreset 他們的密碼。
   * 檢查是否 hello 使用者的密碼由內部部署管理 （同盟或密碼雜湊同步處理）。
     * 如果已部署回寫 hello 使用者的密碼由內部部署管理，hello 使用者允許 tooproceed tooauthenticate 和重設其密碼。
     * 如果未部署回寫，而且 hello 使用者的密碼由內部部署管理，則 hello 使用者是要求其系統管理員 tooreset toocontact 他們的密碼。
5. 如果它由決定該 hello 使用者 toosuccessfully 重設其密碼，然後會引導 hello 使用者 hello 重設程序完成。

## <a name="authentication-methods"></a>驗證方法

如果已啟用自助式密碼重設 (SSPR)，您必須選取至少一個 hello 下列驗證方法的選項。 我們強烈建議選擇至少兩個驗證方法，您的使用者才有更大的彈性。

* 電子郵件
* 行動電話
* 辦公室電話
* 安全性問題

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>哪些欄位用於 hello 目錄中驗證資料

* 辦公室電話對應 tooOffice 電話
    * 使用者會無法 tooset 這欄位本身必須由系統管理員
* 行動電話對應 tooeither （不可見） 的驗證電話或行動電話 （可見）
    * hello 服務驗證電話會首先尋找，然後就會回到 tooMobile 電話如果不存在
* 替代電子郵件地址對應 tooeither 驗證電子郵件 （不可見） 或替代電子郵件
    * hello 服務驗證電子郵件的第一次，看起來則會失敗後 tooAlternate 電子郵件

根據預設，只有 hello 雲端屬性辦公室電話和行動電話會同步處理 tooyour 雲端目錄，從您的內部部署目錄的驗證資料。

使用者可以只重設其密碼，才有 hello 驗證方法中的資料該 hello 系統管理員已啟用，且要求。

如果使用者不想其行動電話號碼 toobe 可見 hello 目錄中，但還是希望像 toouse 它密碼重設，系統管理員應填入 hello 目錄中，然後填入 hello 使用者應該其**驗證電話**屬性透過 hello[密碼重設註冊入口網站](http://aka.ms/ssprsetup)。 系統管理員可以查看這項資訊在 hello 使用者設定檔，但它不在其他位置發行。 如果 Azure 系統管理員帳戶註冊其驗證電話號碼時，它會擴展到 hello 行動電話欄位，同時會顯示。

### <a name="number-of-authentication-methods-required"></a>必要驗證方法數目

此選項會決定 hello 的使用者必須通過 tooreset hello 可用的驗證方法數目下限或解除鎖定其密碼，而且可以設定 tooeither 1 或 2。

使用者可以選擇 toosupply 個驗證方法，如果有啟用 hello 系統管理員。

如果使用者沒有已註冊的 hello 最小必要方法，就會看到錯誤頁面，會將他們導向 toorequest 管理員 tooreset 他們的密碼。

### <a name="how-secure-are-my-security-questions"></a>我的安全性問題有多安全

如果您使用安全性問題，我們建議它們使用另一個方法為它們可能會比其他方法更不安全因為有些人可能知道 hello 答案 tooanother 使用者問題。

> [!NOTE] 
> 安全性問題 hello 目錄中使用者物件上儲存非公開且安全的方式，而且可以只由使用者回答登錄期間。 沒有方法可讓系統管理員 tooread 或修改使用者問題或回答。
>

### <a name="security-question-localization"></a>安全性問題當地語系化

所有預先定義的問題，請遵循已當地語系化為 hello 整組 hello 使用者的瀏覽器地區設定為基礎的 Office 365 語言。

* 您在哪個城市遇見第一個配偶/伴侶？
* 您的父母在哪個城市相遇？
* 您最親近的手足住在哪個城市？
* 您的父親在哪個城市出生？
* 您的第一份工作是在哪個城市？
* 您的母親在哪個城市出生？
* 您在哪個城市渡過 2000 年的新年？
* 什麼是最喜愛的老師在高 hello 姓氏 * 學校？
* 什麼是您套用的入學的 hello 名稱 toobut 不參加？
* Hello 地方您您第一場婚宴 hello 名稱是什麼？
* 您父親的中間名是什麼？
* 您最愛的食物是什麼？
* 您外婆的姓名為何？
* 您母親的中間名是什麼？
* 您最年長手足的生日月份和年度為何？ (例如 1985 年 11 月)
* 您最年長手足的中間名是什麼？
* 您祖父的姓名為何？
* 您最年幼手足的中間名稱是什麼？
* 您六年級時就讀哪間學校？
* 什麼是第一次的 hello 名字童年最佳朋友的？
* 什麼是第一次的 hello 名字您的第一個配偶？
* 您最喜愛的小學老師的 hello 姓是什麼？
* 第一個汽車或機車的 hello 廠牌和型號是什麼？
* Hello 您參加第一所學校 hello 名字是什麼？
* 您已出生 hello 醫院 hello 名是什麼？
* Hello 街道的第一個兒時家用 hello 名字是什麼？
* 您的童年英雄的 hello 名字是什麼？
* 最愛娃娃 hello 名字是什麼？
* 您第一隻寵物的 hello 名字是什麼？
* 您童年時期的綽號是什麼？
* 您中學最喜愛的運動是什麼？
* 您的第一份工作是什麼？
* 什麼是 hello 您兒時電話號碼的末 4 碼？
* 長大時，所希望 toobe 時小時候？
* Hello 您遇最知名的人物是誰？

### <a name="custom-security-questions"></a>自訂安全性問題

自訂安全性問題不會針對不同的地區設定進行當地語系化。 所有自訂問題會顯示在 [hello 會在 hello 系統管理使用者介面中輸入，即使 hello 使用者的瀏覽器地區設定是不同的語言相同。 如果您需要當地語系化的問題，請使用 hello 預先定義的問題。

hello 與自訂安全性問題的最大長度為 200 個字元。

### <a name="security-question-requirements"></a>安全性問題需求

* 答案字元限制下限為 3 個字元。
* 答案字元限制上限為 40 個字元。
* 使用者不會回答相同問題一次以上的 hello
* 使用者可能不會提供 hello 相同回答 toomore 比一個問題
* 任何字元集可能會使用的 toodefine 問題和答案包括 Unicode 字元
* hello 定義的問題數必須大於或等於 toohello 問題需要 tooregister 數目

## <a name="registration"></a>註冊

### <a name="require-users-tooregister-when-signing-in"></a>在登入時，要求使用者 tooregister

啟用此選項需要使用者啟用密碼重設 toocomplete hello 密碼重設註冊登入時使用中的 Azure AD toosign 遵循類似 tooapplications:

* Office 365
* Azure 入口網站
* 存取面板
* 同盟應用程式
* 使用 Azure AD 自訂應用程式

停用這項功能仍然可讓使用者 toomanually 註冊他們的連絡資訊造訪[http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)或按一下 hello**註冊密碼重設**hello 底下的連結hello 存取面板中的設定檔索引標籤。

> [!NOTE]
> 使用者可以按一下 [取消] 5d; 或關閉 hello 視窗關閉 hello 密碼重設註冊入口網站，但每次完成註冊之後才登入時提示。
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>數天之後使用者, 詢問 tooreconfirm 其驗證資訊

此選項可決定 hello 期間設定和 reconfirming 驗證資訊之間的時間和才可使用啟用 hello**在登入時，要求使用者 tooregister**選項。

有效值為 0-730 天 0 表示絕對不會要求使用者 tooreconfirm 其驗證資訊

## <a name="notifications"></a>通知

### <a name="notify-users-on-password-resets"></a>通知使用者密碼重設

如果此選項設定 tooyes，正在重設其密碼的 hello 使用者接收電子郵件通知他們的已變更其密碼透過 hello SSPR 入口 tootheir 主要和備用電子郵件地址檔案在 Azure AD 中。 沒有人會接獲此重設事件的通知。

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>當其他系統管理員重設其密碼時通知所有系統管理員

如果此選項設定 tooyes，則**所有系統管理員**接收通知其他系統管理員已經使用 SSPR 密碼的 Azure AD 中的檔案上的電子郵件 tootheir 主要電子郵件地址。

範例︰環境中有四個系統管理員。 系統管理員 "A" 使用 SSPR 重設其密碼。 系統管理員 B、C 和 D 收到一封電子郵件，警示他們發生此狀況。

## <a name="on-premises-integration"></a>內部部署整合

如果您已安裝、設定及啟用 Azure AD Connect，您會有其他的內部部署整合選項。

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>回寫密碼 tooyour 在內部部署目錄

控制啟用此目錄密碼回寫，而且如果回寫上，指出 hello hello 在內部部署回寫服務狀態。 這非常有用，如果您想 tootemporarily 停用 hello 密碼回寫，而不需重新設定 Azure AD Connect。

* 如果 hello 切換是集 tooyes 回寫會啟用，與同盟和密碼雜湊同步處理的使用者都能 tooreset 他們的密碼。
* 如果 hello 切換是集 toono 回寫會停用，與同盟和密碼雜湊同步處理使用者並不會無法 tooreset 他們的密碼。

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>允許使用者 toounlock 帳戶，而不重設其密碼

指定造訪 hello 密碼重設入口網站的使用者應該是給定的 hello 選項 toounlock 其內部部署 Active Directory 帳戶，而不重設其密碼。 根據預設，Azure AD 會一律解除鎖定帳戶執行密碼重設時，此設定可讓您 tooseparate 這兩項作業。 

* 如果設定太"yes"，則使用者將會是給定的 hello 選項 tooreset 其密碼和解除鎖定 hello 帳戶或 toounlock 而不重設 hello 密碼。
* 如果設定太"no"，然後使用者才能夠 tooperform 結合的密碼重設和帳戶解除鎖定作業。

## <a name="network-requirements"></a>網路需求

### <a name="firewall-rules"></a>防火牆規則

[Microsoft Office URL 和 IP 位址清單](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Azure AD Connect 1.1.443.0 版和更新版本，您需要的輸出 HTTPS 存取 toohello 下列
* passwordreset.microsoftonline.com
* servicebus.windows.net

對於更細微的存取，您可以找到 hello 更新 Microsoft Azure Datacenter IP 範圍，更新每個星期三並放入效果 hello 下列清單星期一[這裡](https://www.microsoft.com/download/details.aspx?id=41653)。

### <a name="idle-connection-timeouts"></a>閒置連線逾時

hello Azure AD Connect 工具會傳送定期 ping/keepalives tooServiceBus 端點 tooensure hello 連線保持運作。 應該 hello 工具偵測到太多連線會遭到刪除，它會自動增加 ping toohello 端點的 hello 頻率。 hello 最低 'ping 時間間隔' 卸除 toois 1 ping 每隔 60 秒，不過，我們強烈建議 proxy/防火牆允許閒置連接 toopersist，至少 2-3 分鐘。 *針對較舊版本，建議 4 分鐘以上。

## <a name="active-directory-permissions"></a>Active Directory 權限

hello hello Azure AD Connect 公用程式中指定的帳戶必須具有重設密碼、 變更密碼、 lockoutTime，寫入權限和寫入權限 pwdLastSet，擴充權限的任一個 hello 根物件**每個網域**該樹系中**或**hello 使用者 Ou 上您想 toobe SSPR 範圍中的。

如果您不確定上述何種帳戶 hello 參考、 開啟 hello Azure Active Directory Connect 組態 UI，然後按一下 hello 檢視目前的組態選項。 hello 帳戶，您需要 tooadd 權限 toois 列在 [同步處理目錄]

設定這些權限允許該樹系中的 hello MA 服務帳戶的每個樹系 toomanage 密碼的使用者帳戶。 **如果您並未 tooassign 這些權限，然後，即使回寫 toobe 正確設定，使用者嘗試 toomanage hello 雲端從其內部部署密碼時，就會發生錯誤。**

> [!NOTE]
> 它可能會佔用 tooan 小時或更多您的目錄中的這些權限 tooreplicate tooall 物件。
>

tooset hello 的密碼回寫 toooccur 的適當權限

1. 使用具有 hello 適當網域管理權限的帳戶開啟 [Active Directory 使用者和電腦
2. 從 hello 檢視] 功能表中，確定已開啟 [進階功能
3. 在 hello 左面板中，以滑鼠右鍵按一下代表 hello hello 網域根目錄的 hello 物件，然後選擇屬性
    * Hello 安全性] 索引標籤
    * 然後按一下 [進階]。
4. Hello 權限] 索引標籤中，按一下 [新增]
5. 挑選 hello 太 （從 Azure AD Connect 的安裝程式） 會被套用權限的帳戶
6. 在 [hello 適用於 toodrop 下拉方塊中選取 [子系的使用者物件
7. 權限] 底下的核取 hello 下列 hello 方塊
    * 未過期密碼
    * 重設密碼
    * 變更密碼
    * 寫入 lockoutTime
    * 寫入 pwdLastSet
8. 按一下 tooapply 套用/確定]，再結束任何開啟的對話方塊。

## <a name="how-does-password-reset-work-for-b2b-users"></a>B2B 使用者的密碼重設運作方式
所有 B2B 組態完全支援密碼重設和變更。  閱讀下列 hello 三個明確 B2B 案例支援密碼重設。

1. **從現有的 Azure AD 租用戶與夥伴組織的使用者**-如果您使用合作的 hello 組織有現有的 Azure AD 租用戶，我們**採用該租用戶中已啟用的任何密碼重設原則**。 中的密碼重設 toowork、 hello 夥伴組織僅需要 toomake 確定已啟用 Azure AD SSPR，也就是對 O365 的客戶不另收費用，而且可以啟用依照下列步驟 hello 我們[開始使用密碼管理](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords)指南。
2. **使用者註冊使用[自助式註冊](active-directory-self-service-signup.md)** -如果您以合作的 hello 組織使用 hello[自助式註冊](active-directory-self-service-signup.md)功能 tooget 入租用戶，我們會讓它們具有重設hello 電子郵件註冊它們。
3. **B2B 使用者**-使用 hello 新建立的任何新 B2B 使用者[Azure AD B2B 功能](active-directory-b2b-what-is-azure-ad-b2b.md)也會無法 tooreset hello 其註冊過程 hello 邀請的電子郵件與密碼。

tootest 與其中一個夥伴的使用者，請移 toohttp://passwordreset.microsoftonline.com。 只要他們定義了替代電子郵件或驗證電子郵件，密碼重設就會如預期般運作。

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR

