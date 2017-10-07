---
title: "aaaAzure Multi-factor Authentication 常見問題集 |Microsoft 文件"
description: "常見問題集與答案相關 tooAzure Multi-factor Authentication。 Multi-Factor Authentication 是一種驗證使用者身分識別的方法。它除了需要使用者名稱與密碼之外，還需要其他驗證方式。 它提供額外的安全性 toouser 登入和交易。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>與 Azure Multi-Factor Authentication 相關的常見問題
此常見問題集回答有關 Azure Multi-factor Authentication 和使用 hello Multi-factor Authentication 服務的常見問題。 它是分解為 hello 服務有關的問題一般情況下，計費模型中，使用者體驗和疑難排解。

## <a name="general"></a>一般
**問：Azure Multi-Factor Authentication Server 如何處理使用者資料？**

Multi-factor Authentication Server，使用者資料儲存只能在 hello 在內部部署伺服器上。 Hello 雲端中不儲存任何持續性的使用者資料。 當 hello 使用者執行雙步驟驗證時，Multi-factor Authentication Server 會傳送資料 toohello Azure Multi-factor Authentication 雲端服務進行驗證。 Multi-factor Authentication Server 與 hello Multi-factor Authentication 雲端服務之間的通訊會透過連接埠 443 輸出使用安全通訊端層 (SSL) 或傳輸層安全性 (TLS)。

當驗證要求傳送 toohello 雲端服務時，收集資料進行驗證和使用方式報表。 雙步驟驗證記錄檔中包含的資料欄位如下：

* **唯一識別碼** (使用者名稱或內部部署 Multi-Factor Authentication Server 識別碼兩者之一)
* **名字和姓氏** (選擇性)
* **電子郵件地址** (選擇性)
* **電話號碼** (進行語音通話或簡訊驗證時)
* **裝置權杖** (執行行動應用程式驗證時)
* **驗證模式**
* **驗證結果**
* **Multi-Factor Authentication Server 名稱**
* **Multi-Factor Authentication Server IP**
* **用戶端 IP** (如果有的話)

可以在 Multi-factor Authentication Server 中設定 hello 選擇性欄位。

hello 驗證結果 （成功或拒絕），而 hello 原因如果它被拒，會儲存與 hello 驗證資料。 可在驗證和使用方式報告中取得此資料。

## <a name="billing"></a>計費
大部分帳單的問題可以藉由參考 tooeither hello 回應[多因素驗證定價頁面](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)或 hello 文件中的有關[如何 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)。

**問： 是否需支付傳送 hello 電話及簡訊驗證會使用我的組織？**

否，則不需收費放置個別的電話或簡訊傳送 toousers 透過 Azure 多重要素驗證。 如果您使用的每個驗證 MFA 提供者，您需要付費每個驗證，但不適用於使用 hello 方法。

您的使用者可能必須支付 hello 電話或簡訊收到，相應 tootheir 個人電話服務。

**問 hello 每位使用者計費模型收取我所有啟用的使用者或只是 hello 執行雙步驟驗證的項目嗎？**

計費根據使用者設定 toouse Multi-factor Authentication，不論它們是否執行雙步驟驗證該月份的 hello 數目。

**問：Multi-Factor Authentication 是如何計費？**

當您建立每個使用者或每個授權的 MFA 提供者時，貴組織的 Azure 訂用帳戶會以使用方式每個月計費作為基礎。 這個計費的模型很類似的虛擬機器和網站的使用方式的 toohow Azure 帳單金額。

當您購買訂用帳戶的 Azure Multi-factor Authentication 時，您的組織只支付 hello 年授權費的每位使用者。 MFA 授權和 Office 365、Azure AD Premium 或 Enterprise Mobility + Security 組合會以這種方式計費。 

深入了解您的選項[如何 tooget Azure Multi-factor Authentication](multi-factor-authentication-versions-plans.md)。

**問：是否有免費版本的 Azure Multi-Factor Authentication？**

在某些情況下，是的。

