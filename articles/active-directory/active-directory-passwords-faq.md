---
title: "常見問題集︰Azure AD SSPR | Microsoft Docs"
description: "有關 Azure AD 自助式密碼重設的常見問題集。"
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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>密碼管理常見問題集

hello 下列是一些常見問題的一切相關 toopassword 重設。

如果您有關於 Azure AD 的一般問題和自助式密碼重設，未在此處找到答案，您可以要求 hello 社群協助在 hello [Azure Ad 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)。 Hello 社群的成員包括工程師，產品經理、 professional，Mvp 和夥伴 IT 專業人員。

此常見問題集分成下列各節的 hello:

* [**密碼重設註冊的相關問題**](#password-reset-registration)
* [**密碼重設的相關問題**](#password-reset)
* [**密碼變更的相關問題**](#password-change)
* [**密碼管理報告的相關問題**](#password-management-reports)
* [**密碼回寫的相關問題**](#password-writeback)

## <a name="password-reset-registration"></a>密碼重設註冊
* **問：我的使用者是否可以註冊自己的密碼重設資料？**

  > **答：**是的只要已啟用密碼重設，且他們已獲得授權，他們可以移 toohello 密碼重設註冊入口網站則位於 http://aka.ms/ssprsetup tooregister 其驗證資訊。 按一下 hello 設定檔 索引標籤，然後按一下 hello 註冊密碼重設選項移 toohello 存取面板 http://myapps.microsoft.com，也可以註冊使用者。
  >
  >
* **問：我是否可以代表我的使用者定義密碼重設資料？**

  > **答：**是，您可以使用 Azure AD Connect，PowerShell hello [Azure 入口網站](https://portal.azure.com)，或 hello Office 管理入口網站。 如需詳細資訊，請參閱 hello 文章[使用 Azure AD 自助式密碼重設資料](active-directory-passwords-data.md)。
  >
  >
* **問：我是否可以從內部部署環境同步處理安全性問題的資料？**

  > **答：** 目前無法這麼做。
  >
  >
* **問：我的使用者是否可以用讓其他使用者看不到資料的方式來註冊該資料？**

  > **答：**是的當使用者註冊使用 hello 密碼重設註冊入口網站儲存到，才會顯示由全域管理員和 hello 使用者的私用的驗證欄位的資料。
    >
    > [!NOTE]
    > 如果**Azure 系統管理員帳戶**註冊它也會填入 hello 行動電話欄位，並會顯示其驗證電話號碼。
    >
  >
  >
* **問： 我的使用者沒有 toobe 註冊才能使用密碼重設嗎？**

  > **答：**否，如果您定義足夠驗證的資訊代表它們時，使用者不需要 tooregister。 密碼重設運作，只要您已正確格式化 hello hello 目錄中的適當欄位中儲存的資料。
  >
  >
* **問： 可以同步處理或代表使用者設定 hello 驗證電話、 驗證電子郵件或 備用驗證電話欄位？**

  > **答：** 目前無法這麼做。
  >
  >
* **問： 如何 hello 註冊入口網站知道哪些選項 tooshow 我的使用者？**

  > **答：** hello 密碼重設註冊入口網站，只顯示 hello 使用者啟用的選項。 下 hello 您目錄中的 設定 索引標籤的 使用者密碼重設原則 > 一節找到這些選項。比方說，這表示，如果尚未啟用安全性問題，使用者便不能 tooregister 該選項。
  >
  >
* **問：使用者何時會被視為已註冊？**

  > **答：**使用者已註冊 SSPR 時完成註冊會視為至少 hello**方法需要 tooreset 數目**您已設定在 hello [Azure 入口網站](https://portal.azure.com)。
  >
  >
## <a name="password-reset"></a>密碼重設
* **問： 要我等候 tooreceive 電子郵件、 簡訊或電話，從密碼重設？**

  > **答：**電子郵件、 簡訊和電話應該與 hello 一般案例 5-20 秒到達在一分鐘。
    >如果您沒有在此時段中收到 hello 通知：
        > * 檢查您的垃圾郵件資料夾。
        > * 核取 hello 號碼或電子郵件連絡是您預期一個 hello。
        > * 請檢查 hello 目錄中的 hello 驗證資料已正確地格式化。
                >     * 範例："+1 4255551234" 或 "user@contoso.com"
  >
  >
* **問：密碼重設支援哪些語言？**

  > **答：** hello 密碼重設 UI、 簡訊及語音電話已當地語系化 hello Office 365 中支援的語言相同。
  >
  >
* **問： hello 密碼重設體驗的哪些部分取得品牌時設定組織商標我的目錄中的 [設定] 索引標籤嗎？**

  > **答：** hello 密碼重設入口網站會顯示您組織的標誌，並可讓您 tooconfigure hello，請連絡系統管理員連結 toopoint tooa 自訂電子郵件或 URL。 密碼重設所傳送的任何電子郵件 hello 電子郵件、 hello 主體中包含您組織的標誌、 色彩、 名稱和自訂的名稱。
  >
  >
* **問： 如何引導使用者有關在哪裡 toogo tooreset 他們的密碼？**

  > **答：**您可以直接傳送使用者 toohttps://passwordreset.microsoftonline.com 或指示 tooclick hello**無法存取您的帳戶連結**任何工作或學校登入頁面上找到。 您也可以在進行更容易存取 tooyour 使用者發佈這些連結。
  >
  >
* **問：我是否可以從行動裝置使用此頁面？**

  > **答：** 是，此頁面可在行動裝置上運作。
  >
  >
* **問：當使用者重設其密碼時，您是否支援將本機 Active Directory 帳戶解除鎖定？**

  > **答：**是，當使用者重設其密碼並使用 Azure AD Connect 部署密碼回寫時，該使用者的帳戶會在其重設密碼時自動解除鎖定。
  >
  >
* **問：我要如何將密碼重設直接整合到我使用者的桌面登入體驗？**

  > **答：**如果您是 Azure AD Premium 客戶，您可以安裝 Microsoft Identity Manager 不需額外成本，並部署 hello 在內部部署密碼重設解決方案 toomeet 這項需求。
  >
  >
* **問：我是否可以針對不同的地區設定，設定不同的安全性問題？**

  > **答：** 目前無法這麼做。
  >
  >
* **問： 如何許多問題我們可以設定 hello 安全性問題驗證選項？**

  > **答：** hello too20 自訂安全性問題，您可以設定[Azure 入口網站](https://portal.azure.com)。
  >
  >
* **問：安全性問題的長度限制為何？**

  > **答：** 安全性問題的長度可以介於 3 到 200 個字元之間。
  >
  >
* **問： 保留時間長度可能答案 toosecurity 問題？**

  > **答：**答案可能是 3 too40 個字元長。
  >
  >
* **問： 會拒絕重複回答 toosecurity 問題嗎？**

  > **答：**是，我們會拒絕重複回答 toosecurity 問題。
  >
  >
* **問： 可能是使用者在暫存 hello 相同的安全性問題一次以上嗎？**

  > **答：**否，使用者註冊一旦特定的問題，便不可以再次註冊該問題。
  >
  >
* **問： 是否可能 tooset 最低限制的註冊和重設的安全性問題？**

  > **答：** 是，可以針對註冊設定一個限制，針對重設設定另一個限制。 註冊可能需要 3-5 個安全性問題，重設也需要 3-5 個安全性問題。
  >
  >
* **問： 如果使用者已註冊多個 hello 問題需要 tooreset 數目上限，如何選取安全性問題重設期間？**

  > **答：** N 安全性問題中隨機選取超出 hello 問題總數，使用者所註冊的其中 N 是 hello**問題需要 tooreset 數目**。 例如，如果使用者具有 5 個安全性問題註冊，但只有 3 需要的 tooreset，hello 5 的 3 會隨機選取，並顯示在重設。 如果 hello 使用者 hello 答案 toohello 問題錯誤，又重新出現 hello 選取程序 tooprevent 問題被破解。
  >
  >
* **問：您是否禁止使用者在短時間內嘗試多次密碼重設？**

  > **答：**是，有密碼重設 tooprotect 免遭不當使用內建的安全性功能。 使用者在一個小時之內只能嘗試 5 次密碼重設，否則會鎖定 24 小時。 使用者只能嘗試 toovalidate 電話號碼 5 次，一小時就會被鎖定 24 小時內。 使用者在一個小時之內只能嘗試單一驗證方法 5 次，否則會鎖定 24 小時。
  >
  >
* **問： 為何 hello 電子郵件和簡訊的單次密碼有效？**

  > **答：** hello 密碼重設工作階段存留期為 105 分鐘。 從 hello hello 開頭密碼重設作業、 hello 使用者 105 分鐘 tooreset 他們的密碼。 hello 電子郵件和簡訊的單次密碼是無效的這段時間之後。
  >
  >

## <a name="password-change"></a>密碼變更
* **問： 我的使用者應 toochange 他們的密碼？**

  > **答：**使用者可能會變更其密碼任何位置看到他們的設定檔圖片或圖示 (如同在 hello 右上角的其[Office 365](https://portal.office.com)或[存取面板](https://myapps.microsoft.com)發生。 使用者可能會變更其密碼，從 hello[存取面板設定檔頁面](https://account.activedirectory.windowsazure.com/r#/profile)。 使用者也可能要求 toochange 他們的密碼會自動在 hello Azure AD 登入畫面，如果他們的密碼已過期。 最後，使用者可能瀏覽 toohello [Azure AD 密碼變更入口網站](https://account.activedirectory.windowsazure.com/ChangePassword.aspx)直接如果他們想 toochange 他們的密碼。
  >
  >
* **問： 是否可以我的使用者通知的 hello Office 入口網站在內部部署密碼到期時？**

  > **答：**這是可能今天如果您使用 ADFS hello 遵循指示：[傳送密碼原則宣告使用 ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396)。 如果您使用密碼雜湊同步處理，則目前還不可能。 這是因為我們無法同步處理從內部部署密碼原則，所以不讓我們 toopost 到期通知 toocloud 遇到。 在任一情況下，也可能會太[通知的使用者其密碼即將使用 PowerShell tooexpire](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx)。
  >
  >

## <a name="password-management-reports"></a>密碼管理報告
* **問： 如何花費時間的總 hello 密碼管理報表上的資料 tooshow？**

  > **答：**資料應該在 hello 密碼管理報表上會出現在 5-10 分鐘內。 它可能佔用 tooan 小時 tooappear 某些執行個體。
  >
  >
* **問： 如何可以篩選 hello 密碼管理報表？**

  > **答：**您可以按一下 hello hello 報表頂端附近的 hello 資料行標籤的 hello 小型的放大鏡 toohello 最右側，以篩選 hello 密碼管理報表。 如果您想 toodo 更複雜的篩選，您可以下載 hello 報表 tooexcel 並建立樞紐分析表。
  >
  >
* **問： 什麼是 hello 最大事件數目會儲存在 hello 密碼管理報表？**

  > **答：**向上 too75，000 密碼重設或密碼重設註冊事件會儲存在 hello 密碼管理報表跨越備份 too30 天。  我們正在 tooexpand 這個數字 tooinclude 更多的事件。
  >
  >
* **問： 如何久 hello 密碼管理報表怎麼做？**

  > **答：** hello 密碼管理報告 hello 中發生的過去 30 天內顯示作業。 現在，如果您需要 tooarchive 這項資料，您可以定期下載 hello 報表並將它們儲存在不同的位置。
  >
  >
* **問： 是否有可能會出現在 hello 密碼管理報表的資料列的數目上限？**

  > **答：**是，75000 資料列最多可能會出現在 hello 密碼管理報表，其中是否顯示在 hello UI 或透過下載。
  >
  >
* **問： 是否有應用程式開發介面 tooaccess hello 密碼重設或註冊報表資料？**

  > **答：** [是]，請參閱 hello 下列文件 toolearn 如何存取 hello 密碼重設報表的資料流。  [了解如何 tooaccess 密碼重設報告事件以程式設計方式](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)。
  >
  >

## <a name="password-writeback"></a>密碼回寫
* **問： 密碼回寫如何 hello 幕後運作？**

  > **答：**看到[密碼回寫的運作方式](active-directory-passwords-writeback.md)進行說明內容後，當您啟用密碼回寫，以及資料流動的方式透過 hello 系統回到內部部署環境。
  >
  >
* **問： 如何長密碼回寫會採用 toowork？是否有像是使用密碼雜湊同步處理的同步處理延遲？**

  > **答：**密碼回寫會立即進行。 它是同步管線，基本上的運作與密碼雜湊同步處理不同。 密碼回寫可讓的使用者 tooget 即時意見 hello 成功的密碼重設或變更作業。 hello 的密碼成功回寫的平均時間不超過 500 毫秒。
  >
  >
* **問︰如果我的內部部署帳戶已停用，這對我的雲端帳戶/存取有何影響？**

  > **答：**已停用您在內部部署的識別碼，就也在 hello 下一個同步處理間隔透過 AAD Connect byt 預設停用識別碼/存取您雲端這是每隔 30 分鐘。
  >
  >
* **問： 如果我在內部部署的帳戶由內部部署 Active Directory 密碼原則限制，沒有 SSPR 遵守此原則時變更 hello 密碼嗎？**

  > **答：** SSPR 依賴的是，並遵守 hello 內部部署 AD 密碼原則，包括一般的 AD 網域密碼原則，以及任何已定義更細緻的密碼原則目標 tooa 指定使用者。
  >
  >
* **問：密碼回寫適用於哪些類型的帳戶？**

  > **答：**密碼回寫適用於「同盟」和「密碼雜湊同步」使用者。
  >
  >
* **問：密碼回寫是否會強制執行我的網域密碼原則？**

  > **答：**是，密碼回寫會強制執行密碼使用期限、歷程記錄、複雜度、篩選及任何其他您可能在本機網域中的密碼上適當加諸的限制。
  >
  >
* **問：密碼回寫是否安全？我要如何確定不會受到駭客入侵？**

  > **答：**是，密碼回寫很安全。 hello 密碼回寫服務所實作的 tooread 深入了解 hello 四個層級的安全性，請簽出 hello[密碼回寫安全性模型](active-directory-passwords-writeback.md#password-writeback-security-model)密碼回寫的運作方式 > 一節。
  >
  >

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR
