---
title: "Azure AD SSPR 與密碼回寫 | Microsoft Docs"
description: "使用 Azure AD 和 Azure AD Connect toowriteback 密碼 tooon 內部部署目錄"
services: active-directory
keywords: "Active directory 密碼管理, 密碼管理, Azure AD 自助式密碼重設"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>密碼回寫概觀

密碼回寫可讓您的 Azure AD tooconfigure toowrite 密碼備份 tooyou 內部部署 Active Directory。 它 hello 需要 tooset 移除註冊和管理複雜的內部部署自助式密碼重設解決方案，並提供方便雲端式使用者 tooreset 其內部部署密碼隨時隨地都能。 密碼回寫是 [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) 的元件，可供目前的 [Azure Active Directory 版本](active-directory-editions.md)訂閱者啟用及使用。

密碼回寫中提供下列功能的 hello

* **零延遲的意見反應** - 密碼回寫是一項同步作業。 如果他們的密碼不符合原則，或已不能 toobe 重設或變更任何原因，會立即通知您的使用者。
* **支援使用 AD FS 或其他同盟技術的使用者密碼重設**-密碼回寫，只要 hello 同盟的使用者帳戶會同步處理到 Azure AD 租用戶，它們都是可以 toomanage 其在內部部署 AD從 hello 雲端的密碼。
* **支援使用的使用者密碼重設[密碼雜湊同步](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)** -時 hello 密碼重設服務偵測到啟用同步處理的使用者帳戶的密碼雜湊同步處理，所以重設兩個此帳戶在內部部署和雲端密碼同時。
* **支援密碼變更 hello 從存取面板和 Office 365** -當同盟或密碼同步處理使用者返回 toochange 到期或尚未到期的密碼，我們寫入這些密碼後 tooyour 本機 AD 環境。
* **回寫密碼時通知系統管理員重設他們從 hello Azure 入口網站**-為系統管理員重設使用者密碼在 hello 每當[Azure 入口網站](https://portal.azure.com)，如果該使用者為同盟或密碼同步，我們會隨即制定 hello在您的本機 AD，以及會選取密碼 hello 系統管理員。 這是目前不支援在 hello Office 管理入口網站中。
* **會強制執行您內部部署 AD 密碼原則**-當使用者重設其密碼，我們確定它符合您內部部署 AD 原則，再認可 toothat 目錄。 這當中包括歷程記錄、複雜度、使用期限、密碼篩選和您在本機 AD 中定義的任何其他密碼限制。
* **不需要任何輸入的防火牆規則**-密碼回寫使用 Azure 服務匯流排轉送當做基礎的通訊通道，這表示，您不需要 tooopen 任何輸入連接埠此功能 toowork 在防火牆上。
* **不支援存在於內部部署 Active Directory 中受保護群組內的使用者帳戶** - 如需受保護群組的詳細資訊，請參閱 [Active Directory 中受保護的帳戶和群組](https://technet.microsoft.com/library/dn535499.aspx)。

## <a name="how-password-writeback-works"></a>密碼回寫的運作方式

當同盟或密碼雜湊同步處理使用者 tooreset 或變更其密碼的 hello 雲端發生 hello 下列情況：

1. 我們會檢查 toosee 有何種密碼 hello 使用者。
    * 如果我們看到 hello 密碼由內部部署管理
        * 我們會檢查如果 hello 回寫服務已啟動且執行中，如果是，我們讓 hello 使用者繼續
        * 如果 hello 回寫服務不是往上，我們告訴 hello 使用者，他們無法重設密碼現在
2. 接下來，hello 使用者傳送嗨適當的驗證閘道，並達到 hello 重設密碼畫面。
3. hello 使用者選取新密碼，並確認它。
4. 按下提交，我們已在 hello 回寫設定程序期間建立的對稱金鑰加密 hello 純文字密碼。
5. 加密 hello 密碼之後, 我們包含在透過 HTTPS 通道 tooyour 租用戶專屬的服務匯流排轉送 （我們也為您設定 hello 回寫設定程序） 送裝載。 此轉送受到只有您的內部部署安裝才會知道的隨機產生密碼所保護。
6. 一旦 hello 訊息抵達服務匯流排，hello 密碼重設端點自動喚醒並看到它有暫止的重設要求。
7. hello 服務接著會尋找 hello 使用者有問題使用 hello 雲端錨點屬性。 針對此查閱 toosucceed:

    * hello 使用者物件必須存在於 AD 連接器空間 hello
    * hello 使用者物件必須是連結的 toohello 相對應的 MV 物件
    * hello 使用者物件必須是連結的 toohello 相對應的 AAD 連接器物件。
    * hello 連結從 AD 連接器物件 tooMV 必須有 hello 同步處理規則`Microsoft.InfromADUserAccountEnabled.xxx`hello 連結。 <br> <br>
    當 hello 呼叫會來自 hello 雲端時，hello 同步處理引擎會使用 hello cloudAnchor 屬性 toolook hello AAD 連接器空間物件，跟 hello 連結後 toohello MV 物件，然後依照 [hello 連結後 toohello AD 物件。 因為可能有多個 AD 物件 （多樹系） 的相同使用者，hello 同步引擎依賴 hello hello`Microsoft.InfromADUserAccountEnabled.xxx`連結 toopick hello 更正其中一個。

    > [!Note]
    > 因為此邏輯，而 Azure AD Connect 必須能夠以 hello PDC 模擬器的密碼回寫 toowork toocommunicate。 如果您在此手動需要 tooenable，您可以以滑鼠右鍵按一下 hello 連接 Azure AD Connect toohello PDC 模擬器**屬性**的 hello Active Directory 同步處理連接器，然後選取**設定目錄分割**。 從該處，尋找 hello**網域控制站連線設定**區段，並檢查 hello 方塊**只使用慣用的網域控制站**。 即使 hello 慣用 DC 不是 PDC 模擬器，Azure AD Connect 會嘗試 tooconnect toohello PDC 密碼回寫。

8. 一旦找到 hello 使用者帳戶，我們會嘗試直接在 hello 適當 AD 樹系中的 tooreset hello 密碼。
9. 如果 hello 密碼設定作業成功，我們會告訴 hello 使用者，其密碼已經變更集。
    > [!NOTE]
    > 萬一 hello hello 使用者的密碼已同步處理的 tooAzure AD 時使用的密碼同步處理，沒有機會 hello 在內部部署密碼原則是比 hello 雲端密碼原則更弱。 在此情況下，仍強制任何 hello 在內部部署原則，並改為允許的密碼雜湊同步處理 toosynchronize hello 雜湊的密碼。 這可確保您在內部部署的原則會強制執行的 hello 雲端，不論如果您使用密碼同步或同盟 tooprovide 單一登入。

10. 如果 hello 密碼設定作業失敗，我們會傳回 hello toohello 使用者時發生錯誤，並且讓他們再試一次。
    * hello 作業可能會因為 hello 下列失敗
        * hello 服務已關閉
        * 選取這些 hello 密碼不符合公司原則
        * 我們找不到 hello 本機 AD 中的 hello 使用者

    我們有許多這類情況的訊息，告知 hello 使用者他們可以執行特定 tooresolve hello 問題。

## <a name="configuring-password-writeback"></a>設定密碼回寫

我們建議您使用 hello 自動更新功能[Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)如果您想 toouse 密碼回寫。

DirSync 和 Azure AD 同步作業已不再支援的方法，啟用密碼回寫 hello 發行項的[從 DirSync 和 Azure AD Sync 升級](connect/active-directory-aadconnect-dirsync-deprecated.md)已與您轉換的詳細資訊 toohelp。

hello 下列步驟假設您已經使用 hello 您環境中設定 Azure AD Connect [Express](./connect/active-directory-aadconnect-get-started-express.md)或[自訂](./connect/active-directory-aadconnect-get-started-custom.md)設定。

1. tooconfigure 並啟用密碼回寫登入 tooyour Azure AD Connect 的伺服器，然後啟動 hello **Azure AD Connect**組態精靈。
2. 在 [hello 歡迎使用] 畫面上按一下**設定**。
3. 在 [hello 其他工作畫面上按一下**自訂同步處理選項**，然後選擇 [**下一步**。
4. Hello 連接 tooAzure AD 畫面上輸入全域系統管理員認證，然後選擇**下一步**。
5. Hello 上您的目錄和網域連線，而且您可以選擇篩選螢幕的 OU**下一步**。
6. 在 hello 選擇性功能] 畫面上核取 hello 方塊旁太**密碼回寫**按一下**下一步**。
   ![在 Azure AD Connect 中啟用密碼回寫][Writeback]
7. Hello 準備 tooconfigure 畫面上按一下 [**設定**並等候 hello 程序 toocomplete。
8. 當您看到「設定完成」時，您可以按一下 **[結束]**

## <a name="licensing-requirements-for-password-writeback"></a>密碼回寫的授權需求

如需有關授權，請參閱 hello 主題[授權所需的密碼回寫](active-directory-passwords-licensing.md#licenses-required-for-password-writeback)或 hello 下列站台

* [Azure Active Directory 價格網站](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>密碼回寫支援的內部部署驗證模式

密碼回寫適用於下列使用者的密碼類型 hello:

* **僅限雲端的使用者**︰密碼回寫不適用於這種情況，因為沒有內部部署密碼
* **已同步處理密碼的使用者**︰支援密碼回寫
* **同盟使用者**︰支援密碼回寫
* **傳遞驗證使用者**︰支援密碼回寫

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>密碼回寫支援的使用者和系統管理員作業

密碼會回寫，在下列情況下的所有 hello:

* **支援的使用者作業**
  * 任何使用者自助式自願變更密碼作業
  * 任何使用者自助式強制變更密碼作業 (例如密碼到期)
  * 任何使用者自助式密碼重設源自 hello[密碼重設入口網站](https://passwordreset.microsoftonline.com)
* **支援的系統管理員作業**
  * 任何系統管理員自助式自願變更密碼作業
  * 任何系統管理員自助式強制變更密碼作業 (例如密碼到期)
  * 任何系統管理員自助式密碼重設源自 hello[密碼重設入口網站](https://passwordreset.microsoftonline.com)
  * 任何從 hello 重設的系統管理員起始使用者密碼[Azure 傳統入口網站](https://manage.windowsazure.com)
  * 任何從 hello 重設的系統管理員起始使用者密碼[Azure 入口網站](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>密碼回寫不支援的使用者和系統管理員作業

密碼是**不**寫入中任何 hello 下列情況：

* **不支援的使用者作業**
  * 重設自己的密碼使用 PowerShell v1、 v2、 或 hello Azure AD Graph API 的所有使用者
* **不支援的系統管理員作業**
  * 任何從 hello 重設的系統管理員起始使用者密碼[Office 管理入口網站](https://portal.office.com)
  * 任何系統管理員起始使用者密碼從 PowerShell v1、 v2、 重設或 hello Azure AD Graph API

當我們使用 tooremove 這些限制時，我們不需要特定的時間軸，我們可以在尚未共用。

## <a name="password-writeback-security-model"></a>密碼回寫的安全性模型

密碼回寫是一項極為安全的服務。  您的資訊保護的 tooensure，我們會啟用如下所述的 4 層的安全性模型。

* **租用戶特定的服務匯流排轉送**
  * 當您設定 hello 服務時，我們會設定租用戶特定服務匯流排轉送由隨機產生的強式密碼，Microsoft 也無法存取受保護。
* **受到鎖定的密碼編譯強式密碼加密金鑰**
  * 建立 hello service bus 轉送之後，我們會建立我們使用 tooencrypt hello 密碼就會自動收到 hello 線上強式對稱金鑰。 此機碼只有位於您公司的密碼存放區在 hello 雲端中，這是大量鎖定且稽核，就像在 hello 目錄中的任何密碼。
* **業界標準 TLS**
  1. 當密碼重設或變更作業發生 hello 雲端中，我們對 hello 純文字密碼，並以您的公開金鑰加密它。
  2. 我們然後將之放在 HTTPS 訊息，透過使用 Microsoft 的 SSL 憑證 tooyour service bus 轉送加密通道傳送。
  3. Hello 訊息抵達服務匯流排，在內部部署代理程式喚醒時設定，並驗證之後 tooService 匯流排使用 hello 先前產生的強式密碼。
  4. 在內部部署代理程式收取 hello 加密訊息，它使用我們產生 hello 私密金鑰解密。
  5. 在內部部署代理程式接著會嘗試透過 AD DS SetPassword API hello tooset hello 密碼。
     * 這個步驟可讓我們 tooenforce AD 內部部署密碼原則 （複雜性、 存在時間、 記錄、 篩選等） hello 雲端中。
* **訊息到期原則** 
  * 如果 Service Bus 中的 hello 訊息位於，因為在內部部署服務已關閉，它會將階段逾時，並在幾分鐘的時間 tooincrease 安全性更進一步之後移除。

### <a name="password-writeback-encryption-details"></a>密碼回寫的加密詳細資料

使用者送出，才能到達您在內部部署環境、 tooensure 最大的服務的可靠性和安全性之後，密碼重設要求會經過 hello 加密步驟說明如下。

* **步驟 1-使用 2048年位元 RSA 金鑰的密碼加密**-當使用者提交密碼 toobe 寫回 tooon 內部部署，第一個，hello 提交的密碼本身使用 2048年位元 RSA 金鑰加密。
* **步驟 2-封裝層級加密使用 AES GCM** -然後 hello 整個封裝 （密碼 + 必要的中繼資料） 會使用 AES GCM 進行加密。 這可防止任何人都直接存取 toohello 基礎 ServiceBus 通道檢視/竄改 hello 內容。
* **步驟 3-所有通訊，就會都發生 5060，TLS / SSL** -所有與 ServiceBus hello 通訊會發生在 SSL/TLS 通道。 這可以保護 hello 內容來自未經授權的第 3 個合作對象。
* **自動金鑰變換每六個月**自動每 6 月或每次密碼回寫是停用 / 重新啟用 Azure AD Connect，我們變換所有這些金鑰 tooensure 最大的服務安全性和安全。

### <a name="password-writeback-bandwidth-usage"></a>密碼回寫頻寬使用量

密碼回寫是一種低頻寬的服務，會傳送要求回 toohello 在內部部署代理程式只能在下列情況下的 hello:

1. 兩個傳送的訊息時啟用或停用透過 Azure AD Connect 的 hello 功能。
2. 一則訊息會傳送一次每隔五分鐘做為服務活動訊號，只要 hello 服務正在執行。
3. 每次提交新密碼時會傳送兩則訊息
    * 第一則訊息，以要求 tooperform hello 作業
    * 第二個訊息，其中包含 hello hello 作業結果，會傳送 hello 下列情況：
        * 每次在使用者自助式密碼重設期間提交新密碼時。
        * 每次在使用者密碼變更作業期間提交新密碼時。
        * 每次在系統管理員起始使用者密碼重設 （從 hello Azure 管理員入口網站只） 期間，送出新密碼。

#### <a name="message-size-and-bandwidth-considerations"></a>訊息大小和頻寬考量

hello hello 訊息上面所述的每個的大小通常是在 1 kb，甚至在極端負載下，hello 密碼回寫服務本身會耗用幾秒千位元的頻寬。 因為每個訊息會傳送即時，所需的密碼更新作業時，才而且 hello 訊息大小很小，因為 hello 頻寬使用量 hello 回寫功能的有效地是太小 toohave 任何實數明顯的影響。

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "在 Azure AD Connect 中啟用密碼回寫"