Azure 系統管理員的多重要素驗證提供的免費存取的 Azure MFA 功能子集 tooMicrosoft 線上服務，包括 hello Azure 和 Office 365 系統管理員入口網站。 這項優惠僅適用於 tooglobal 沒有 hello 完整版的 Azure MFA 透過 MFA 授權、 組合或獨立耗用量為基礎提供者的 Azure Active Directory 執行個體中的系統管理員。 如果您的系統管理員使用 hello 免費版本，然後您購買完整版的 Azure MFA 時，所有全域管理員會自動付費版本的 toohello 提升權限。

Office 365 使用者的 Multi-factor Authentication 提供 tooOffice 365 服務，包括 Exchange Online 和 SharePoint Online 的存取免費的 Azure MFA 功能子集。 這項優惠適用於具有 Azure Active Directory hello 對應執行個體沒有 hello 完整版本的 Azure MFA 透過 MFA 授權、 組合或獨立耗用量為基礎提供者時指派 Office 365 授權 toousers。

**問：我的組織是否能隨時在「每位使用者」與「每次驗證」耗用量計費模式之間切換？**

如果貴組織購買的 MFA 是使用量計費型獨立服務，則您可以在建立 MFA 提供者時選擇計費模式。 建立 MFA 提供者之後，您無法變更 hello 計費模型。 不過，您可以刪除 hello MFA 提供者，然後建立一個具有不同的計費模型。

建立 MFA 提供者時，它可以是連結的 tooan Azure Active Directory （也稱為 「 Azure AD 租用戶 」）。 如果 hello 目前的 MFA 提供者是連結的 tooan Azure AD 租用戶，您就可以安全地刪除 hello MFA 提供者，並建立一個是連結的 toohello 相同的 Azure AD 租用戶。 或者，如果您購買足夠 MFA、 Azure AD Premium，或企業行動力 + 安全性 (EMS) 授權 toocover 所有使用者啟用 MFA，您可以完全刪除 hello MFA 提供者。

如果您的 MFA 提供者是*不*連結的 tooan Azure AD 租用戶，或您連結 hello 新 MFA 提供者 tooa 不同的 Azure AD 租用戶，不會傳輸使用者設定和組態選項。 此外，現有的 Azure MFA 伺服器需要重新啟動使用透過產生啟用認證 toobe hello 新的 MFA 提供者。 重新啟動 hello MFA Server toolink 它們 toohello 新的 MFA 提供者不會影響通話和簡訊驗證，但通知將會停止運作的所有使用者，直到它們重新啟用 hello 行動應用程式的行動裝置應用程式。

於[開始使用 Azure Multi-Factor Auth 提供者](multi-factor-authentication-get-started-auth-provider.md)中深入了解 MFA 提供者。

**問：我的組織是否能隨時在「根據使用量計費」和「訂用帳戶」(根據授權計費模式) 之間切換？**

在某些情況下，是的。

如果您的目錄有*根據使用者計費*的 Azure Multi-Factor Authentication 提供者，您可以新增 MFA 授權。 擁有授權的使用者不會計算在 hello 每位使用者消費型計費。 沒有授權的使用者仍然可以為 MFA 透過 hello MFA 提供者啟用。 如果您購買並指派授權給所有使用者設定 toouse Multi-factor Authentication，您可以刪除 hello Azure Multi-factor Authentication 提供者。 如果您將更多使用者授權比在 hello 未來，您一律可以建立另一位使用者的 MFA 提供者。

如果您的目錄有*每個驗證*Azure Multi-factor Authentication 提供者，只要 hello MFA 提供者是連結的 tooyour 訂用帳戶時，您會一律在每個驗證，計費。 您可以指派 MFA 授權 toousers，但您將仍然要支付每隔兩步驟驗證要求，不論其來自有人 MFA 授權指派。

**問我的組織擁有 toouse，以及同步處理身分識別 toouse Azure 多重要素驗證？**

