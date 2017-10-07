---
title: "針對 Azure Active Directory 中的企業狀態漫遊設定進行疑難排解 | Microsoft Docs"
description: "提供有關設定和應用程式資料同步可能答案 toosome 問題 IT 系統管理員。"
services: active-directory
keywords: "企業狀態漫遊設定, windows 雲端, 企業狀態漫遊常見問題集"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>針對 Azure Active Directory 中的企業狀態漫遊設定進行疑難排解

本主題提供如何的相關資訊 tootroubleshoot 和診斷企業狀態漫遊的問題，並提供的已知問題清單。

## <a name="preliminary-steps-for-troubleshooting"></a>疑難排解的預備步驟 
開始之前疑難排解確認，hello 使用者和裝置已設定正確，且裝置 hello 和 hello 使用者符合所有 hello 需求的企業狀態漫遊。 

1. Hello 裝置上安裝 Windows 10 與 hello 最新的更新和最小版本 1511 （作業系統組建 10586 或更新版本）。 
2. hello 裝置已加入，或已加入網域並向 Azure AD 註冊的 Azure AD。
3. 在 hello Azure Active Directory 入口網站**企業狀態漫遊**hello 目錄下啟用**設定** > **裝置** > **使用者可以同步設定及企業應用程式資料**。 選取所有的使用者，或是 hello 使用者是用於透過 hello 選取選項的同步處理已啟用，而且包含在 hello 安全性群組。
4. hello 使用者具有 Azure Active Directory Premium 訂閱指派 toothem。  
5. hello 裝置已重新啟動，並啟用企業狀態漫遊之後 hello 使用者登入。

## <a name="information-tooinclude-when-you-need-help"></a>當您需要協助的資訊 tooinclude
如果您無法解決您的問題與下列 hello 指引，您可以連絡我們的支援工程師。 當您與他們連絡時，我們建議 tooinclude hello 下列資訊：

- **Hello 錯誤的一般描述**– 有 hello 使用者看見的錯誤訊息？ 如果不發生任何錯誤訊息，說明 hello 未預期的行為，您會注意到，在詳細資料。 哪些功能可供同步和是預期 toosync hello 使用者？ 多項功能不會同步，或者是隔離的 it tooone？
- **受影響的使用者** – 是有一位還是多位使用者的同步處理成功/失敗？ 每個使用者涉及多少裝置？ 它們是否都沒有同步處理，或它們之間部分已同步處理，部分沒有同步處理？
- **Hello 使用者資訊**– 何種身分識別是使用 toolog toohello 裝置中的 hello 使用者嗎？ Hello 使用者如何記錄 toohello 裝置？ 它們屬於選取的安全性群組，允許 toosync 嗎？ 
- **Hello 裝置的相關資訊**– 此裝置加入 Azure AD 之或已加入網域？ 哪些組建是 hello 的裝置上？ Hello 最新的更新有哪些？
- **日期 / 時間 / 時區**– hello 確切的日期和的時間看到 hello 錯誤 （包含 hello 時區）？
- 包含這項資訊有助於我們盡快為您解決問題。

## <a name="troubleshooting-and-diagnosing-issues"></a>疑難排解和診斷問題
本節提供如何建議 tootroubleshoot 及診斷問題的相關的 tooEnterprise 漫遊狀態。

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>確認同步處理，並 hello"同步您的設定 」 設定 頁面 

1. 加入 Windows 10 電腦 tooa 之後網域設定 tooallow 企業狀態漫遊，請使用您的工作帳戶登入。 跳過**設定** > **帳戶** > **同步處理您的設定**，並確認同步處理和 hello 個別的設定，和該 hello 頂端hello 設定頁面會指出您正在使用工作帳戶同步處理。 確認在您登入帳戶也會使用相同帳戶的 hello**設定** > **帳戶** > **您資訊**。 
2. 確認同步處理運作跨多部機器 hello 原始電腦，例如移動 hello 工作列 toohello 靠右或最上層的一端囉 」 畫面上，進行一些變更。 觀賞 hello 變更五分鐘內傳播 toohello 第二部電腦。 
 - 鎖定和解除鎖定囉 」 畫面 （Win + L） 可協助您在同步處理觸發程序。
 - 您必須使用 hello 的同步處理 toowork – 這兩種電腦上的相同登入帳戶，因為企業狀態漫遊是繫結的 toohello 使用者帳戶和 hello 電腦帳戶。

**可能的問題**: hello 設定 頁面上有呈灰色，hello 切換，而不是查看帳戶，您看到 hello 文字"一些 Windows 功能才會出現您使用 Microsoft 帳戶或工作帳戶 」。 針對已設定 toobe 的裝置已加入網域並註冊 tooAzure AD，但是 hello 裝置已成功驗證 tooAzure AD，可能會發生此問題。 可能的原因是必須套用 hello 裝置原則，但此應用程式會以非同步的方式，而且可能會因為幾小時的時間延遲。 這個問題，請依照中的 hello 步驟確認的 tooverify hello 裝置登錄狀態 toocheck 如果 hello 這樣的狀況。

