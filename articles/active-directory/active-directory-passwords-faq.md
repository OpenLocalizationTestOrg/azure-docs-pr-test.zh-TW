---
title: "自助式密碼重設常見問題集 - Azure Active Directory"
description: "有關 Azure AD 自助式密碼重設的常見問題集。"
services: active-directory
keywords: "Active directory 密碼管理, 密碼管理, Azure AD 自助式密碼重設"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2018
ms.author: joflore
ms.custom: seohack1
ms.openlocfilehash: 29b25a476344ed048673039beacdffd39469ec85
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="password-management-frequently-asked-questions"></a>密碼管理常見問題集

以下是與密碼重設相關之所有事項的一些常見問題 (FAQ)。

如果您有關於 Azure Active Directory (Azure AD) 和自助式密碼重設 (SSPR) 的一般問題，但在這裡找不到答案，則可以在 [Azure Ad 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)上向社群尋求協助。 社群的成員包括工程師、產品經理、MVP 和夥伴 IT 專業人員。

此常見問題集分成下列各節：

* [密碼重設註冊的相關問題](#password-reset-registration)
* [密碼重設的相關問題](#password-reset)
* [密碼變更的相關問題](#password-change)
* [密碼管理報告的相關問題](#password-management-reports)
* [密碼回寫的相關問題](#password-writeback)

## <a name="password-reset-registration"></a>密碼重設註冊

* **問：我的使用者是否可以註冊自己的密碼重設資料？**

  > **答：** 是。 只要已啟用密碼重設功能且使用者已獲得授權，他們就可以前往密碼重設註冊入口網站 (http://aka.ms/ssprsetup) 來註冊其驗證資訊。 使用者也可以透過「存取面板」(http://myapps.microsoft.com) 註冊。 若要透過「存取面板」註冊，使用者必須選取其個人資料圖片，請選取 [設定檔]，然後選取 [註冊密碼重設] 選項。
  >
  >
* **問：如果針對群組啟用密碼重設，之後又決定針對所有人啟用，我的使用者需要重新註冊嗎？**

  > **答：**否。 已填入驗證資料的使用者不需要重新註冊。
  >
  >
* **問：我是否可以代表我的使用者定義密碼重設資料？**

  > **答：**是，您可以透過 Azure AD Connect、PowerShell、[Azure 入口網站](https://portal.azure.com)或「Office 365 系統管理中心」來進行此操作。 如需詳細資訊，請參閱 [Azure AD 自助式密碼重設所用的資料](active-directory-passwords-data.md)。
  >
  >
* **問：我是否可以從內部部署環境同步處理安全性問題的資料？**

  > **答：**否，目前無法這麼做。
  >
  >
* **問：我的使用者是否可以註冊資料又不讓其他使用者看見該資料？**

  > **答：** 是。 當使用者使用密碼重設註冊入口網站來註冊資料時，該資料會儲存到僅供全域管理員和該使用者檢視的私密驗證欄位中。
  >
  >
* **問：我的使用者是否必須先註冊才能使用密碼重設？**

  > **答：**否。 如果您代表使用者定義足夠的驗證資訊，使用者就不需要註冊。 只要您已將儲存在目錄中適當欄位的資料正確格式化，密碼重設就能運作。
  >
  >
* **問：我是否可以代表我的使用者同步處理或設定驗證電話、驗證電子郵件或備用驗證電話欄位？**

  > **答：**否，目前無法這麼做。
  >
  >
* **問：註冊入口網站如何判斷要對我的使用者顯示哪些選項？**

  > **答：**密碼重設註冊入口網站只會顯示您已為使用者啟用的選項。 您可以在目錄 [設定] 索引標籤的 [使用者密碼重設原則] 區段底下找到這些選項。例如，如果您未啟用安全性問題，使用者便無法註冊該選項。
  >
  >
* **問：使用者何時會被視為已註冊？**

  > **答︰**當使用者所註冊的重設密碼方法數已至少達到您在 [Azure 入口網站](https://portal.azure.com)中設定的 [需要重設的方法數] 時，便會視為已完成 SSPR 註冊。
  >
  >

## <a name="password-reset"></a>密碼重設

* **問：您是否禁止使用者在短時間內多次嘗試密碼重設？**

  > **答：**是，密碼重設有內建安全性功能，以防止濫用。 
  >
  > 使用者在 24 小時的期間內只能嘗試五次密碼重設，否則會被鎖定 24 小時。 
  >
  > 使用者在一個小時之內只能嘗試驗證電話號碼、傳送 SMS 或驗證安全性問題和回答五次，否則會被鎖定 24 小時。 
  >
  > 使用者在 10 分鐘的期間內最多可以傳送某一封電子郵件 10 次，否則會被鎖定 24 小時。
  >
  > 一旦使用者重設其密碼之後，就會重設計數器。
  >
  >
* **問：密碼重設之後，我應該等待多久才能收到電子郵件、SMS 或來電？**

  > **答：**應該在 1 分鐘內即可收到電子郵件、SMS 訊息及來電。 一般情況下為 5 到 20 秒。
    >如果您未在此時間範圍內收到通知，請︰
        > * 檢查您的垃圾郵件資料夾。
        > * 確認所聯繫的號碼或電子郵件是您預期的號碼或電子郵件。
        > * 確認目錄中的驗證資料已正確格式化，例如 +1 4255551234 或 *user@contoso.com*。 
  >
  >
* **問：密碼重設支援哪些語言？**

  > **答：**密碼重設 UI、SMS 訊息及語音通話都已採用 Office 365 支援的相同語言當地語系化。
  >
  >
* **問：當我在目錄的 [設定] 索引標籤中設定組織商標項目時，哪個密碼重設體驗部分會有商標？**

  > **答：**密碼重設入口網站會顯示您的組織標誌，並可讓您將 [請連絡您的系統管理員] 連結設定成指向自訂的電子郵件或 URL。 密碼重設所傳送的所有電子郵件都會在電子郵件本文中包含您的組織標誌、色彩及名稱，並且會從該特定名稱的設定進行自訂。
  >
  >
* **問：如何教育我的使用者要在哪裡重設其密碼？**

  > **答：**請試試 [SSPR 部署](active-directory-passwords-best-practices.md#email-based-rollout)一文中的一些建議。
  >
  >
* **問：我是否可以從行動裝置使用此頁面？**

  > **答：** 是，此頁面可在行動裝置上運作。
  >
  >
* **問：當使用者重設其密碼時，您是否支援將本機 Active Directory 帳戶解除鎖定？**

  > **答：** 是。 當使用者重設其密碼時，如果已透過 Azure AD Connect 部署密碼回寫，該使用者的帳戶就會在其重設密碼時自動解除鎖定。
  >
  >
* **問：我要如何將密碼重設直接整合到我使用者的桌面登入體驗？**

  > **答：**如果您是 Azure AD Premium 客戶，則無須額外付費即可安裝 Microsoft Identity Manager，並部署內部部署密碼重設解決方案。
  >
  >
* **問：我是否可以針對不同的地區設定，設定不同的安全性問題？**

  > **答：**否，目前無法這麼做。
  >
  >
* **問：我可以為安全性問題驗證選項設定多少問題？**

  > **答：**您可以在 [Azure 入口網站](https://portal.azure.com)中設定最多 20 個自訂安全性問題。
  >
  >
* **問：安全性問題的長度限制為何？**

  > **答：**安全性問題的長度可為 3 到 200 個字元。
  >
  >
* **問：安全性問題答案的長度限制為何？**

  > **答：** 答案的長度可為 3 到 40 個字元。
  >
  >
* **問：重複的安全性問題答案是否會遭到拒絕？**

  > **答：** 是，我們會拒絕重複的安全性問題答案。
  >
  >
* **問：使用者是否可以將同一個安全性問題註冊多次？**

  > **答：**否。 使用者註冊特定問題之後，便無法再次註冊該問題。
  >
  >
* **問：是否可以針對註冊和重設設定安全性問題的最小限制？**

  > **答：** 是，可以針對註冊設定一個限制，針對重設設定另一個限制。 註冊可能需要 3 到 5 個安全性問題，重設可能也需要 3 到 5 個問題。
  >
  >
* **問：我已將原則設定為要求使用者使用安全性問題進行重設，但 Azure 系統管理員似乎是以不同方式設定。**

  > **答：**這是預期中的行為。 Microsoft 會針對任何 Azure 系統管理員角色強制執行強式預設雙閘道密碼重設原則。 這會讓系統管理員無法使用安全性問題。 如需有關此原則的詳細資訊，請參閱 [Azure Active Directory 中的密碼原則和限制](active-directory-passwords-policy.md#administrator-password-policy-differences)一文。
  >
  >
* **問：如果使用者註冊的問題數目超過重設所需的問題數目上限，在重設期間會如何選取安全性問題？**

  > **答：**會在使用者已註冊的問題總數當中隨機選取 *N* 個安全性問題，其中 *N* 是為 [需要重設的方法數] 選項設定的數量。 例如，如果使用者已註冊 5 個安全性問題，但只需 3 個問題即可重設密碼，系統就會在重設時隨機選取並顯示 5 個問題中的 3 個問題。 為了防止猜題攻擊，如果使用者回答問題的答案錯誤，選取程序就會重來。
  >
  >
* **問：電子郵件和 SMS 單次密碼的有效期限是多久？**

  > **答：**密碼重設的工作階段存留期為 15 分鐘。 從密碼重設作業開頭算起，使用者有 15 分鐘可以重設其密碼。 這段時間之後，電子郵件和 SMS 單次密碼就會無效。
  >
  >
* **問：是否可以防止使用者重設其密碼？**

  > **答：**是，如果您使用群組來啟用 SSPR，就可以將個別使用者從允許其重設密碼的群組中移除。
  >
  >

## <a name="password-change"></a>密碼變更

* **問︰我的使用者應該到何處變更密碼？**

  > **答︰**使用者可以在出現個人資料圖片或圖示的任何位置變更其密碼 (例如在其 [Office 365](https://portal.office.com) 入口網站或[存取面板](https://myapps.microsoft.com)的右上角)。 使用者可以從[存取面板設定檔頁面](https://account.activedirectory.windowsazure.com/r#/profile)變更其密碼。 如果使用者的密碼已到期，Azure AD 登入頁面也可能自動要求使用者變更密碼。 最後，如果使用者想要變更其密碼，也可以直接瀏覽至 [Azure AD 密碼變更入口網站](https://account.activedirectory.windowsazure.com/ChangePassword.aspx)。
  >
  >
* **問︰當我使用者的內部部署密碼到期時，Office 入口網站是否會通知他們？**

  > **答：**是，目前如果您使用「Active Directory 同盟服務」(AD FS)，就可以傳送通知。 如果您使用 AD FS，請依照[使用 AD FS 來傳送密碼原則宣告](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396) \(機器翻譯\) 一文中的指示進行操作。 如果您使用密碼雜湊同步處理，則目前還無法傳送通知。 我們不會從內部部署目錄同步處理密碼原則，因此無法對雲端體驗發佈到期通知。 在上述任一情況下，也可以[透過 PowerShell 通知密碼即將到期的使用者](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx) \(英文\)。
  >
  >
* **問：是否可以防止使用者變更其密碼？**

  > **答：**針對僅限雲端的使用者，並無法防止其變更密碼。 針對內部部署使用者，則可以選取 [使用者不能變更密碼] 選項。 所選取的使用者會無法變更其密碼。
  >
  >

## <a name="password-management-reports"></a>密碼管理報告

* **問：資料需要多久的時間才會顯示在密碼管理報告上？**

  > **答：** 資料應該會在 5 到 10 分鐘內顯示在密碼管理報告上。 在某些情況下，可能會花費長達一小時的時間才顯示。
  >
  >
* **問：我要如何篩選密碼管理報告？**

  > **答：**若要篩選密碼管理報告，請選取靠近報告頂端、資料行標籤最右邊的小放大鏡圖示。 如果您想要進行更豐富的篩選，可以將報告下載到 Excel 並建立樞紐分析表。
  >
  >
* **問：密碼管理報告中最多可以儲存多少事件？**

  > **答：**密碼管理報告中最多可以儲存 75,000 個密碼重設或密碼重設註冊事件，最多可回溯 30 天。 我們正在擴展此數目，以包含更多的事件。
  >
  >
* **問：密碼管理報告可以回溯到多久以前？**

  > **答：** 密碼管理報告會顯示過去 30 天內發生的作業。 現在，如果您需要封存這項資料，您可以定期下載報告並將它們儲存在不同的位置。
  >
  >
* **問：密碼管理報告可以顯示的資料列是否有數目上限？**

  > **答：** 是。 不論是在 UI 中顯示或是下載，任一密碼管理報告最多都只能顯示 75,000 個資料列。
  >
  >
* **問：是否有可用來存取密碼重設或註冊報告資料的 API？**

  > **答：** 是。 若要了解如何存取密碼重設報告資料流，請參閱[了解如何以程式設計方式存取密碼重設報告事件](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) \(英文\)。
  >
  >

## <a name="password-writeback"></a>密碼回寫

* **問：密碼回寫如何在幕後運作？**

  > **答：**請參閱[密碼回寫的運作方式](active-directory-passwords-writeback.md)一文，以了解啟用密碼回寫時會發生的情況，以及資料如何透過系統回流到您的內部部署環境。
  >
  >
* **問：密碼回寫需要多久時間才會運作？是否有像是使用密碼雜湊同步處理時的同步處理延遲？**

  > **答：**密碼回寫會立即進行。 它是同步管線，基本上的運作與密碼雜湊同步處理不同。 密碼回寫可以讓使用者即時取得密碼重設或變更作業成功的回應。 成功回寫密碼的平均時間低於 500 毫秒。
  >
  >
* **問︰如果我的內部部署帳戶已停用，這對我的雲端帳戶和存取權有何影響？**

  > **答︰**如果您的內部部署識別碼已停用，您的雲端識別碼和存取權也會在下一次透過 Azure AD Connect 進行同步處理時停用。 此同步處理預設會每 30 分鐘執行一次。
  >
  >
* **問︰如果我的內部部署帳戶受到內部部署 Active Directory 密碼原則限制，當我變更密碼時，SSPR 是否會遵守此原則？**

  > **答：**是，SSPR 會依據並遵守內部部署 Active Directory 密碼原則。 此原則包括一般 Active Directory 網域密碼原則，以及任何以使用者為目標的已定義、更精細密碼原則。
  >
  >
* **問：密碼回寫適用於哪些類型的帳戶？**

  > **答：**密碼回寫適用於同盟和已同步處理密碼雜湊的使用者。
  >
  >
* **問：密碼回寫是否會強制執行我的網域密碼原則？**

  > **答：** 是。 密碼回寫會強制執行密碼有效期、歷程記錄、複雜度、篩選，以及任何其他您可能在本機網域中的密碼上適當加諸的限制。
  >
  >
* **問：密碼回寫是否安全？我要如何確定不會受到駭客入侵？**

  > **答：**是，密碼回寫很安全。 若要深入了解密碼回寫服務所實作的四層安全性，請參閱[密碼回寫概觀](active-directory-passwords-writeback.md)一文中的[密碼回寫的安全性模型](active-directory-passwords-writeback.md#password-writeback-security-model)一節。
  >
  >

## <a name="next-steps"></a>後續步驟

* [如何完成 SSPR 成功首度發行？](active-directory-passwords-best-practices.md)
* [重設或變更您的密碼](active-directory-passwords-update-your-own-password.md)
* [註冊自助式密碼重設](active-directory-passwords-reset-register.md)
* [您有授權問題嗎？](active-directory-passwords-licensing.md)
* [SSPR 使用哪些資料，以及您應該為使用者填入哪些資料？](active-directory-passwords-data.md)
* [哪些驗證方法可供使用者使用？](active-directory-passwords-how-it-works.md#authentication-methods)
* [使用 SSPR 的原則選項有哪些？](active-directory-passwords-policy.md)
* [什麼是密碼回寫，且為什麼我需要了解它？](active-directory-passwords-writeback.md)
* [如何回報 SSPR 中的活動？](active-directory-passwords-reporting.md)
* [SSPR 中的所有選項有哪些，以及它們有何意義？](active-directory-passwords-how-it-works.md)
* [我認為有中斷。如何針對 SSPR 進行疑難排解？](active-directory-passwords-troubleshoot.md)