如果貴組織使用根據使用量計費的模型，則 Azure Active Directory 為選擇性項目，並非必要。 如果您的 MFA 提供者不是連結的 tooan Azure AD 租用戶，您可以只部署 Azure Multi-factor Authentication Server 或 hello Azure Multi-factor Authentication SDK 在內部。

因為授權將會新增 toohello Azure AD 租用戶，當您購買，並將它們指派 toousers hello 目錄中的 hello 授權模型需要 azure Active Directory。

## <a name="manage-and-support-user-accounts"></a>管理和支援使用者帳戶

**問： 我應該分辨我的使用者 toodo 它們沒有收到回應其在電話上，或沒有與其電話？**

我們希望您的所有使用者並非只設定一種驗證方式。 告知 tootry 登入一次，但卻選取 hello 登入頁面上的其他驗證方法。

您可以指向使用者 toohello[使用者疑難排解指南](./end-user/multi-factor-authentication-end-user-troubleshoot.md)。


**問： 我該怎麼辦如果其中一個 我的使用者無法取得 tootheir 帳戶中？**

您可以讓它們成為 toogo 透過 hello 註冊程序一次，重設 hello 使用者帳戶。 深入了解[管理使用者和裝置設定中使用 Azure Multi-factor Authentication hello 雲端](multi-factor-authentication-manage-users-and-devices.md)。

**問：如果我的其中一個使用者遺失手機，而該手機上正在使用應用程式密碼，我該怎麼做？**

tooprevent 未經授權的存取，刪除所有 hello 使用者的應用程式密碼。 Hello 使用者具有更換裝置之後，它們可以重新建立 hello 密碼。 深入了解[管理使用者和裝置設定中使用 Azure Multi-factor Authentication hello 雲端](multi-factor-authentication-manage-users-and-devices.md)。

**問： 如果使用者無法登入 toonon 瀏覽器應用程式？**