### <a name="verify-hello-device-registration-status"></a>確認 hello 裝置登錄狀態
企業狀態漫遊需要 hello 裝置 toobe 向 Azure AD 註冊。 雖然不是特定 tooEnterprise 狀態漫遊，遵循下列指示 hello 可以幫助確認該 hello 註冊 Windows 10 用戶端，並確認憑證指紋，Azure AD 設定 URL，NGC 狀態，以及其他資訊。

1.  開啟 hello 命令提示字元停權。 這在 Windows 中，開啟 toodo hello 執行啟動器 （Win + R），並輸入"cmd"tooopen。
2.  一旦開啟 hello 命令提示字元，輸入 「*dsregcmd.exe /status*"。
3.  預期的輸出，如 hello **AzureAdJoined**欄位值應該是"YES"， **WamDefaultSet**欄位值應該是"YES"，並且 hello **WamDefaultGUID**欄位值應該是GUID"(azure Ad)"hello 結尾。

**可能的問題**: **WamDefaultSet**和**AzureAdJoined** hello 欄位值中有 「 否 」，hello 裝置已加入網域且已註冊使用 Azure AD，和 hello 裝置不會同步。如果顯示這個，hello 裝置可能需要套用的原則 toobe toowait 或 hello hello 裝置連線 tooAzure AD 時發生失敗的驗證。 hello 使用者有 toowait hello 原則 toobe 套用的幾個小時。 其他疑難排解步驟可能包含由簽署 out 與中，或啟動工作排程器中的 hello 工作重試自動註冊。 在某些情況下，於已提升權限的命令提示字元視窗中執行 *dsregcmd.exe /leave*、重新開機，然後再試一次註冊，可能有助於解決此問題。


