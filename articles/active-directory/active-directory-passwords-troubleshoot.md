---
title: "疑難排解︰Azure AD SSPR | Microsoft Docs"
description: "針對 Azure AD 自助式密碼重設進行疑難排解"
services: active-directory
keywords: 
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
ms.date: 08/08/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 361ef5f37e4e9de83d3f9d5a8e5177d186fe86d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-self-service-password-reset"></a>Tootroubleshoot 自助式密碼重設的方式

如果您有問題的自助式密碼重設，hello 之後的項目可協助您快速使用 tooget 項目。

## <a name="troubleshoot-self-service-password-reset-errors-that-a-user-may-see"></a>針對使用者可能會看到的自助式密碼重設錯誤進行疑難排解

| 錯誤 | 詳細資料 | 技術詳細資訊 |
| --- | --- | --- |
| TenantSSPRFlagDisabled = 9 | 很抱歉 <br> 因為您的系統管理員已為貴組織停用密碼重設，此時您無法重設密碼。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡系統管理員並要求他們 tooenable 這項功能。 詳細資訊，讀取 toolearn[的說明，請我忘記密碼 Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-update-your-own-password#common-problems-and-their-solutions)。 | SSPR_0009：我們已偵測到您的系統管理員尚未啟用「密碼重設」。 請連絡您的系統管理員並要求他們 tooenable 密碼重設為您的組織。 |
| WritebackNotEnabled = 10 |很抱歉 <br> 因為您的系統管理員尚未為貴組織啟用必要的服務，此時您無法重設密碼。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡系統管理員並要求他們 toocheck 貴組織的設定。 進一步了解這個必要的服務，toolearn 讀取[設定密碼回寫](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-writeback#configuring-password-writeback)。 | SSPR_0010：我們已偵測到「密碼回寫」尚未啟用。 請連絡您的系統管理員並要求他們 tooenable 密碼回寫。 |
| SsprNotEnabledInUserPolicy = 11 | 很抱歉  <br> 因為您的系統管理員尚未為貴組織設定密碼重設，此時您無法重設密碼。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡您的系統管理員並要求他們 tooconfigure 密碼重設。 toolearn 深入了解密碼重設組態讀取的 hello 文章[快速入門： Azure AD 自助式密碼重設](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-getting-started)。 | SSPR_0011：您的組織尚未定義密碼重設原則。 請連絡您的系統管理員並要求他們 toodefine 密碼重設原則。 |
| UserNotLicensed = 12 | 很抱歉 <br> 因為缺少貴組織所需要的授權，此時您無法重設密碼。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡您的系統管理員並要求他們 toocheck 授權指派。 進一步了解授權 toolearn 閱讀 hello 文章[授權需求的 Azure AD 自助式密碼重設](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-licensing)。 | SSPR_0012： 您的組織沒有所需的 hello 授權必要 tooperform 密碼重設。 請連絡您的系統管理員並要求他們 tooreview 授權指派。 |
| UserNotMemberOfScopedAccessGroup = 13 | 很抱歉 <br> 您無法重設密碼此時因為您的系統管理員未設定帳戶 toouse 密碼重設。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡系統管理員並要求他們 tooconfigure 密碼重設您的帳戶。 深入了解帳戶組態的密碼重設閱讀 hello 文章 toolearn[轉出使用者密碼重設](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-best-practices)。 | SSPR_0012：您不是已啟用密碼重設之群組的成員。 請連絡系統管理員，並要求 toobe 加入的 toohello 群組。 |
| UserNotProperlyConfigured = 14 | 很抱歉 <br> 因為缺少您帳戶所需要的資訊，此時您無法重設密碼。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡系統管理員並要求他們 tooreset 您為您的密碼。 有存取 tooyour 帳戶之後，您可以了解註冊 hello 必要資訊遵循 hello hello 文件中的步驟[註冊自助式密碼重設](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-reset-register)。 | SSPR_0014： 額外的安全性資訊是需要的 tooreset 您的密碼。 tooproceed，請連絡您的系統管理員並要求他們 tooreset 您的密碼。 您有存取 tooyour 帳戶之後，您可以註冊 https://aka.ms/ssprsetup 的其他安全性資訊。 您的系統管理員可以新增其他安全性資訊 tooyour 帳戶中的 hello 步驟[集合與密碼重設的讀取的驗證資料](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-data#set-and-read-authentication-data-using-powershell)。 |
| OnPremisesAdminActionRequired = 29 | 很抱歉 <br> 因為貴組織的密碼重設設定發生問題，此時無法重設密碼。 沒有任何進一步的動作，您可以採取 tooresolve 這種情況。 請連絡您的系統管理員並要求他們 tooinvestigate。 進一步了解 hello 潛在問題 toolearn 閱讀 hello 文章[疑難排解密碼回寫](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback)。 | SSPR_0029： 我們會無法 tooreset 您的密碼到期，您在內部部署的組態 tooan 時發生錯誤。 請連絡您的系統管理員並要求他們 tooinvestigate。 |
| OnPremisesConnectivityError = 30 | 很抱歉 <br> 我們無法重設密碼此時由於連線問題 tooyour 組織。 沒有任何動作 tootake 的但是 hello 問題可能是已解決，如果您稍後再試。 如果 hello 問題持續發生，請連絡您的系統管理員，並要求他們 tooinvestigate。 有關連線問題的詳細資訊讀取的 toolearn[疑難排解密碼回寫連線](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-troubleshoot#troubleshoot-password-writeback-connectivity)。 | SSPR_0030： 我們無法重設您的密碼到期，tooa 連線不佳與內部部署環境。 請連絡您的系統管理員並要求他們 tooinvestigate。|


## <a name="troubleshoot-password-reset-configuration-in-hello-azure-portal"></a>疑難排解 hello Azure 入口網站中的密碼重設設定

| **錯誤** | 方案 |
| --- | --- |
| 我看不到 hello**密碼重設**下 hello Azure 入口網站中的 Azure AD 區段 | 如果您沒有 Azure AD Premium 或 Basic 授權指派 toohello 系統管理員執行 hello 作業，也可能會發生。 <br> 這可以藉由指派的授權 toohello 系統管理員帳戶有問題使用 hello 發行項解決[指派、 驗證，並解決授權問題](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| 我沒看到特定設定選項 | Hello UI 的許多項目會隱藏起來。 嘗試啟用所有您想要 toosee 的 hello 選項。 |
| 我沒看到 hello**內部整合** 索引標籤 | 只有在您下載 Azure AD Connect 並設定密碼回寫後，這個選項才會出現。 如需有關本主題的詳細資訊，請參閱 hello 文章[開始使用 Azure AD Connect 以快速設定](./connect/active-directory-aadconnect-get-started-express.md)。 |

## <a name="troubleshoot-password-reset-reporting"></a>針對密碼重設報告進行疑難排解

| **錯誤** | 方案 |
| --- | --- |
| 我沒看到任何密碼管理的活動類型會出現在 hello**自助密碼管理**稽核事件類別目錄 | 如果您沒有 Azure AD Premium 或 Basic 授權指派 toohello 系統管理員執行 hello 作業，也可能會發生。 <br> 這可以藉由指派的授權 toohello 系統管理員帳戶有問題使用 hello 發行項解決 [指派、 驗證，並解決問題的授權] |
| 使用者註冊顯示多個時間 | 當使用者註冊時，我們目前會將所註冊的每一筆個別資料記錄為個別事件。 <br> 如果您想 tooaggregate 這項資料，您可以下載 hello 報表，並開啟 hello 資料當做樞紐分析表中的 excel toohave 更大的彈性。

## <a name="troubleshoot-password-reset-registration-portal"></a>針對密碼重設註冊入口網站進行疑難排解

| **錯誤** | 方案 |
| --- | --- |
| 目錄未啟用密碼重設**您的系統管理員尚未啟用您 toouse 這項功能** | 交換器 hello**自助服務密碼重設啟用**旗標太**群組**或**可否**按一下**儲存** |
| 使用者沒有 Azure AD Premium 或 Basic 授權指派**您的系統管理員尚未啟用您 toouse 這項功能** | 如果您沒有 Azure AD Premium 或 Basic 授權指派 toohello 系統管理員執行 hello 作業，也可能會發生。 <br> 這可以藉由指派的授權 toohello 系統管理員帳戶有問題使用 hello 發行項解決[指派、 驗證，並解決授權問題](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| 處理要求時發生錯誤 | 許多問題都會造成此情形，但這個錯誤通常是因為服務中斷或設定問題所導致。 如果您看到這個錯誤，而且它會影響您的業務，請連絡 Microsoft 支援服務人員以尋求其他協助。 |

## <a name="troubleshoot-password-reset-portal"></a>針對密碼重設入口網站進行疑難排解

| **錯誤** | 方案 |
| --- | --- |
| 目錄未啟用密碼重設功能。 | 交換器 hello**自助服務密碼重設啟用**旗標太**群組**或**可否**按一下**儲存** |
| 使用者尚未獲得 Azure AD Premium 或 Basic 授權 | 如果您沒有 Azure AD Premium 或 Basic 授權指派 toohello 系統管理員執行 hello 作業，也可能會發生。 <br> 這可以藉由指派的授權 toohello 系統管理員帳戶有問題使用 hello 發行項解決[指派、 驗證，並解決授權問題](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses) |
| 目錄已啟用密碼重設，但使用者的驗證資訊遺失或格式不正確 | 請確定該使用者具有正確後再繼續 hello 目錄中檔案的連絡資料。 如需有關本主題的詳細資訊，請參閱 hello 文章[使用 Azure AD 自助式密碼重設資料](active-directory-passwords-data.md)。 |
| 目錄已啟用密碼重設，但是使用者只有一個連絡資料的檔案若原則設 toorequire 兩個驗證步驟 | 確定使用者有至少兩個已正確設定的連絡方法 (例如：行動電話**和**辦公室電話)，然後再繼續。 |
| 目錄已啟用密碼重設，但使用者已正確設定，使用者會無法連絡的 toobe | 這可能是暫時性服務錯誤或不正確的連絡資料，我們偵測不到正確的 hello 結果。 <br> <br> 如果 hello 使用者等候 10 秒，再試一次，而且會出現 「 連絡您的系統管理員 」 連結。 再按一下 再試一次重試 hello 呼叫，而按一下 「 連絡您的系統管理員 」 將傳送表單電子郵件 tooadministrators 要求密碼重設 toobe 該使用者帳戶執行。 |
| 使用者從未收到 hello 密碼重設簡訊或電話 | 這可能是格式不正確的電話號碼 hello 目錄中的 hello 結果。 請確定 hello 電話號碼的格式 hello"+ ccc xxxyyyzzzzXeeee"。 <br> <br> 密碼重設不支援擴充功能，即使您指定一個 hello （其會移除之前會分派 hello 呼叫） 的目錄中。 請嘗試使用不含副檔名，或將 hello 擴充功能整合到 PBX hello 電話號碼。 |
| 使用者從未收到密碼重設電子郵件 | hello 這個問題的最常見的原因是垃圾郵件篩選器會拒絕該 hello 訊息。 請檢查您的垃圾郵件、 垃圾郵件，或已刪除的項目 資料夾的 hello 電子郵件。 <br> 也請確定您所檢查的 hello 訊息 hello 正確的電子郵件。 |
| 我已設定密碼重設原則，但是當系統管理員帳戶使用密碼重設時，卻未套用該原則 | Microsoft 會管理及控制 hello 系統管理員密碼重設原則 tooensure hello 最高的安全性層級。 |
| 使用者被禁止在一天當中嘗試重設密碼太多次 | 我們實作自動節流機制 tooblock 使用者嘗試 tooreset 他們的密碼太多次在短時間內。 其發生條件如下： <br> 1.使用者嘗試 toovalidate 電話號碼 5 次，一小時的時間。 <br> 2.使用者嘗試 toouse hello 安全性問題閘門 5 次在一小時內。 <br> 3.使用者嘗試 tooreset hello 的密碼 5 次在一小時內的相同使用者帳戶。 <br> toofix，指示 hello 使用者 toowait hello 最後一次之後, 的 24 小時，而且 hello 使用者將則是可以 tooreset 其密碼。 |
| 使用者在驗證其電話號碼時看到錯誤 | 輸入 hello 電話號碼與 hello 檔案上的電話號碼不相符時，就會發生此錯誤。 請確定 hello 使用者輸入 hello 完整的電話號碼，包括區域和國家/地區的程式碼，當嘗試 toouse 密碼重設的電話式方法。 |
| 處理要求時發生錯誤 | 許多問題都會造成此情形，但這個錯誤通常是因為服務中斷或設定問題所導致。 如果您看到這個錯誤，而且它會影響您的業務，請連絡 Microsoft 支援服務人員以尋求其他協助。 |

## <a name="troubleshoot-password-writeback"></a>針對密碼回寫進行疑難排解

| **錯誤** | 方案 |
| --- | --- |
| 密碼重設服務無法啟動在內部部署錯誤 6800 hello Azure AD Connect 機器的應用程式事件記錄檔中。 <br> <br> 上架之後，同盟或密碼雜湊同步使用者無法重設其密碼。 | 啟用密碼回寫時，hello 同步處理引擎會呼叫與 toohello 雲端上線服務的 hello 回寫文件庫 tooperform hello 組態 （上線）。 在上線期間或啟動密碼回寫結果的 hello WCF 端點在 Azure AD Connect 機器的事件記錄檔中的 hello 事件記錄檔中的錯誤時所發生的任何錯誤。 <br> <br> 在 ADSync 服務重新啟動，如果已設定回寫，hello WCF 端點會啟動。 不過，如果 hello hello 端點啟動失敗，我們會記錄事件 6800，並讓 hello 同步處理服務啟動。 出現這個事件表示該 hello 密碼回寫端點未啟動。 事件記錄檔詳細資料，這個事件 (6800) 事件記錄項目產生的 PasswordResetService 元件指出為什麼 hello 端點無法啟動。 檢閱這些事件記錄檔錯誤，並再試一次 toorestart hello Azure AD Connect，如果密碼回寫仍然無法運作。 如果 hello 問題持續發生，請嘗試 toodisable，然後重新啟用密碼回寫。
| 當使用者嘗試 tooreset 密碼或解除鎖定帳戶，以啟用密碼回寫時，hello 作業失敗。 <br> <br> 此外，您會看到事件 hello Azure AD Connect 的事件記錄檔包含: 「 同步處理引擎會傳回錯誤 hr = 800700CE，訊息 = hello 檔案名稱或副檔名太長"hello 解除鎖定作業之後，就會發生。 | 尋找 hello Active Directory 帳戶的 Azure AD Connect 並重設 hello 密碼 toocontain 不能超過 127 個字元。 從 hello [開始] 功能表，然後開啟同步處理服務。 導覽 tooConnectors 並尋找 hello Active Directory 連接器。 選取它，然後按一下 [屬性]。 瀏覽 toohello 頁面上的認證，然後輸入 hello 新密碼。 選取 [確定] tooclose hello 頁面。 |
| 在 hello 的 hello Azure AD Connect 的安裝程序的最後一個步驟，您會看到錯誤指出無法設定密碼回寫。 <br> <br> hello Azure AD Connect 應用程式事件記錄檔包含文字的錯誤 32009 「 取得驗證權杖 」。 | 在 hello 下列兩種情況下，會發生這個錯誤：<br> <br> a. 您指定了不正確 hello hello 開頭 hello Azure AD Connect 的安裝程序在指定的全域管理員帳戶的密碼。<br> b. 您嘗試的 toouse hello 全域管理員帳戶的同盟的使用者指定在 hello 開頭 hello Azure AD Connect 的安裝程序。<br> <br> toofix 這個錯誤，請確認您使用不是同盟的帳戶 hello 開頭 hello hello Azure AD Connect 安裝程序，您指定的全域管理員，然後指定該 hello 密碼是否正確。 |
| hello Azure AD Connect 電腦事件記錄檔包含 hello PasswordResetService 所擲回的 32002 錯誤。 <br> <br> hello 錯誤為: 「 連線 tooServiceBus 時發生錯誤，hello 權杖提供者是否無法 tooprovide 安全性權杖...」 | 您在內部部署的環境不能 tooconnect toohello 服務匯流排端點 hello 雲端中。 這個錯誤通常是封鎖輸出連線 tooa 特定連接埠或網址的防火牆規則所造成。 如需詳細資訊，請參閱[網路需求](active-directory-passwords-how-it-works.md#network-requirements)。 一旦您已更新這些規則，重新開機 hello Azure AD Connect 機器及密碼回寫應該再次開始工作。 |
| 在運作一段時間後，同盟或密碼雜湊同步使用者無法重設其密碼。 | 在某些罕見的情況下，hello 密碼回寫服務可能會失敗 toorestart 時重新啟動 Azure AD Connect。 在這些情況下，首先，檢查是否顯示 toobe 啟用內部部署密碼回寫 這可以使用 hello Azure AD Connect 精靈或 powershell （請參閱來上面）。如果 hello 功能出現 toobe 啟用，請再試一次啟用或停用 hello 功能一次透過 hello UI 或 PowerShell。 如果這麼做沒有效，請嘗試完整解除安裝再重新安裝 Azure AD Connect。 |
| 同盟或密碼雜湊同步處理嘗試的 tooreset 其密碼會送出 hello 密碼有指出發生服務問題之後，請參閱錯誤的使用者。 <br ><br> 此外 toothis，在密碼重設作業，您可能會看到關於管理代理程式錯誤與您在內部部署事件記錄檔中的存取遭拒。 | 如果您的事件記錄檔中看到這些錯誤，請確認該 hello AD MA 帳戶 （精靈中所指定 hello 次組態的 hello） 有 hello 密碼回寫的必要權限。 <br> <br> **之後指定此權限，就可以在 hello 權限 tootrickle too1 小時向下透過 sdprop 背景工作上 hello DC。** <br> <br> 密碼重設 toowork，hello 權限需要 toobe hello 安全性描述元重設其密碼，則 hello 使用者物件上加上戳記。 之前 hello 使用者物件上出現此權限，密碼重設會繼續 toofail 因存取遭拒絕。 |
| 同盟或密碼雜湊同步處理嘗試的 tooreset 其密碼會送出 hello 密碼有指出發生服務問題之後，請參閱錯誤的使用者。 <br> <br> 此外 toothis，在密碼重設作業，您可能會看到錯誤 hello Azure AD Connect 服務 」 物件找不到 」 錯誤，指出從事件記錄檔中。 | 此錯誤通常表示該 hello 同步處理引擎為無法 toofind hello hello AAD 連接器空間中的使用者物件或 hello 連結的 MV 或 AD 連接器空間物件。 <br> <br> tootroubleshoot，請確定該 hello 使用者確實從內部 tooAAD 透過 hello 目前執行個體的 Azure AD Connect 同步處理，並檢查 hello hello 連接器空間和 MV 中的 hello 物件的狀態。 確認該 hello AD CS 物件連接器 toohello MV 物件透過 hello"Microsoft.InfromADUserAccountEnabled.xxx"規則。|
| 同盟或密碼雜湊同步處理嘗試的 tooreset 其密碼會送出 hello 密碼有指出發生服務問題之後，請參閱錯誤的使用者。 <br> <br> 此外 toothis，在密碼重設作業，您可能會看到錯誤指出 「 找到多個相符 」 錯誤 hello Azure AD Connect 服務從事件記錄檔中。 | 這表示該 hello 同步處理引擎偵測到該 hello MV 物件連接的 toomore 比透過"Microsoft.InfromADUserAccountEnabled.xxx"hello 一個 AD CS 物件。 這表示該 hello 使用者有多個樹系中已啟用的帳戶。 **密碼回寫不支援此案例。** |
| 密碼作業因設定錯誤而失敗。 hello 應用程式事件記錄檔包含 <br> <br> Azure AD Connect 錯誤 6329 文字： 0x8023061f （hello 作業失敗，因為此管理代理程式未啟用密碼同步處理）。 | 發生這種情況的新 AD 樹系 （或 tooremove 和出現有的樹系） 之後 hello Azure AD Connect 設定是否已變更的 tooadd hello 功能已啟用密碼回寫。 位於這類新增樹系中的使用者，其密碼作業會失敗。 toofix hello 問題，請停用然後重新啟用 hello 密碼回寫功能，完成 hello 樹系組態變更。 |

## <a name="password-writeback-event-log-error-codes"></a>密碼回寫事件記錄檔錯誤碼

疑難排解密碼回寫問題的最佳作法是您 Azure AD Connect 的電腦的應用程式事件記錄檔的 tooinspect。 這個事件記錄包含密碼回寫的兩個相關來源的事件。 hello PasswordResetService 來源描述作業和問題相關的 toohello 作業密碼回寫。 hello ADSync 來源描述作業和 AD 環境中的問題相關的 toosetting 密碼。

### <a name="source-of-event-is-adsync"></a>事件來源為 ADSync

| 代碼 | 名稱/訊息 | 說明 |
| --- | --- | --- |
| 6329 | 釋出： MMS(4924) 0x80230619 – 「 限制可防止 hello 進行密碼變更 toohello 目前指定的其中一個。 」 | Hello 密碼回寫服務嘗試 tooset hello 密碼有效期、 歷程記錄、 複雜性或篩選需求 hello 網域不符合您的本機目錄上的密碼時，就會發生此事件。 <br> <br> 如果您有密碼最小保留期限，以及最近有變更視窗的時間內的 hello 密碼時，您不能 toochange hello 密碼再次直到達到指定的 hello 最長使用期限您的網域。 為了測試用途，最短使用期限應該設定 too0。 <br> <br> 如果您有啟用，密碼歷程記錄需求，則您必須選取已不用於 hello 最後 N 次，其中 N 是 hello 密碼歷程記錄的密碼設定。 如果您選取已用於 hello 最後 N 次，密碼就會在此情況下看到失敗。 為了測試用途，歷程記錄應該設定 too0。 <br> <br> 如果您有密碼複雜性需求，全部都 hello 使用者嘗試 toochange 時，會強制執行，或重設密碼。 <br> <br> 如果您啟用密碼篩選，而且使用者選取的密碼不符合篩選準則的 hello，然後 hello 重設或變更作業將會失敗。 |
| HR 8023042 | 同步處理引擎會傳回錯誤 hr = 80230402，訊息 = 物件失敗，因為有重複的項目以 hello 嘗試 tooget 相同錨點 | 此事件發生於 hello 多個網域中啟用相同的使用者識別碼。 例如，如果您正在同步處理帳戶/資源樹系，且有 hello 同一個使用者 id 存在且已啟用在每一個，這項錯誤可能會發生。 <br> <br> 如果您使用非唯一的錨點屬性 (例如別名或 UPN)，而且兩個使用者共用該相同的錨點屬性時，也會發生此錯誤。 <br> <br> tooresolve 這個問題，請確定，您不需要任何重複的使用者網域內，而且每個使用者使用唯一的錨點屬性。 |

### <a name="source-of-event-is-passwordresetservice"></a>事件來源為 PasswordResetService

| 代碼 | 名稱/訊息 | 說明 |
| --- | --- | --- |
| 31001 | PasswordResetStart | 這個事件表示 hello 在內部部署服務偵測到密碼重設源自 hello 雲端同盟或密碼雜湊同步處理使用者要求。 此事件是 hello 第一個事件中每個密碼重設回寫作業。 |
| 31002 | PasswordResetSuccess | 這個事件表示，使用者密碼重設作業期間選取新的密碼、 我們認為這個密碼符合公司的密碼需求，而且該密碼已經成功地寫回 toohello 本機 AD 環境。 |
| 31003 | PasswordResetFail | 此事件表示使用者選取的密碼，並，密碼已成功送達 toohello 在內部部署環境中，但是當我們嘗試 tooset hello 本機 AD 環境中的 hello 密碼時，發生失敗。 此狀況有幾個可能原因： <br> <br> hello 使用者的密碼不符合 hello 年齡、 歷程記錄、 複雜性或篩選需求 hello 網域。 試試這個全新的密碼 tooresolve。 <br> <br> hello MA 服務帳戶沒有 hello 使用者帳戶有問題的 hello 適當的權限 tooset hello 新密碼。 <br> <br> hello 使用者帳戶是在受保護的群組中，例如網域或 enterprise admins，不允許密碼設定作業。 |
| 31004 | OnboardingEventStart | 如果您啟用密碼回寫，使用 Azure AD Connect，就會發生此事件，而且表示我們開始入門訓練您的組織 toohello 密碼回寫 web 服務。 |
| 31005 | OnboardingEventSuccess | 這個事件表示 hello 上架程序成功，密碼回寫功能是準備 toouse。 |
| 31006 | ChangePasswordStart | 這個事件表示 hello 在內部部署服務偵測到來自 hello 雲端的同盟或密碼雜湊同步處理使用者的密碼變更要求。 此事件是每個密碼變更回寫作業中的 hello 第一個事件。 |
| 31007 | ChangePasswordSuccess | 此事件表示使用者在密碼變更作業期間選取新的密碼，我們認為這個密碼符合公司的密碼需求，而且該密碼已經成功地寫回 toohello 本機 AD 環境。 |
| 31008 | ChangePasswordFail | 此事件表示使用者選取的密碼，並，密碼已成功送達 toohello 在內部部署環境中，但是當我們嘗試 tooset hello 本機 AD 環境中的 hello 密碼時，發生失敗。 此狀況有幾個可能原因： <br> <br> hello 使用者的密碼不符合 hello 年齡、 歷程記錄、 複雜性或篩選需求 hello 網域。 試試這個全新的密碼 tooresolve。 <br> <br> hello MA 服務帳戶沒有 hello 使用者帳戶有問題的 hello 適當的權限 tooset hello 新密碼。 <br> <br> hello 使用者帳戶是在受保護的群組中，例如網域或 enterprise admins，不允許密碼設定作業。 |
| 31009 | ResetUserPasswordByAdminStart | hello 在內部部署服務偵測到密碼重設源自 hello 系統管理員代表使用者的同盟或密碼雜湊同步處理使用者要求。 這個事件是每個系統管理員起始密碼重設回寫作業中的 hello 第一個事件。 |
| 31010 | ResetUserPasswordByAdminSuccess | hello 管理系統管理員起始密碼重設作業期間選取新的密碼、 我們認為這個密碼符合公司的密碼需求，而且該密碼已經成功地寫回 toohello 本機 AD 環境。 |
| 31011 | ResetUserPasswordByAdminFail | hello 系統管理員代表使用者，選取密碼和密碼已成功送達 toohello 在內部部署環境中，但是當我們嘗試 tooset hello 本機 AD 環境中的 hello 密碼時，發生失敗。 此狀況有幾個可能原因： <br> <br> hello 使用者的密碼不符合 hello 年齡、 歷程記錄、 複雜性或篩選需求 hello 網域。 試試這個全新的密碼 tooresolve。 <br> <br> hello MA 服務帳戶沒有 hello 使用者帳戶有問題的 hello 適當的權限 tooset hello 新密碼。 <br> <br> hello 使用者帳戶是在受保護的群組中，例如網域或 enterprise admins，不允許密碼設定作業。 |
| 31012 | OffboardingEventStart | 如果您停用密碼回寫，使用 Azure AD Connect，就會發生此事件，而且表示，我們已開始終止您的組織 toohello 密碼回寫 web 服務。 |
| 31013| OffboardingEventSuccess| 這個事件表示 hello 終止程序成功，並確認密碼回寫功能已成功停用。 |
| 31014| OffboardingEventFail| 這個事件表示 hello 終止程序不成功。 這可能是由於 tooa hello 雲端或內部部署系統管理員帳戶在設定期間，指定的權限錯誤，或因為停用密碼回寫時，會嘗試 toouse 同盟的雲端全域管理員。 toofix，檢查您的系統管理權限，且您不使用任何同盟帳戶時設定 hello 密碼回寫功能。|
| 31015| WriteBackServiceStarted| 這個事件表示該 hello 密碼回寫服務已順利啟動，且準備好 tooaccept 密碼管理要求從 hello 雲端。|
| 31016| WriteBackServiceStopped| 這個事件表示 hello 密碼回寫服務已停止，並從 hello 雲端任何密碼管理要求將不會成功。|
| 31017| AuthTokenSuccess| 這個事件表示我們成功擷取 hello Azure AD Connect 設定 toostart hello 終止或上線程序期間所指定的全域管理員的授權權杖。|
| 31018| KeyPairCreationSuccess| 這個事件表示我們成功建立是使用的 tooencrypt 密碼從 hello 雲端 toobe 傳送 tooyour 在內部部署環境的 hello 密碼加密金鑰。|
| 32000| UnknownError| 這個事件表示密碼管理作業期間發生未知的錯誤。 查看更多詳細資料的 hello 事件中的 hello 例外狀況文字。 如果您遇到問題，請嘗試停用再重新啟用密碼回寫。 如果沒有用，包括事件記錄檔，以及追蹤識別碼指定的測試人員 tooyour 支援工程師 hello 複本。|
| 32001| ServiceError| 此事件表示時發生錯誤連接 toohello 雲端密碼重設服務，而且通常會發生 hello 在內部部署服務時無法 tooconnect toohello 密碼重設 web 服務。|
| 32002| ServiceBusError| 這個事件表示連接 tooyour 租用戶的服務匯流排執行個體時發生錯誤。 可能原因是您在內部部署環境中封鎖了輸出連線。 請檢查您的防火牆 tooensure 您透過 TCP 443 和 toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/，允許連線並再試一次。 如果仍遇到問題，請嘗試停用再重新啟用密碼回寫。|
| 32003| InPutValidationError| 這個事件表示傳遞 tooour web 服務 API 的 hello 輸入無效。 Hello 再次嘗試操作。|
| 32004| DecryptionError| 這個事件表示已從 hello 雲端抵達的 hello 密碼解密時發生錯誤。 這可能是因為解密金鑰不相符 hello 雲端服務與內部部署環境之間。 tooresolve 這個停用及重新啟用密碼回寫內部部署環境中。|
| 32005| ConfigurationError| 上架期間，我們將租用戶特定的資訊儲存在內部部署環境的設定檔中。 這個事件表示發生錯誤時啟動 hello 服務時無法儲存這個檔案，或是已讀取 hello 檔時發生錯誤。 toofix 此問題，請嘗試停用並重新啟用密碼回寫 tooforce 重寫此組態檔。|
| 32007| OnBoardingConfigUpdateError| 在上線期間，我們會傳送 hello 雲端 toohello 資料內部部署密碼重設服務。 Tooan 記憶體檔案，才能傳送 toohello 同步處理服務 toostore 安全地在磁碟上的這項資訊，然後寫入該資料。 這個事件表示在記憶體中寫入或更新該資料時發生問題。 toofix 此問題，請嘗試停用並重新啟用密碼回寫 tooforce 重寫這項設定。|
| 32008| ValidationError| 這個事件表示我們從 hello 密碼重設 web 服務收到無效的回應。 toofix 此問題，請嘗試停用並重新啟用密碼回寫。|
| 32009| AuthTokenError| 這個事件表示，我們無法取得授權權杖 hello 全域管理員帳戶在 Azure AD Connect 的安裝期間指定。 這個錯誤可能因不正確的使用者名稱或密碼 hello 全域系統管理員帳戶指定的帳戶，或因為 hello 全域管理員帳戶指定為同盟。 toofix 這個問題，請重新執行組態 hello 更正使用者名稱和密碼，並確認 hello 系統管理員 （僅限雲端或密碼同步處理） 的受管理的帳戶。|
| 32010| CryptoError| 這個事件表示有錯誤發生時產生 hello 密碼加密金鑰或解密從 hello 雲端服務的密碼。 此錯誤可能表示您的環境有問題。 查看更多程式事件記錄檔 toolearn hello 詳細資料，並解決此問題。 您也可以此嘗試停用再重新啟用 hello 密碼回寫服務 tooresolve。|
| 32011| OnBoardingServiceError| 這個事件表示 hello 在內部部署服務無法正常通訊與 hello 密碼重設 web 服務 tooinitiate hello 上架程序。 這可能是因為有防火牆規則或是取得租用戶的授權權杖時發生問題。 toofix，請確認您並未封鎖輸出連線透過 TCP 443 或 TCP 9350-9354 toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/，且該 hello 使用 tooonboard 的 AAD 系統管理員帳戶不同盟。|
| 32013| OffBoardingError| 這個事件表示 hello 在內部部署服務無法正常通訊與 hello 密碼重設 web 服務 tooinitiate hello 終止程序。 這可能是因為有防火牆規則或是取得租用戶的授權權杖時發生問題。 toofix，請確認您並未封鎖透過 443 或 toohttps://ssprsbprodncu-sb.accesscontrol.windows.net/，輸出連線，且該 hello 使用 toooffboard 的 AAD 系統管理員帳戶不同盟。|
| 32014| ServiceBusWarning| 這個事件表示我們必須 tooretry tooconnect tooyour 租用戶的服務匯流排執行個體。 在正常情況下，這應該不是個問題，但如果您看到此事件很多次，請考慮檢查您的網路連線 tooservice 匯流排，特別是如果它是高度延遲或低頻寬連線。|
| 32015| ReportServiceHealthError| 在順序的密碼回寫服務的 toomonitor hello 健全狀況，我們會傳送活動訊號資料 tooour 密碼重設 web 服務每隔 5 分鐘。 這個事件表示，有錯誤發生時傳送此健全狀況資訊後 toohello 雲端 web 服務。 此健全狀況資訊不包含 OII 或 PII 資料，並完全活動訊號和基本服務統計資料，讓我們能夠提供 hello 雲端中的服務狀態資訊。|
| 33001| ADUnKnownError| 這個事件表示已由 AD 傳回未知的錯誤，請檢查 hello Azure AD Connect 伺服器事件日誌以取得有關此錯誤更多資訊 hello ADSync 來源中的事件。|
| 33002| ADUserNotFoundError| 這個事件表示該 hello 的使用者正在嘗試 tooreset 或 hello 在內部部署目錄中找不到密碼的變更。 這可能是已刪除在內部部署 hello 使用者時，但不是在 hello 雲端，或如果沒有同步處理發生問題。檢查您同步處理記錄檔，以及上次 hello 一些執行同步處理的詳細資訊，如需詳細資訊。|
| 33003| ADMutliMatchError| 當密碼重設或變更要求源自 hello 雲端時，我們使用 hello 雲端錨點指定的 Azure AD Connect toodetermine hello 安裝程序期間如何 toolink 要求後 tooa 使用者在內部部署環境中的。 這個事件表示我們在 hello 與您在內部部署目錄中發現兩位使用者相同雲端錨點屬性。 檢查您同步處理記錄檔，以及上次 hello 一些執行同步處理的詳細資訊，如需詳細資訊。|
| 33004| ADPermissionsError| 這個事件表示該 hello 管理代理程式服務帳戶沒有 hello 適當權限 hello 帳戶有問題的 tooset 新的密碼。 請確定該 hello hello 使用者樹系中的 MA 帳戶擁有 hello 樹系中的所有物件重設及變更密碼權限。 如需有關如何 toothis 的詳細資訊，請參閱步驟 4： 設定 hello 適當的 Active Directory 權限。|
| 33005| ADUserAccountDisabled| 這個事件表示我們嘗試 tooreset，或變更已停用在內部部署帳戶的密碼。 啟用 hello 帳戶，然後再次嘗試 hello 操作。|
| 33006| ADUserAccountLockedOut| 事件表示我們嘗試 tooreset 或變更已被鎖定在內部部署帳戶的密碼。 當使用者在短時間內嘗試進行變更或重設密碼作業太多次，就可能發生鎖定。 Hello 帳戶解除鎖定，然後再試一次 hello 作業。|
| 33007| ADUserIncorrectPassword| 這個事件表示該 hello 使用者執行密碼變更作業時，請指定不正確的目前密碼。 指定 hello 正確的目前密碼並再試一次。|
| 33008| ADPasswordPolicyError| Hello 密碼回寫服務嘗試 tooset hello 密碼有效期、 歷程記錄、 複雜性或篩選需求 hello 網域不符合您的本機目錄上的密碼時，就會發生此事件。 <br> <br> 如果您有密碼最小保留期限，以及最近有變更視窗的時間內的 hello 密碼時，您不能 toochange hello 密碼再次直到達到指定的 hello 最長使用期限您的網域。 為了測試用途，最短使用期限應該設定 too0。 <br> <br> 如果您有啟用，密碼歷程記錄需求，則您必須選取已不用於 hello 最後 N 次，其中 N 是 hello 密碼歷程記錄的密碼設定。 如果您選取已用於 hello 最後 N 次，密碼就會在此情況下看到失敗。 為了測試用途，歷程記錄應該設定 too0。 <br> <br> 如果您有密碼複雜性需求，全部都 hello 使用者嘗試 toochange 時，會強制執行，或重設密碼。 <br> <br> 如果您啟用密碼篩選，而且使用者選取的密碼不符合篩選準則的 hello，然後 hello 重設或變更作業將會失敗。|
| 33009| ADConfigurationError| 這個事件表示撰寫密碼後 tooyour 內部部署與 Active Directory tooa 組態問題到期目錄發生問題。 檢查來自 hello ADSync 服務，如需有關所發生之錯誤的訊息的 hello Azure AD Connect 機器的應用程式事件記錄檔。|


## <a name="troubleshoot-password-writeback-connectivity"></a>疑難排解密碼回寫連線

如果您遇到的 Azure AD Connect 與 hello 密碼回寫元件的服務中斷，這裡有一些您可以將 tooresolve 此的快速步驟：

* [重新啟動 hello Azure AD Connect 同步處理服務](#restart-the-azure-ad-connect-sync-service)
* [停用再重新啟用 hello 密碼回寫功能](#disable-and-re-enable-the-password-writeback-feature)
* [安裝 hello 最新的 Azure AD Connect 版本](#install-the-latest-azure-ad-connect-release)
* [疑難排解密碼回寫](#troubleshoot-password-writeback)

一般情況下，我們建議您執行下列步驟順序上方 toorecover hello 您的服務 hello 最快速的方式。

### <a name="restart-hello-azure-ad-connect-sync-service"></a>重新啟動 hello Azure AD Connect 同步處理服務

重新啟動 hello Azure AD Connect 同步服務有助於 tooresolve 連線問題或其他 hello 服務的暫時性問題。

1. 身為管理員，按一下 **啟動**hello 執行的伺服器上**Azure AD Connect**。
2. 型別**"services.msc"**在 hello 搜尋方塊，然後按**Enter**。
3. 尋找 hello **Microsoft Azure AD Sync**項目。
4. Hello 服務項目上按一下滑鼠右鍵，按一下**重新啟動**，並等候 hello 作業 toocomplete。

   ![重新啟動 hello Azure AD 同步服務][Service Restart]

下列步驟重新建立您的連接與 hello 雲端服務，並解決任何您可能會遇到的干擾。 如果重新啟動 hello 同步處理服務無法解決您的問題，我們建議您 toodisable 再試一次，並重新啟用 hello 密碼回寫功能做為下一個步驟。

### <a name="disable-and-re-enable-hello-password-writeback-feature"></a>停用再重新啟用 hello 密碼回寫功能

停用並重新啟用 hello 密碼回寫功能可協助 tooresolve 連線問題。

1. 身為管理員，開啟 hello **Azure AD Connect 設定精靈**。
2. 在 [hello**連接 tooAzure AD** ] 對話方塊中，輸入您**Azure AD 全域管理員認證**
3. 在 [hello**連接 tooAD DS** ] 對話方塊中，輸入您**AD 網域服務的系統管理員認證**。
4. 在 hello**用來唯一識別您的使用者** 對話方塊中，按一下 hello**下一步**按鈕。
5. 在 hello**選用功能** 對話方塊中，取消核取 hello**密碼回寫**核取方塊。
6. 按一下**下一步**透過 hello 剩餘對話方塊頁面，而不需要變更任何項目，直到取得 toohello**準備 tooconfigure**頁面。
7. 請確定該 hello 設定頁面會顯示 hello**為停用密碼回寫選項**然後按一下綠色的 hello**設定**按鈕 toocommit 您的變更。
8. 在 [hello**已經完成**] 對話方塊中，取消選取 hello**立即同步處理**選項，然後再按一下**完成**tooclose hello 精靈。
9. 重新開啟 hello **Azure AD Connect 設定精靈**。
10. **重複步驟 2-8**，期間請您務必**檢查 hello 密碼回寫選項**上 hello**選用功能**畫面 toore 啟用 hello 服務。

這些步驟會重新建立您與雲端服務的連線，解決您可能會遇到的中斷問題。

如果停用再重新啟用 hello 密碼回寫功能無法解決您的問題，我們建議您嘗試 tooreinstall 為下一個步驟的 Azure AD Connect。

### <a name="install-hello-latest-azure-ad-connect-release"></a>安裝 hello 最新的 Azure AD Connect 版本

重新安裝 Azure AD Connect 可以解決我們的雲端服務和您的本機 AD 環境之間的設定和連線問題。

我們建議，請嘗試 hello 上面所述的前兩個步驟之後，才執行此步驟。

> [!WARNING]
> 如果您已自訂方塊同步處理規則，超出 hello**這些備份再繼續執行升級，並手動將其重新佈署在完成之後**。

1. 從 hello 下載 hello 最新版本的 Azure AD Connect [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771)。
2. 由於您已安裝 Azure AD Connect，您必須 tooperform 就地升級 tooupdate 您 Azure AD Connect 安裝 toohello 最新版本。
3. 執行 hello 下載封裝，並遵循螢幕上指示 tooupdate hello 您 Azure AD Connect 的電腦。

這些步驟會重新建立您與雲端服務的連線，解決您可能會遇到的任何中斷問題。

如果安裝的 hello 最新版本的 hello Azure AD Connect 的伺服器無法解決您的問題，我們建議您嘗試停用再重新啟用密碼回寫最後一個步驟是安裝 hello 最新版本之後。

## <a name="verify-whether-azure-ad-connect-has-hello-required-permission-for-password-writeback"></a>驗證 Azure AD Connect 是否具有密碼回寫 hello 所需權限 
Azure AD Connect 需要 AD**重設密碼**權限 tooperform 密碼回寫。 如果 toofind Azure AD Connect 具有 hello 權限指定的內部部署 AD 使用者帳戶，您可以使用 hello Windows 的有效權限功能：

1. 登入 tooAzure AD 連線伺服器並啟動 hello**同步處理服務管理員**（→ 開始同步處理服務）。
2. 在 hello**連接器**索引標籤上，選取 hello 內部**AD 連接器**按一下**屬性**。  
![有效權限 - 步驟 2](./media/active-directory-passwords-troubleshoot/checkpermission01.png)  
3. 在 hello 快顯對話方塊中，選取 [hello**連接 tooActive Directory 樹系**] 索引標籤並記下 hello**使用者名**屬性。 這是 Azure AD Connect tooperform 目錄同步處理所使用的 hello AD DS 帳戶。 Azure AD Connect tooperform 密碼回寫 hello AD DS 帳戶必須重設密碼權限。  
![有效權限 - 步驟 3](./media/active-directory-passwords-troubleshoot/checkpermission02.png)  
4. 登入 tooan 內部部署網域控制站並開始 hello **Active Directory 使用者和電腦**應用程式。
5. 按一下 [檢視]，並確定 [進階功能] 選項已啟用。  
![有效權限 - 步驟 5](./media/active-directory-passwords-troubleshoot/checkpermission03.png)  
6. 尋找 hello 想 tooverify AD 使用者帳戶。 Hello 帳戶上按一下滑鼠右鍵，然後選取**屬性**。  
![有效權限 - 步驟 6](./media/active-directory-passwords-troubleshoot/checkpermission04.png)  
7. 在 hello 快顯對話方塊中，移 toohello**安全性**索引標籤上，按一下 **進階**。  
![有效權限 - 步驟 7](./media/active-directory-passwords-troubleshoot/checkpermission05.png)  
8. 在 [hello 進階安全性設定快顯對話方塊中，移 toohello**有效存取權**] 索引標籤。
9. 按一下**選取使用者**，選取 使用 Azure AD Connect 的 hello AD DS 帳戶 （請參閱步驟 3）。 然後按一下 [檢視有效存取權]。  
![有效權限 - 步驟 9](./media/active-directory-passwords-troubleshoot/checkpermission06.png)  
10. 向下捲動並尋找 [重設密碼]。 如果勾選 hello 項目，則表示 hello AD DS 帳戶具有權限的 hello tooreset hello 密碼已選取 AD 使用者帳戶。  
![有效權限 - 步驟 10](./media/active-directory-passwords-troubleshoot/checkpermission07.png)  

## <a name="azure-ad-forums"></a>Azure AD 論壇

如果您有關於 Azure AD 的一般問題和自助式密碼重設，您可以要求 hello 社群協助在 hello [Azure AD 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)。 Hello 社群的成員包括工程師，產品經理、 professional，Mvp 和夥伴 IT 專業人員。

## <a name="contact-microsoft-support"></a>連絡 Microsoft 支援

如果找不到 hello 回應 tooan 問題我們的支援團隊一律會使用 tooassist 您進一步。

tooproperly 協助，我們會要求您提供儘可能詳細資料時開啟案例包括：

* **Hello 錯誤的一般描述**-什麼是 hello 錯誤？ 發現的 hello 行為是什麼？ 我們可以重現 hello 錯誤？ 請提供盡可能詳細的資料。
* **頁面**-哪一頁，您您注意到 hello 錯誤？ 請如果您無法 tooand 螢幕擷取畫面，附上 hello URL。
* **支援的程式碼**-hello 使用者看到 hello 錯誤時產生的 hello 支援程式碼是什麼？ 
    * toofind 這重現 hello 錯誤，然後按一下 hello 支援程式碼在 hello 囉 」 畫面底部的連結和傳送嗨支援工程師 hello 所產生的 GUID。
    ![尋找在 hello 囉 」 畫面底部的 hello 支援程式碼][Support Code]
    * 如果您是在沒有支援代碼 hello 底部 頁面上，按 F12，並搜尋 SID 和 CID，並傳送這些兩個結果 toohello 支援工程師。
* **日期、 時間和時區**-請附上 hello 確切的日期和時間**與 hello 時區**hello 錯誤發生。
* **使用者識別碼**位人員被 hello 使用者看到 hello 錯誤？ (user@contoso.com)
    * 這是同盟使用者嗎？
    * 這是密碼雜湊同步使用者嗎？
    * 這是僅限雲端的使用者嗎？
* **授權**-hello 使用者是否獲指派 Azure AD Premium 或 Azure AD Basic 授權？
* **應用程式事件記錄檔**-如果您使用密碼回寫，而且 hello 錯誤是在您的內部部署基礎結構，包括從 hello Azure AD Connect 的伺服器應用程式事件記錄檔的壓縮的複本時連絡支援人員。

    

[Service Restart]: ./media/active-directory-passwords-troubleshoot/servicerestart.png "重新啟動 hello Azure AD 同步服務"
[Support Code]: ./media/active-directory-passwords-troubleshoot/supportcode.png "支援的程式碼位於 hello 右下方的 hello 視窗"

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