如果您的組織仍會使用舊版用戶端，而且您[允許使用應用程式密碼的 hello](multi-factor-authentication-whats-next.md#app-passwords)，則您的使用者無法登入 toothese 舊版用戶端使用其使用者名稱和密碼。 相反地，它們需要太[設定應用程式密碼](./end-user/multi-factor-authentication-end-user-app-passwords.md)。 您的使用者必須清除 （刪除） 他們登入的資訊，重新啟動 hello 應用程式，然後再登入他們的使用者名稱和*應用程式密碼*而不是其規則的密碼。

如果您的組織沒有舊版用戶端，您應該不允許您的使用者 toocreate 應用程式密碼。

> [!NOTE]
> 適用於 Office 2013 用戶端的新式驗證
>
> 只有不支援最新驗證方式的應用程式需要應用程式密碼。 Office 2013 用戶端支援新式驗證通訊協定，但需要 toobe 設定。 新的 Office 用戶端會自動支援最新的驗證通訊協定。 如需詳細資訊，請參閱 hello [Office 2013 現代化驗證公用預覽公告](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。

**問： 我的使用者會說有時候它們不會收到 hello 文字訊息，或回覆 tootwo 單向簡訊但 hello 驗證逾時。**

不保證文字訊息的傳送和接收回覆雙向簡訊中因為有可能會影響 hello 服務的 hello 可靠性無法控制因素。 這些因素包括 hello 目的地國家/地區、 hello 行動電話服務廠商，hello 訊號強度。

如果您的使用者通常會有問題的可靠地接收文字訊息，告訴他們 toouse hello 行動應用程式或電話方法改為。 hello 行動裝置應用程式可以收到通知，同時透過電話和 Wi-fi 連線。 此外，即使 hello 裝置完全沒有訊號 hello 行動裝置應用程式可以產生驗證碼。 hello Microsoft 驗證器應用程式是供[Android](http://go.microsoft.com/fwlink/?Linkid=825072)， [IOS](http://go.microsoft.com/fwlink/?Linkid=825073)，和[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)。

如果您必須使用簡訊，則建議盡可能使用單向簡訊，而不要使用雙向簡訊。 單向 SMS 是更可靠，它可以防止使用者支付簡訊費用從信賴憑證者收到來自另一個國家/地區的 tooa 文字訊息。

**問： 是否可以變更 hello 一段時間 hello 系統逾時之前，使用者必須從簡訊 tooenter hello 驗證碼？**

在某些情況下是可以的。 

單向 SMS Azure MFA Server v7.0 或更高版本，您可以設定 hello 逾時設定所設定的登錄機碼。 Hello MFA 雲端服務會傳送 hello 文字訊息之後，hello 驗證碼 （或單次密碼） 會傳回 toohello MFA Server。 hello MFA Server 預設會將儲存 hello 程式碼中記憶體達 300 秒。 如果 hello 使用者未輸入 hello hello 前的程式碼已通過 300 秒，其驗證遭到拒絕。 使用這些步驟 toochange hello 預設逾時設定：

1. 移 tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor。
2. 建立 DWORD 登錄機碼稱為**pfsvc_pendingSmsTimeoutSeconds**和設定 hello 時間，以秒為單位的 hello Azure MFA Server toostore 單次密碼。

>[!TIP] 
>如果您有多個 MFA 伺服器時，處理 hello 原始驗證要求的其中一個 hello 知道 toohello 使用者送出 hello 驗證碼。 當 hello 使用者輸入 hello 代碼時，hello 驗證要求 toovalidate 必須將它傳送 toohello 相同的伺服器。 如果 hello 程式碼驗證傳送 tooa 不同的伺服器，hello 驗證遭到拒絕。 

使用 Azure MFA Server 雙向簡訊，您可以設定 hello 逾時設定 hello MFA 管理入口網站中。 如果使用者不 hello 定義逾時期限之內回應 toohello SMS，其驗證遭到拒絕。 

使用 Azure MFA （包括 hello AD FS 配接器或 hello 網路原則伺服器的延伸模組） 的 hello 雲端中的單向 SMS，您無法設定 hello 逾時設定。 Azure AD 會儲存 180 秒 hello 驗證碼。 

**問：我是否可以搭配 Azure Multi-Factor Authentication Server 使用硬體權杖？**

如果您正在使用 Azure Multi-Factor Authentication Server，則可以匯入協力廠商的 Open Authentication (OATH) 一次性限時密碼 (TOTP) 權杖，然後將它們用於雙步驟驗證。

您可以使用 ActiveIdentity 語彙基元，這是 TOTP OATH 權杖，如果您將 hello 祕密金鑰放在 CSV 檔案匯入 tooAzure Multi-factor Authentication Server。 只要 hello 用戶端系統可以接受 hello 使用者輸入，您可以使用 Active Directory Federation Services (ADFS)、 Internet Information Server (IIS) 表單為基礎的驗證與遠端驗證撥號使用者服務 (RADIUS) OATH 權杖。

您可以匯入協力廠商 OATH TOTP 語彙基元，以下列格式的 hello:  

- 可攜式對稱金鑰容器 (PSKC)  
- 如果 hello 檔案包含序號、 秘密金鑰基底 32 格式和時間間隔的 CSV  

**問： 是否可以使用 Azure Multi-factor Authentication Server toosecure 終端機服務？**

可以，但如果您使用的是 Windows Server 2012 R2 或更新版本，則只能使用遠端桌面閘道 (RD 閘道) 保護「終端機服務」。

Windows Server 2012 R2 中的安全性變更變更 Azure Multi-factor Authentication Server 會在 Windows Server 2012 和舊版 toohello 本機安全性授權 (LSA) 安全性封裝的連接。 對於 Windows Server 2012 或較舊版本中的終端機服務版本，您可以[使用 Windows 驗證來保護應用程式](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure)。 如果您是使用 Windows Server 2012 R2，則需要 RD 閘道。

**問：我已在 MFA Server 中設定顯示來電號碼，但我的使用者仍接到使用匿名來電的 Multi-Factor Authentication。**

當透過 hello 公用電話網路放置的 Multi-factor Authentication 通話時，有時候它們路由傳送透過電信業者不支援呼叫者識別碼。 因為這個緣故，呼叫者識別碼不保證，即使 hello Multi-factor Authentication 系統一律會傳送它。

**問： 為什麼我的使用者正在提示的 tooregister 他們的安全性資訊？**
有幾個原因，使用者可能會提示的 tooregister 他們的安全性資訊：

- hello 使用者已啟用 MFA 的系統管理員在 Azure AD 中，但不會有尚未登錄其帳戶的安全性資訊。
- hello 使用者已啟用的自助式密碼重設 Azure AD 中。 hello 安全性資訊會幫助他們重設其密碼的 hello 未來，如果使用者曾忘記。
- hello 使用者存取具有條件式存取原則 toorequire MFA，且先前尚未為 MFA 註冊應用程式。
- hello 使用者正在註冊的裝置與 Azure AD （包括 Azure AD Join），和您的組織需要為裝置註冊 MFA 但 hello 使用者先前尚未註冊為 MFA。
- hello 使用者產生 Windows Hello 企業中 Windows 10 （這需要 MFA） 和先前尚未註冊 MFA。
- hello 組織已建立並啟用已套用的 toohello 使用者註冊 MFA 原則。
- hello 使用者先前註冊 MFA，但選擇驗證方法，因為已停用系統管理員。 hello 使用者因此必須通過 MFA 註冊一次 tooselect 新的預設驗證方法。


## <a name="errors"></a>Errors
**問：如果使用者在使用行動應用程式通知時看到「驗證要求不適用於已啟用的帳戶」錯誤訊息，應該怎麼辦？**

告知 toofollow 此程序 tooremove 他們的帳戶從 hello 行動應用程式，然後再次新增：

1. 跳過[您 Azure 入口網站的設定檔](https://account.activedirectory.windowsazure.com/profile/)並以您的組織帳戶登入。
2. 選取 [其他安全性驗證]。
3. 移除 hello 行動裝置應用程式中的 hello 現有的帳戶。
4. 按一下**設定**，然後依照 hello 指示 tooreconfigure hello 行動裝置應用程式。

**問： 我應該使用者如果？ tooa 非瀏覽器應用程式在登入時，他們會看到 0x800434D4L 錯誤訊息**

當您嘗試 toosign tooa 非瀏覽器應用程式中，不能使用需要雙步驟驗證的帳戶在本機電腦上安裝時，就會發生 hello 0x800434D4L 錯誤。

這項錯誤的因應措施是 toohave 個別使用者帳戶管理員相關和非系統管理作業。 稍後，您可以之間連結信箱您的系統管理員帳戶與非系統管理員帳戶，讓您可以使用非系統管理員帳戶登入 tooOutlook。 如需此解決方案的詳細資訊，了解如何太[能力 tooopen 和檢視 hello 使用者的信箱內容提供系統管理員 hello](http://help.outlook.com/141/gg709759.aspx?sl=1)。

## <a name="next-steps"></a>後續步驟
如果您的問題未在此處找到答案，請將它留在 hello 在 hello hello 頁面底部的註解。 或者，以下是取得協助的一些其他選項︰

* 搜尋 hello [Microsoft 支援知識庫](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport)解決方案 toocommon 技術問題。
* 搜尋和瀏覽 hello 社群的技術問題和解答或詢問您自己的問題在 hello [Azure Active Directory 論壇](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)。
* 如果您是舊版的 PhoneFactor 客戶，而且您有任何疑問或需要重設密碼的說明，使用 hello[密碼重設](mailto:phonefactorsupport@microsoft.com)連結 tooopen 支援案例。
* 請透過 [Azure Multi-Factor Authentication Server (PhoneFactor) 支援](https://support.microsoft.com/oas/default.aspx?prid=14947)連絡支援專業人員。 連絡我們時，請盡量包含有關問題的最多資訊，這樣會十分有幫助。 您可以提供的資訊包括 hello 頁面看到 hello 錯誤、 hello 特定錯誤碼、 hello 特定的工作階段識別碼和 hello 識別碼 hello 使用者看到 hello 錯誤的位置。