**可能的問題**: hello 欄位**AzureAdSettingsUrl**是空白的然後 hello 裝置不同步。 hello 使用者可能已上次登入 toohello 裝置 hello Azure Active 中啟用企業狀態漫遊之前目錄入口網站。 重新啟動 hello 裝置並擁有 hello 使用者登入。 （選擇性） 在 hello 入口網站，再試一次需要的 hello IT 系統管理員停用並重新啟用的使用者可能會同步處理設定及企業應用程式資料。 一旦重新啟用，重新啟動 hello 裝置，而且擁有 hello 使用者登入。 如果這樣做無法解決 hello 問題**AzureAdSettingsUrl**可能是空的不正確的裝置憑證 hello 案例。 在此情況下，於已提升權限的命令提示字元視窗中執行 *dsregcmd.exe /leave*、重新開機，然後再試一次註冊，可能有助於解決此問題。

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>企業狀態漫遊與 Multi-Factor Authentication 
某些狀況下，企業狀態漫遊可能會失敗 toosync 資料如果 Azure Multi-factor Authentication Server 設定。 如需這些徵狀的其他詳細資訊，請參閱 hello 支援文件[KB3193683](https://support.microsoft.com/kb/3193683)。 

**可能的問題**： 如果您的裝置 hello Azure Active Directory 入口網站上的設定的 toorequire Multi-factor Authentication，您可能會失敗 toosync 設定時登入 tooa Windows 10 裝置使用的密碼。 這種類型的 Multi-factor Authentication 設定是預定的 tooprotect Azure 系統管理員帳戶。 系統管理員使用者仍然可能無法 toosync 簽署 tootheir Windows 10 裝置與他們的 Microsoft Passport for Work 的 PIN，或藉由存取其他 Azure 服務，例如 Office 365 時完成多重要素驗證。

**可能的問題**： 如果 hello 系統管理員設定 hello Active Directory 同盟服務多重要素驗證條件式存取原則和 hello hello 裝置上的存取權杖到期，同步處理可能會失敗。 請確認您登入和登出使用 hello Microsoft Passport for Work 的 PIN 或存取其他 Azure 服務，例如 Office 365 時完成多重要素驗證。

###<a name="event-viewer"></a>事件檢視器
對進階疑難排解，事件檢視器可以使用的 toofind 特定錯誤。 這些案例記載在 hello 表中。 您可以在事件檢視器找到 hello 事件 > 應用程式及服務記錄檔 > **Microsoft** > **Windows** > **SettingSync**和針對與同步處理身分識別相關的問題**Microsoft** > **Windows** > **Azure AD**。


## <a name="known-issues"></a>已知問題

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>同步處理在使用 MDM 軟體側載應用程式的裝置上無法運作

執行會影響裝置 hello Windows 10 年度更新 (版本 1607)。 在 hello SettingSync Azure 記錄檔事件檢視器，經常會看到錯誤 80070259 hello 事件識別碼 6013。

**建議的動作**  
請確定 Windows 10 hello v1607 用戶端具有 hello 2016 年 8 月 23 日累計更新 ([KB3176934](https://support.microsoft.com/kb/3176934) OS 建置 14393.82)。 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Internet Explorer 我的最愛不會同步

執行會影響裝置 hello Windows 10 11 月更新 (版本 1511)。

**建議的動作**  
請確定 Windows 10 hello v1511 用戶端具有 hello 2016 年 7 月累計更新 ([KB3172985](https://support.microsoft.com/kb/3172985) OS 建置 10586.494)。

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>佈景主題和使用「Windows 資訊保護」保護的資料不會同步處理 

tooprevent 資料外洩，與受保護的資料[Windows 資訊保護](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)將不會同步透過企業狀態漫遊的裝置使用 hello Windows 10 年度更新。



**建議的動作**  
無。 未來的更新 tooWindows 可解決此問題。

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>已加入網域的裝置上不會同步處理日期、時間及地區設定 
  
加入網域的裝置不會經歷 hello 日期、 時間和地區設定的同步處理： 自動的時間。 使用自動時間可能會覆寫 hello 其他日期、 時間和地區設定和導致不 toosync 這些設定。 

**建議的動作**  
無。 

---

### <a name="uac-prompts-when-syncing-passwords"></a>同步密碼時出現 UAC 提示

會影響裝置執行 hello Windows 10 11 月更新 (版本 1511) 與無線 NIC 設定 toosync 密碼。

**建議的動作**  
請確定 Windows 10 hello v1511 用戶端具有 hello 累計更新 ([KB3140743](https://support.microsoft.com/kb/3140743) OS 建置 10586.494)。

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>同步處理不會在使用智慧卡登入的裝置上運作
如果您嘗試 toosign tooyour Windows 裝置使用智慧卡或虛擬智慧卡中的，設定同步處理將會停止運作。     

**建議的動作**  
無。 未來的更新 tooWindows 可解決此問題。

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>已加入網域的裝置不會在離開公司網路後同步處理     
已加入網域的裝置註冊的 tooAzure AD 如果 hello 裝置是很長的時間，且位於異地，因此無法完成網域驗證，可能會發生同步處理失敗。

**建議的動作**  
Hello 裝置 tooa 公司網路連線，以便可以繼續同步處理。

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Azure AD 聯結裝置無法同步處理而且 hello 使用者混合大小寫的使用者主體名稱。
 Hello 使用者具有混合大小寫字母的 UPN （例如使用者名稱而不是使用者名稱） 而 hello 使用者是已經升級，從 Windows 10 組建 10586 too14393 加入 Azure AD 之裝置上，如果 hello 使用者的裝置可能會失敗 toosync。 

**建議的動作**  
將需要 toounjoin hello 使用者，並將它重新加入 hello 裝置 toohello 雲端。 toodo hello 本機系統管理員使用者身分，登入和移過退出 hello 裝置**設定** > **系統** > **有關**並選取"管理者或中斷與工作或學校 」。 清除 hello 以下檔案，然後按一下 Azure AD Join hello 裝置一次在**設定** > **系統** > **有關**，然後選取 連線tooWork 或學校 」。 繼續 toojoin hello 裝置 tooAzure Active Directory 和完整 hello 流程。

在 hello 清除步驟中，清除 hello 下列檔案：
- `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\` 中的 Settings.dat
- 所有 hello hello 資料夾下的檔案`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>事件識別碼 6065：80070533 此使用者無法登入，因為此帳戶目前已停用  
在 hello SettingSync/偵錯記錄檔事件檢視器，可以 hello 使用者的認證已過期時會出現此錯誤。 此外，它可能發生在 hello 租用戶自動沒有 AzureRMS 佈建。 

**建議的動作**  
在 hello 第一個案例中，有 hello 使用者更新其認證和登入 toohello 裝置 hello 新的認證。 中所列的 hello 步驟繼續 toosolve hello AzureRMS 問題[KB3193791](https://support.microsoft.com/kb/3193791)。 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>事件識別碼 1098：錯誤：0xCAA5001C 權杖代理人操作失敗  
在 hello AAD/操作記錄檔事件檢視器，可能會出現此錯誤與事件 1104年: AAD 雲端 AP 外掛程式呼叫 Get 語彙基元傳回錯誤： 0xC000005F。 如果缺少權限或擁有權屬性，就會發生這個問題。    

**建議的動作**  
繼續進行列出的 hello 步驟[KB3196528](https://support.microsoft.com/kb/3196528)。  



## <a name="next-steps"></a>後續步驟

- 使用 hello[使用者之聲論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming)tooprovide 意見反應，讓的建議方式 tooimprove 企業狀態漫遊。

- 如需詳細資訊，請參閱 hello[企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)。 

## <a name="related-topics"></a>相關主題
* [企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)
* [在 Azure Active Directory 中啟用企業狀態漫遊](active-directory-windows-enterprise-state-roaming-enable.md)
* [設定和資料漫遊常見問題集](active-directory-windows-enterprise-state-roaming-faqs.md)
* [設定同步處理的群組原則和 MDM 設定](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 漫遊設定參考](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
